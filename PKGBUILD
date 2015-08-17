# Maintainer: Swift Geek <swifgeek ɐ google m č0m>

pkgname=vsprog-svn
pkgver=a
pkgrel=1
pkgdesc="Versaloon Programmer Platform is a generic framework for MCU programming"
arch=("i686" "x86_64")
url="http://www.versaloon.com/"
license=('GPL3')
depends=('libusb' 'libxml2')
makedepends=('subversion')
provides=('vsprog')
source=("$pkgname::svn+http://vsprog.googlecode.com/svn/trunk/")
#source=("$pkgname::svn+http://vsprog.googlecode.com/svn/trunk/#revision=1442")
md5sums=('SKIP')

pkgver() {
  cd "${srcdir}/${pkgname}"
  svnversion
}

build() {
  cd "${pkgname}"
  chmod a+x ./bootstrap
  ./bootstrap
  ./configure --enable-maintainer-mode --prefix=/usr
  make
}

package() {
  cd "${pkgname}"
  make DESTDIR="${pkgdir}" install

  # UDEV rule
  # /dev/ttyACM* access is needed anyway, which belongs to uucp
  install -d "${pkgdir}/usr/lib/udev/rules.d/"
#  install -m644 "${srcdir}/dongle/driver/linux/60-versaloon.rules" "${pkgdir}/usr/lib/udev/rules.d/"
  echo 'SUBSYSTEM=="usb", ATTRS{idVendor}=="0483", ATTRS{idProduct}=="a038", GROUP="uucp", MODE="0666"' > ${pkgdir}/usr/lib/udev/rules.d/60-versaloon.rules
}
