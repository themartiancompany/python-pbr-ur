# Maintainer: Daniel Wallace <danielwallace at gtmanfred dot com>
# Contributor: Limao Luo <luolimao+AUR@gmail.com>

pkgbase=python-pbr
pkgname=(python-pbr python2-pbr)
pkgver=1.6.0
pkgrel=1
pkgdesc="Python Build Reasonableness"
arch=('any')
url=https://pypi.python.org/pypi/pbr
license=(Apache)
makedepends=(python2-setuptools python-setuptools git)
source=(http://pypi.python.org/packages/source/p/${pkgname#*-}/${pkgname#*-}-$pkgver.tar.gz)
sha256sums=('4eaee8ff5544703edd1951ed1dc0b283da99a74f740d9f9055eeefcf329de1d1')
sha512sums=('a0393cc7774ea3e181ba75c976f5961686afeb214d8c16f3fdd3838154323cd856ded759cae1c6a25b0371c72d95e579b04de0902d56c432ef137f820032c0fd')

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
