# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Daniel Wallace <danielwallace at gtmanfred dot com>
# Contributor: Limao Luo <luolimao+AUR@gmail.com>

pkgbase=python-pbr
pkgname=(python-pbr python2-pbr)
pkgver=4.0.3
pkgrel=1
pkgdesc="Python Build Reasonableness"
arch=('any')
url='https://pypi.python.org/pypi/pbr'
license=('Apache')
makedepends=('python2-setuptools' 'python-setuptools' 'git')
checkdepends=('python-testscenarios' 'python2-testscenarios' 'python-testrepository' 'python2-testrepository'
              'python-testresources' 'python2-testresources' 'python-mock' 'python2-mock' 'python-virtualenv'
              'python2-virtualenv' 'python-wheel' 'python2-wheel' 'python-sphinx' 'python2-sphinx')
source=("$pkgbase-$pkgver.tar.gz::https://github.com/openstack-dev/pbr/archive/$pkgver.tar.gz")
sha512sums=('354fef43cc2c4a615df0940a940f78a2c98e9edcbc8f4bc5e7e7743081ab3826cadf78a5a8e67468628d7a856d60c5eab8a713b1058cc511853ed156cacd684d')

prepare() {
  cp -a pbr-$pkgver{,-py2}

  find pbr-$pkgver-py2 -name \*.py -exec sed -i '1s/python$/&2/' {} +

  export PBR_VERSION=$pkgver
}

build() {
  cd "$srcdir"/pbr-$pkgver
  python setup.py build

  cd "$srcdir"/pbr-$pkgver-py2
  python2 setup.py build
}

check() {
  cd "$srcdir"/pbr-$pkgver
  python setup.py testr || warning "Tests failed"

  cd "$srcdir"/pbr-$pkgver-py2
  PYTHON=python2 python2 setup.py testr || warning "Tests failed"
}

package_python-pbr() {
  depends=('python-setuptools')

  cd pbr-$pkgver
  python setup.py install -O1 --root="$pkgdir"
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-pbr() {
  depends=('python2-setuptools')

  cd pbr-$pkgver-py2
  python2 setup.py install -O1 --root="$pkgdir"
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
  
  mv "$pkgdir"/usr/bin/pbr{,2}
}
