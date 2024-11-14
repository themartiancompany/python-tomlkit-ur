# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Felix Yan <felixonmars@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>

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
_pkg=tomlkit
_pkgname="${_pkg}"
pkgname="${_py}-${_pkg}"
pkgver=0.13.0
pkgrel=1
pkgdesc='Style-preserving TOML library for Python'
_ns="sdispater"
url="https://github.com/${_ns}/$_pkgname"
license=(
  MIT
)
arch=(
  any
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-"{"build","installer","wheel"}
  "${_py}-poetry-core"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-yaml"
)
_archive="${_pkg}-${pkgver}"
_pypi="https://files.pythonhosted.org/packages/source"
source=(
  "${_pypi}/${_pkg::1}/${_pkg}/${_archive}.tar.gz"
)
sha256sums=(
  '08ad192699734149f5b97b45f1f18dad7eb1b6d16bc72ad0c2335772650d7b72'
)

build() {
  cd \
    "${_archive}"
  "${_py}" \
    -m \
      build \
    -wn
}

check() {
  cd \
    "${_archive}"
  pytest
}

package() {
  cd \
    "${_archive}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm0644 \
    -t \
    "$pkgdir/usr/share/licenses/$pkgname/" \
    "LICENSE"
}
