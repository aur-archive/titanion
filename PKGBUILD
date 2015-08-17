# Maintainer: Anntoin Wilkinson <anntoin@gmail.com>
# Contributor: Nick Bolten <Shirakawasuna@gmail.com>

pkgname=titanion
pkgver=0.3
pkgrel=12
pkgdesc="An addictive game by Kenta Cho.  Classic shoot-em-up with abstract feel"
arch=('i686' 'x86_64')
license=('custom')
url="http://www.asahi-net.or.jp/~cs8k-cyu/windows/ttn_e.html"
depends=('glu' 'sdl_mixer')
makedepends=('gdc1')
source=('http://abagames.sakura.ne.jp/windows/ttn0_3.zip'
http://ftp.de.debian.org/debian/pool/main/t/${pkgname}/${pkgname}_0.3.dfsg1-4.debian.tar.gz)
md5sums=('33044d2542f93753b5aa1611fbf22e69'
         '4b0b43db98928100d549f2543fd9ff06')

prepare (){
  cd $srcdir/ttn

  _patchdir="../debian/patches/"
  cat $_patchdir/series | egrep -v '^#|^\ #' | sed "s:^:$_patchdir/:" | xargs -n1 patch -p1 -i

  sed -i 's:\/games::' ./src/abagames/util/sdl/{sound,texture}.d \
                       ./src/abagames/ttn/screen.d
  sed -i 's:gdmd-v1:gdmd1:' Makefile
  sed -i 's:gdc-v1:gdc1:' Makefile
}

build (){
  cd $srcdir/ttn
  make
}

package() {
  cd $srcdir/ttn

  # Install binaries
  install -D -m755 $pkgname $pkgdir/usr/bin/$pkgname

  # Install other resources
  find {images,sounds} -type f -exec install -Dm644 {} $pkgdir/usr/share/$pkgname/{} \;

  # Install man page and debian copyright notice
  install -D -m644 ../debian/$pkgname.6 $pkgdir/usr/share/man/man6/$pkgname.6
  install -D -m644 ../debian/copyright $pkgdir/usr/share/licenses/$pkgname/copyright

  # Install desktop file and icon
  install -D -m644 ../debian/$pkgname.desktop $pkgdir/usr/share/applications/$pkgname.desktop
  install -D -m644 ../debian/$pkgname.xpm $pkgdir/usr/share/pixmaps/$pkgname.xpm
}

# vim:set ts=2 sw=2 et:
