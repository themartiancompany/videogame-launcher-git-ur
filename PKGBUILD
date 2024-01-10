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
pkgdesc="(A)ur helper"
url="https://www.humaninstrumentalityproject.org"
pkgver="v0.1.1"
pkgrel=2
license=(
  'AGPL3')
_arch_ns="tallero"
_gh_ns="theamericancompany"
_arch="gitlab.archlinux.org"
_gh="github.com"
_host="${_gh}"
_ns="${_gh_ns}"
_ssh="ssh://git@${_host}:${_ns}/${_pkgbase}"
_local="file://${HOME}/${_pkgbase}"
_http="https://${_host}/${_ns}/${_pkgbase}"
# _url="${_local}"
_url="${_http}"
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
source=(
  "${pkgname}::git+${_url}.git"
  # "${pkgname}::git+${_local}"
)
sha256sums=(
  'SKIP'
)

pkgver() {
  cd \
    "${pkgname}"
  git \
    describe \
    --tags | \
    sed 's/-/+/g'
}

check() {
  cd \
    "${pkgname}"
  make \
    -k \
    check
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
