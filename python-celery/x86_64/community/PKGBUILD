# Maintainer: qontinuum <qontinuum@artixlinux.org>
# Contributor: Marcin Kolenda <marcinkolenda419@gmail.com>
# Contributor: Valentin Haloiu <vially.ichb+aur@gmail.com>
# Contributor: Lukas Linhart <bugs@almad.net>
# Contributor: Marco Elver <marco.elver AT gmail.com>
# Contributor: apkawa <apkawa@gmail.com>

pkgname=python-celery
pkgver=5.2.7
pkgrel=2
pkgdesc='Distributed Asynchronous Task Queue'
arch=('any')
url='http://celeryproject.org/'
license=('BSD')
depends=('python-billiard' 'python-click-didyoumean' 'python-click-plugins' 'python-click-repl'
         'python-kombu' 'python-pytz' 'python-vine')
optdepends=('python-cryptography: for celery.security'
            'python-pymongo: for celery.backends.mongodb'
            'python-msgpack: for using the msgpack serializer'
            'python-pyro: for using Pyro4 message transport'
            'python-redis: for celery.backends.redis'
            'python-sqlalchemy: for celery.backends.database'
            'python-boto3: for SQS transport'
            'python-yaml: for using the yaml serializer'
            'python-pyzmq: for using ZeroMQ transport')
makedepends=('python-setuptools')
# checkdepends on systemd for sysusers hook to create 'bin' user, because celery's test suite requires gid 1 to exist
checkdepends=('python-pytest-celery' 'python-pytest-subtests' 'python-pytest-timeout' 'python-case'
              'python-cryptography' 'python-gevent' 'python-pymongo' 'python-msgpack' 'python-pyro'
              'python-redis' 'python-sqlalchemy' 'python-boto3' 'python-yaml' 'python-pyzmq'
              'python-eventlet' 'python-moto' 'etmpfiles')
source=("https://pypi.io/packages/source/c/celery/celery-$pkgver.tar.gz"
        celery.tmpfiles.d)
options=('!emptydirs')
sha512sums=('68e3bb082f97ebe20391293cc8fa96c41c8f5ac5e8c24b2b7bd66eb104ec459bdfa49741e47486676e5daa88d7a71e3eb0d9432851aeafc74b0d4352e567e853'
            '67279b75c3b44d065811c9c90aee006296164000912d5bb97c74956b26ee4ad4f0847e846052a896d379848b869c849300367e676d3f689cf29e3a0c7ae5310b')

build() {
  cd celery-$pkgver
  python setup.py build
}

check() {
  cd celery-$pkgver
  # t/unit/apps/test_multi.py & t/unit/bin/test_multi.py: needs write permission to /var/run/celery
  python -m pytest --deselect t/unit/apps/test_multi.py --deselect t/unit/bin/test_multi.py
}

package() {
  cd celery-$pkgver
  python setup.py install --root="$pkgdir" --optimize=1 --skip-build
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
  install -Dm644 "$srcdir"/celery.tmpfiles.d "$pkgdir"/usr/lib/tmpfiles.d/celery.conf
}
