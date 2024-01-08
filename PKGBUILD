# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>
# Contributor: Fabio Castelli (muflone) <webreg@muflone.com>

_pkgbase=ur
pkgbase="${_pkgbase}-git"
pkgname=(
  "${pkgbase}"
)
pkgdesc="(A)ur helper."
url="https://www.humaninstrumentalityproject.org"
pkgver=0.1
pkgrel=2
license=('AGPL3')
_arch_ns="tallero"
_gh_ns="theamericancompany"
_arch="https://gitlab.archlinux.org"
_gh="https://github.com"
_http="${_gh}"
_url="${_http}/${_ns}/${_pkgbase}"
depends=(
  "aspe"
  "reallymakepkg"
)
makedepends=(
  'git'
)
checkdepends=(
  'shellcheck'
)
optdepends=(
  'git'
)
arch=(
  any
)
_ns="tallero"
source=(
  "${pkgname}::git+${_url}.git"
)
sha256sums=(
  'SKIP'
)

check() {
  cd \
    "${pkgname}"
  make -k check
}

package() {
  local _opts=()
  _opts=(
    DESTDIR="${pkgdir}"
    PREFIX='/usr'
  )
  cd \
    "${pkgname}"
  make \
    "${_opts[@]}" \
    install
}

# vim:set sw=2 sts=-1 et:
