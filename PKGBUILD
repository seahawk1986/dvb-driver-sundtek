# Maintainer: Your Name <youremail@domain.com>
pkgname=dvb-driver-sundtek
pkgver=130109.125056
pkgrel=1yavdr1
pkgdesc="sundtek userspace driver"
arch=('i686' 'x86_64')
url="http://www.sundtek.de/media/"
license=('proprietary')
groups=('drivers')
depends=()
makedepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=dvb-driver-sundtek.install
changelog=
source=(http://www.sundtek.de/media/sundtek_installer_$pkgver.sh)
noextract=()
md5sums=('22724aef35078663bfdceb9bf7797d1a')

build() {
  chmod +x sundtek_installer_${pkgver}.sh
  ./sundtek_installer_${pkgver}.sh -e

  if [ "$CARCH" == x86_64 ]; then
    _arch=64bit
  elif [ "$CARCH" == i686 ]; then
    _arch=32bit
  fi

  tar xzmf ${_arch}/installer.tar.gz -C ${pkgdir}
  # remove obsolete files
  rm -f ${pkgdir}/opt/bin/lirc.sh
  rm -rf ${pkgdir}/etc/udev/rules.d/80-mediasrv.rules
  rm -rf ${pkgdir}/etc/udev/rules.d/80-remote-eeti.rules

  chmod gou=sx ${pkgdir}/opt/bin/mediasrv
  mkdir -p ${pkgdir}/usr/lib/pm-utils/sleep.d
  cp ${pkgdir}/opt/lib/pm/10mediasrv ${pkgdir}/usr/lib/pm-utils/sleep.d/

  mkdir -p ${pkgdir}/usr/include
  ln -s ${pkgdir}/opt/include ${pkgdir}/usr/include/sundtek

  mkdir -p ${pkgdir}/usr/lib/pkgconfig
  ln -s ${pkgdir}/opt/doc/libmedia.pc ${pkgdir}/usr/lib/pkgconfig

  mkdir -p ${pkgdir}/usr/lib/systemd/system/
  cp ${pkgdir}/opt/doc/sundtek.service ${pkgdir}/usr/lib/systemd/system/

  # we use systemctl to enable the service during install
  rm ${pkgdir}/etc/systemd/system/multi-user.target.wants/sundtek.service
}

#package() {
#  cd "$srcdir/$pkgname-$pkgver"

#  make DESTDIR="$pkgdir/" install
#}
