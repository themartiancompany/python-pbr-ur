# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Daniel Wallace <danielwallace at gtmanfred dot com>
# Contributor: Limao Luo <luolimao+AUR@gmail.com>

pkgbase=python-pbr
pkgname=(python-pbr python2-pbr)
pkgver=1.10.0
pkgrel=1
pkgdesc="Python Build Reasonableness"
arch=('any')
url=https://pypi.python.org/pypi/pbr
license=('Apache')
makedepends=('python2-setuptools' 'python-setuptools' 'git')
checkdepends=('python-testscenarios' 'python2-testscenarios' 'python-testrepository' 'python2-testrepository'
              'python-testresources' 'python2-testresources' 'python-mock' 'python2-mock' 'python-virtualenv'
              'python2-virtualenv' 'python-wheel' 'python2-wheel' 'python-sphinx' 'python2-sphinx')
source=("git+https://git.openstack.org/openstack-dev/pbr#tag=$pkgver")
sha512sums=('SKIP')

prepare() {
  cp -a pbr{,-py2}

  find pbr-py2 -name \*.py -exec sed -i '1s/python$/&2/' {} +
}

build() {
  cd "$srcdir"/pbr
  python setup.py build

  cd "$srcdir"/pbr-py2
  python2 setup.py build
}

check() {
  cd "$srcdir"/pbr
  python setup.py test || warning "Tests failed"

  cd "$srcdir"/pbr-py2
  PYTHON=python2 python2 setup.py test || warning "Tests failed"
}

package_python-pbr() {
  depends=('python-setuptools')

  cd pbr
  python setup.py install -O1 --root="$pkgdir"
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-pbr() {
  depends=('python2-setuptools')

  cd pbr-py2
  python2 setup.py install -O1 --root="$pkgdir"
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
  
  mv "$pkgdir"/usr/bin/pbr{,2}
}
