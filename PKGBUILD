# Maintainer: Daniel Wallace <danielwallace at gtmanfred dot com>
# Contributor: Limao Luo <luolimao+AUR@gmail.com>

pkgbase=python-pbr
pkgname=(python-pbr python2-pbr)
pkgver=1.8.0
pkgrel=1
pkgdesc="Python Build Reasonableness"
arch=('any')
url=https://pypi.python.org/pypi/pbr
license=(Apache)
makedepends=(python2-setuptools python-setuptools git)
source=(http://pypi.python.org/packages/source/p/${pkgname#*-}/${pkgname#*-}-$pkgver.tar.gz)
sha256sums=('44a0ef9295bb59698f461124741a21a0f7f76d42e160d8a0a4bf1693338036fc')
sha512sums=('e1c1e7f0ebff7d7dc8af6c3a6fe1841ee80a9620b25f4146bd30ccbd2212e6332fa8c2aa1ca044cda2915a8bad6df468bd1dc365c330508fa8f07b8fa231736f')

prepare() {
    cp -a ${pkgname#*-}-$pkgver python2-pbr-$pkgver
    find python2-pbr-$pkgver -name \*.py -exec sed -i '1s/python$/&2/' {} +
}

build() {
    export SKIP_PIP_INSTALL=1
    cd ${pkgname#*-}-$pkgver/
    python setup.py build
    cd $srcdir/python2-pbr-$pkgver
    python2 setup.py build
}

package_python-pbr() {
    cd ${pkgname#*-}-$pkgver/
    depends=(python-pip)
    python setup.py install --prefix=/usr --root="$pkgdir"
    install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
package_python2-pbr() {
    cd $pkgname-$pkgver/
    depends=(python2-pip)
    python2 setup.py install --prefix=/usr --root="$pkgdir"
    install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
    mv $pkgdir/usr/bin/pbr{,2}
}
