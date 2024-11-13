# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Daniel Wallace <danielwallace at gtmanfred dot com>
# Contributor: Limao Luo <luolimao+AUR@gmail.com>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=pbr
pkgname="${_py}-${_pkg}"
pkgver=6.0.0
pkgrel=4
pkgdesc="Python Build Reasonableness"
arch=(
  'any'
)
url="https://pypi.python.org/pypi/${_pkg}"
license=(
  'Apache-2.0'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  'git'
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-six"
  "${_py}-stestr"
  "${_py}-testresources"
  "${_py}-testscenarios"
  "${_py}-testtools"
  "${_py}-virtualenv"
  "${_py}-sphinx"
  "${_py}-testrepository"
)
_http="https://github.com"
_ns="openstack-dev"
_url="${_http}/${_ns}/${_pkg}"
source=(
  "git+${_url}.git#tag=${pkgver}"
)
sha512sums=(
  '4a998f47307a56f43b95a615128050fb71360a4b3fc8d9e3d539b4f8935ec19533e7b4d55cf763ff4ef3a4ae66806b1242d70980b7805a6b85c1dc4aa59fd190'
)

build() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${_pkg}"
  stestr \
    run \
      --exclude-regex \
        'test_pep_517_support|test_requirement_parsing'
}

package() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      installer \
      --destdir="${pkgdir}" \
      dist/*.whl
  install \
    -Dm644 \
    "LICENSE" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}
