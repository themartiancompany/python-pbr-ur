# Maintainer: Daniel Wallace <danielwallace at gtmanfred dot com>
# Contributor: Limao Luo <luolimao+AUR@gmail.com>

pkgbase=python-pbr
pkgname=(python-pbr python2-pbr)
pkgver=0.8.0
pkgrel=1
pkgdesc="Python bindings to the OpenStack Identity API (Keystone)"
arch=('any')
url=https://pypi.python.org/pypi/pbr
license=(Apache)
makedepends=(python2-setuptools python-setuptools)
source=(http://pypi.python.org/packages/source/p/${pkgname#*-}/${pkgname#*-}-$pkgver.tar.gz)
sha256sums=('799cbdd896806ffa736bca0021aa61619fee5813148f8418366c690af80ee94a')
sha512sums=('feae0eab60a5f64ac8dda519af6b9e671014d42a3ae77cd15080b034872d1d69e87f754caf082479943def7ff5bfb11a3b1524de236e189bc496e3688791aff4')

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
