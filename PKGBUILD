# Maintainer: Daniel Wallace <danielwallace at gtmanfred dot com>
# Contributor: Limao Luo <luolimao+AUR@gmail.com>

pkgbase=python-pbr
pkgname=(python-pbr python2-pbr)
pkgver=0.10.0
pkgrel=1
pkgdesc="Python bindings to the OpenStack Identity API (Keystone)"
arch=('any')
url=https://pypi.python.org/pypi/pbr
license=(Apache)
makedepends=(python2-setuptools python-setuptools)
source=(http://pypi.python.org/packages/source/p/${pkgname#*-}/${pkgname#*-}-$pkgver.tar.gz)
sha256sums=('52a61a863566fafa45507a9aa40e6c88edc1e09d96cde5f5a6aa3b4d26c913ce')
sha512sums=('0e83fb57c5104e782da49f6d509371c33904b38aa92c8de851a6f92fe8138b95904d51d269c3b63a4a76bac6439d037e1192ad2010cc535a3741e4a539220da6')

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
}
