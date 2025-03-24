# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2023, 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>

_os="$( \
  uname \
    -o)"
_git='true'
_offline='false'
_solc="true"
_hardhat="true"
_proj="hip"
_Proj="humaninstrumentalityproject"
_py="python"
_contracts="true"
_docs="true"
_pkg=evm-contracts-source-index
_pkgbase="${_pkg}"
_offline="false"
pkgbase="${_pkg}-git"
pkgname=(
  "${pkgbase}"
)
if [[ "${_contracts}" == "true" ]]; then
  pkgname+=(
    "${_pkg}-contracts-git"
  )
fi
if [[ "${_docs}" == "true" ]]; then
  pkgname+=(
    "${_pkg}-docs-git"
  )
fi
_pkgdesc=(
  "Distributed, decentralized,"
  "uncensorable, network-neutral"
  "network-independent Ethereum Virtual"
  "Machine (EVM) smart contracts source"
  "code index and repository using the"
  "Ethereum Virtual Machine File"
  "System (EVMFS) for resources hosting."
)
pkgdesc="${_pkgdesc[*]}"
url="https://${_pkg}.${_Proj}.org"
pkgver=0.1.1.r36.g4d6ca23
pkgrel=1
license=(
  'AGPL3'
)
_branch="master"
_tarname="${_pkg}-${_branch}"
_arch_ns="tallero"
_gh_ns="themartiancompany"
_arch="gitlab.archlinux.org"
_gh="github.com"
_host="${_gh}"
_ns="${_gh_ns}"
_ssh="ssh://git@${_host}:${_ns}/${_pkg}"
_local="file://${HOME}/${_pkg}"
_http="https://${_host}/${_ns}/${_pkg}"
_url="${_http}"
depends=(
  "evm-contracts-tools"
  "evm-gnupg"
  "evm-openpgp-keyserver"
  "evm-wallet"
  "evmfs"
  "libcrash-bash"
  "libevm"
)
makedepends=(
  'evm-make'
  'make'
  "${_py}-docutils"
)
if [[ "${_solc}" == "true" ]]; then
  makedepends+=(
    "solidity=0.8.28"
  )
fi
if [[ "${_hardhat}" == "true" ]]; then
  makedepends+=(
    "hardhat"
  )
fi
group=(
  "${_proj}-git"
)
checkdepends=(
  'shellcheck'
)
provides=(
)
conflicts=(
)
arch=(
  'any'
)
if [[ "${_offline}" == true ]]; then
  _url="${_local}"
fi
if [[ "${_git}" == true ]]; then
  makedepends+=(
    'git'
  )
  _src="${_tarname}::git+${_url}#branch=${_branch}"
elif [[ "${_git}" == false ]]; then
  makedepends+=(
    'curl'
    'jq'
  )
  _src="${_tarname}.tar.gz::${_url}/archive/refs/heads/${_branch}.tar.gz"
fi
source=(
  "${_src}"
)
sha256sums=(
  'SKIP'
)

_nth() {
  local \
    _str="${1}" \
    _n="${2}"
  echo \
    "${_str}" | \
    awk \
      -F '+' \
      '{print $'"${_n}"'}'
}

_jq_pkgver() {
  local \
    _version \
    _rev \
    _commit
  _version="$( \
    curl \
      --silent \
      "${_gh_api}/tags" | \
      jq \
        '.[0].name')"
  _version_commit="$( \
    curl \
      --silent \
      "${_gh_api}/tags" | \
      jq \
        '.[0].commit.sha')"
  _rev="$( \
    curl \
      --silent \
      "${_gh_api}/commits" | \
      jq \
        'map(.sha == '${_version_commit}' ) | index(true)')"
  _commit="$( \
    curl \
      --silent \
      "${_gh_api}/commits" | \
      jq \
        '.[0].sha')"
  printf \
    "%s.r%s.g%s" \
    "${_version}" \
    "${_rev}" \
    "${_commit}"
}

_parse_ver() {
  local \
    _pkgver="${1}" \
    _out="" \
    _ver \
    _rev \
    _commit
  _ver="$( \
    _nth \
      "${_pkgver}" \
      "1")"
  _rev="$( \
    _nth \
      "${_pkgver}" \
      "2")"
  _commit="$( \
    _nth \
      "${_pkgver}" \
      "3")"
  _out=${_ver}
  [[ "${_rev}" != "" ]] && \
    _out+=".r${_rev}"
  [[ "${_commit}" != "" ]] && \
    _out+=".${_commit}"
  echo \
    "${_out}"
}

_git_pkgver() {
  local \
    _pkgver
  _pkgver="$( \
    git \
      describe \
      --tags \
      --long | \
      sed \
        's/-/+/g')"
  _parse_ver \
    "${_pkgver}"
}

pkgver() {
  cd \
    "${_tarname}"
  if [[ "${_git}" == true ]]; then
    _git_pkgver
  elif [[ "${_git}" == false ]]; then
    _jq_pkgver
  fi
}

check() {
  cd \
    "${pkgname}"
  make \
    -k \
    check
}

build() {
  local \
    _make_opts=()
  _make_opts=(
    --debug
  )
  cd \
    "${_tarname}"
  if [[ "${_contracts}" == "true" ]]; then
    if [[ "${_solc}" == "true" ]]; then
      SOLIDITY_COMPILER_BACKEND="solc" \
      make \
        "${_make_opts[@]}" \
        all
    fi
    if [[ "${_hardhat}" == "true" ]]; then
      SOLIDITY_COMPILER_BACKEND="hardhat" \
      make \
        "${_make_opts[@]}" \
        all
    fi
  fi
}

package_evm-contracts-source-index-contracts-git() {
  local \
    _make_opts=()
  provides+=(
    "${_pkg}-contracts=${pkgver}"
  )
  conflicts+=(
    "${_pkg}-contracts"
  )
  _make_opts=(
    DESTDIR="${pkgdir}"
    PREFIX='/usr'
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install-contracts-sources
  make \
    "${_make_opts[@]}" \
    install-contracts-deployments-config
  if [[ "${_solc}" == "true" ]]; then
    make \
      "${_make_opts[@]}" \
      install-contracts-deployments-solc
  fi
  if [[ "${_hardhat}" == "true" ]]; then
    make \
      "${_make_opts[@]}" \
      install-contracts-deployments-hardhat
  fi
}

package_evm-contracts-source-index-git() {
  local \
    _make_opts=()
  depends+=(
    "${_pkg}-contracts"
  )
  provides+=(
    "${_pkg}=${pkgver}"
  )
  conflicts+=(
    "${_pkg}"
  )
  _make_opts=(
    DESTDIR="${pkgdir}"
    PREFIX='/usr'
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install-scripts
}

package_evm-contracts-source-index-docs-git() {
  local \
    _make_opts=()
  provides+=(
    "${_pkg}-docs=${pkgver}"
  )
  conflicts+=(
    "${_pkg}-docs"
  )
  _make_opts=(
    DESTDIR="${pkgdir}"
    PREFIX='/usr'
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install-doc
  make \
    "${_make_opts[@]}" \
    install-man
}

# vim:set sw=2 sts=-1 et:
