# Maintainer: Doug Newgard <scimmia at archlinux dot info>
# Contributor: Andrey Mivrenik <gim at fastmail dot fm>
# Contributor: Glen Oakley <goakley123@gmail.com>

_piver=""

_qmake="qmake"
if [[ -z $_piver ]] && [[ -n $LOCAL_PI_VER ]]; then
  _piver=$LOCAL_PI_VER
fi

if [[ -n "$_piver" ]]; then
  _qmake="/opt/qt-sdk-raspberry-pi${_piver}/bin/qmake"
fi

_pkgname=cool-retro-term
pkgname=$_pkgname-git
pkgver=1.0.0.r51.g69d35a7
pkgrel=1
pkgdesc='A good looking terminal emulator which mimics the old cathode display'
arch=('any')
url='https://github.com/Swordfish90/cool-retro-term'
license=('GPL3')
depends=('qmltermwidget-git')
makedepends=('git' 'qt-sdk-raspberry-pi${_piver}')
provides=("$_pkgname=$pkgver")
conflicts=("$_pkgname")
install=$_pkgname.install
source=("git://github.com/Swordfish90/cool-retro-term.git")
sha256sums=('SKIP')

prepare() {
  cd "$srcdir/$_pkgname"

  sed -i '/qmltermwidget/d' cool-retro-term.pro
}

pkgver () {
  cd "$srcdir/$_pkgname"

  git describe --tags --long | sed -r 's/^v//;s/-RC/RC/;s/([^-]*-g)/r\1/;s/-/./g'
}

build() {
  cd "$srcdir/$_pkgname"

  $_qmake
  make
}

package() {
  local systemd_deploy_path=${pkgdir}/usr/lib/systemd/system
  cd "$srcdir/$_pkgname"

  make INSTALL_ROOT="$pkgdir" install

  mkdir -p ${systemd_deploy_path}

  cp ${startdir}/*.service ${systemd_deploy_path}
}
