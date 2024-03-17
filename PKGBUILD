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
pkgver="0.1.1"
pkgrel=2
license=(
  'AGPL3'
)
_arch_ns="tallero"
_gh_ns="themartiancompany"
_arch="gitlab.archlinux.org"
_gh="github.com"
_host="${_gh}"
_ns="${_gh_ns}"
_ssh="ssh://git@${_host}:${_ns}/${_pkgbase}"
_local="file://${HOME}/${_pkgbase}"
_http="https://${_host}/${_ns}/${_pkgbase}"
_url="${_http}"
depends=(
  "aspe"
  "reallymakepkg"
  "sus"
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
[[ "${_offline}" == "true" ]] && \
  _url="${_local}"
_branch="master"
source=(
  "${pkgname}::git+${_url}#branch=${_branch}"
)
sha256sums=(
  'SKIP'
)

_parse_ver() {
  local \
    _pkgver="${1}" \
    _out="" \
    _ver \
    _rev \
    _commit
  _ver="$( \
    echo \
      "${_pkgver}" | \
          awk \
            -F '+' \
            '{print $1}')"
  _rev="$( \
    echo \
      "${_pkgver}" | \
      awk \
        -F '+' \
        '{print $2}')"
  _commit="$( \
    echo \
      "${_pkgver}" | \
      awk \
        -F '+' \
        '{print $3}')"
  _out=${_ver}
  [[ "${_rev}" != "" ]] && \
    _out+=".r${_rev}"
  [[ "${_commit}" != "" ]] && \
    _out+=".${_commit}"
  echo \
    "${_out}"
}

pkgver() {
  local \
    _pkgver
  cd \
    "${pkgname}"
  _pkgver="$( \
    git \
      describe \
      --tags | \
      sed \
        's/-/+/g')"
  _parse_ver \
    "${_pkgver}"
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
