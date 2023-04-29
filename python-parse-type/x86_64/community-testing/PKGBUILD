# Maintainer: Qontinuum <qontinuum@artixlinux.org>

pkgname=python-parse-type
pkgver=0.6.0
pkgrel=3
pkgdesc="Simplifies to build parse types based on the parse module"
url="https://github.com/jenisys/parse_type"
license=('BSD')
arch=('any')
depends=('python-parse' 'python-six')
makedepends=('python-setuptools')
checkdepends=('python-pytest' 'python-pytest-html')
source=("https://github.com/jenisys/parse_type/archive/v$pkgver/$pkgname-$pkgver.tar.gz")
sha512sums=('cbe2c8d2bac567cb89b600ef4b0fb5e65c5afdb8e83c3da01cf0b80ce40630c6fb0e1156e352f8b64d5b6d69555126edfbd3f48c6482f7fe8cfb79fcff8ac5b7')

build() {
  cd parse_type-$pkgver
  python setup.py build
}

check() {
  cd parse_type-$pkgver
  pytest
}

package() {
  cd parse_type-$pkgver
  python setup.py install --root="$pkgdir" --optimize=1

  install -Dm644 LICENSE -t "$pkgdir"/usr/share/licenses/$pkgname/
}
