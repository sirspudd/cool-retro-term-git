# Maintainer: Doug Newgard <scimmia at archlinux dot info>
# Contributor: Andrey Mivrenik <gim at fastmail dot fm>
# Contributor: Glen Oakley <goakley123@gmail.com>

_pi_ver=2
_pkgname=cool-retro-term
pkgname=$_pkgname-git
pkgver=1.0.0.r39.g64e6208
pkgrel=1
pkgdesc='A good looking terminal emulator which mimics the old cathode display'
arch=('any')
url='https://github.com/Swordfish90/cool-retro-term'
license=('GPL3')
depends=('qmltermwidget-git' 'qt-sdk-raspberry-pi2-target-libs')
makedepends=('git')
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
  local qmake=/opt/qt-sdk-raspberry-pi${_pi_ver}/bin/qmake

  $qmake
  make
}

package() {
  cd "$srcdir/$_pkgname"

  make INSTALL_ROOT="$pkgdir" install
}
