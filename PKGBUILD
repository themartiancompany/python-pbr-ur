# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Daniel Wallace <danielwallace at gtmanfred dot com>
# Contributor: Limao Luo <luolimao+AUR@gmail.com>

pkgbase=python-pbr
pkgname=(python-pbr python2-pbr)
pkgver=1.9.1
pkgrel=1
pkgdesc="Python Build Reasonableness"
arch=('any')
url=https://pypi.python.org/pypi/pbr
license=('Apache')
makedepends=('python2-setuptools' 'python-setuptools' 'git')
checkdepends=('python-testscenarios' 'python2-testscenarios' 'python-testrepository' 'python2-testrepository'
              'python-testresources' 'python2-testresources' 'python-mock' 'python2-mock' 'python-virtualenv'
              'python2-virtualenv' 'python-wheel' 'python2-wheel' 'python-sphinx' 'python2-sphinx')
source=(http://pypi.python.org/packages/source/p/pbr/pbr-$pkgver.tar.gz)
sha512sums=('02c05652ee7504ec45330ab281be5880d70aa8017b1181446323d811b97e0c2deb6b3ff693516e32dd9ba2ecc653b13dbe33114e52414e78a478f5374b195cf1')

prepare() {
  cp -a pbr-$pkgver{,-py2}

  find pbr-$pkgver-py2 -name \*.py -exec sed -i '1s/python$/&2/' {} +
}

build() {
  cd "$srcdir"/pbr-$pkgver
  python setup.py build

  cd "$srcdir"/pbr-$pkgver-py2
  python2 setup.py build
}

check() {
  cd "$srcdir"/pbr-$pkgver
  python setup.py test || warning "Tests failed"

  cd "$srcdir"/pbr-$pkgver-py2
  PYTHON=python2 python2 setup.py test || warning "Tests failed"
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
