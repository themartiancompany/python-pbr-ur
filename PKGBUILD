# Maintainer: Daniel Wallace <danielwallace at gtmanfred dot com>
# Contributor: Limao Luo <luolimao+AUR@gmail.com>

pkgbase=python-pbr
pkgname=(python-pbr python2-pbr)
pkgver=0.10.8
pkgrel=1
pkgdesc="Python bindings to the OpenStack Identity API (Keystone)"
arch=('any')
url=https://pypi.python.org/pypi/pbr
license=(Apache)
makedepends=(python2-setuptools python-setuptools)
source=(http://pypi.python.org/packages/source/p/${pkgname#*-}/${pkgname#*-}-$pkgver.tar.gz)
sha256sums=('a741650c697abe9dd3da00039a57a45a15a6eed017a16f6b7e4c0161fae2b4b2')
sha512sums=('d79455288657ca07e38a64393d54bda8f88b75242b929ea9f88ac809ba88fffa4793eba0459cae368d822164de5a89721c77fadd05ab624db5897f6cf447b1f4')

prepare() {
    cp -a ${pkgname#*-}-$pkgver python2-pbr-$pkgver
    find python2-pbr-$pkgver -name \*.py -exec sed -i '1s/python$/&2/' {} +
}

build() {
    cd ${pkgname#*-}-$pkgver/
    python setup.py build
    cd $srcdir/python2-pbr-$pkgver
    python2 setup.py build
}

package_python-pbr() {
    cd ${pkgname#*-}-$pkgver/
    depends=(python)
    python setup.py install --prefix=/usr --root="$pkgdir"
    install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
package_python2-pbr() {
    cd $pkgname-$pkgver/
    depends=(python2)
    python2 setup.py install --prefix=/usr --root="$pkgdir"
    install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
    mv $pkgdir/usr/bin/pbr{,2}
}
