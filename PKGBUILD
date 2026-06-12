# SPDX-License-Identifier: AGPL-3.0

#    -----------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    -----------------------------------------------------
#
#    This program is free software: you can redistribute
#    it and/or modify it under the terms of the
#    GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it
#    will be useful, but WITHOUT ANY WARRANTY;
#    without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#    See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the
#    GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.


# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
#   Tobias Powalowski
#     <tpowa@archlinux.org>

_os="$(
  uname \
    -o)"
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
if [[ "${_os}" == "Android" ]]; then
  _libc="ndk-sysroot"
  _compiler="clang"
  _libcompiler="llvm-libs"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _libc="glibc"
  _compiler="gcc"
  _libcompiler="libgcc"
elif [[ "${_os}" == "Msys" ]]; then
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _sh="sh"
else
  _msg=(
    "Unknown os '${_os}'."
  )
  msg \
    "${_msg[*]}"
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _sh="sh"
fi
if [[ ! -v "_systemd" ]]; then
  if [[ "${_os}" == "GNU/Linux" ]]; then
    _systemd="true"
  else
    _systemd="false"
  fi
fi
if [[ ! -v "_git" ]]; then
  _git="true"
fi
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
fi
if [[ ! -v "_ns" ]]; then
  _ns="pub/scm/utils/pciutils"
  if [[ "${_git_service}" == "github" ]]; then
    _ns="themartiancompany"
  fi
fi
if [[ ! -v "_http" ]]; then
  _http="https://git.kernel.org"
  if [[ "${_git_service}" == "github" ]]; then
    _http="https://${_git_service}.com"
  fi
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _archive_format="zip"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    fi
  fi
fi
_pkg=pciutils
pkgbase="${_pkg}"
pkgname=(
  "${pkgbase}"
)
pkgver=3.15.0
_commit="b424ac8b498317965bfd3ab33ae21b158a7f1dd2"
_bundle_commit="2c24fbf8bf88c297db991a0b45c1926309dc6145"
pkgrel=19
_pkgdesc=(
  "PCI bus configuration space"
  "access library and tools"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  "aarch64"
  "arm"
  "armv7l"
  "armv8l"
  "i686"
  "mips"
  "pentium4"
  "powerpc"
  "x86_64"
)
license=(
  'GPL-2.0-only'
)
url="https://mj.ucw.cz/sw/${_pkg}"
depends=(
  "glibc"
  "hwdata"
  "kmod"
)
if [[ "${_systemd}" == "true" ]]; then
  depends+=(
    "systemd-libs"
  )
fi
makedepends=(
  "make"
  'git'
)
optdepends=(
  'which: for update-pciids'
  'grep: for update-pciids'
  'curl: for update-pciids'
)
source=()
sha256sums=()
_url="${_http}/${_ns}/${_pkg}"
_tag="${_commit}"
_tag_name="commit"
_tarname="${_pkg}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
_bundle_sum="c1e0b0d92eb76ab3eae6975e8df04025b8a5aa3529a743d844065fba5f778d37"
_bundle_sig_sum="02e412a71c0e9eb4d018f26a59dc6bca0a9e3da83c59eaaac32b2e261accc821"
_github_sum="d5cdffa74aca16b6a42ce5caf2e639169fc070e7ff726c9842e91fbfeace229d"
_github_sig_sum="6a247e44cb2b28c6060e370cc71213ca25070bc2543ba5fe70cd98e85de5a57d"
if [[ "${_git}" == "true" ]]; then
  _sum="${_bundle_sum}"
  _sig_sum="${_bundle_sig_sum}"
elif [[ "${_git}" == "false" ]]; then
  _sum="${_github_sum}"
  _sig_sum="${_github_sig_sum}"
fi
# Dvorak
_sig_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
# ffren
_evmfs_ns="0xB6622d419f7BBa353d4e25e99d6BB02Bdb229742"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_sig_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_sig_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_sig_dir}/${_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
if [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _uri="git+${_url}.git#tag=v${pkgver}?signed"
    _src="${_tarfile}::${_uri}"
  elif [[ "${_git}" == false ]]; then
    _uri=""
    if [[ "${_git_service}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/archive/${_commit}.${_archive_format}"
        _sum="${_github_sum}"
      fi
    elif [[ "${_git_service}" == "gitlab" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/-/archive/${_tag}/${_tag}.${_archive_format}"
      fi
    fi
    _src="${_tarfile}::${_uri}"
  fi
elif [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _src="${_evmfs_src}"
    source+=(
      "${_sig_src}"
    )
    sha256sums+=(
      "${_sig_sum}"
    )
  fi
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)
if [[ "${_evmfs}" == "true" ]]; then
  validpgpkeys=(
    # Truocolo
    #   <truocolo@aol.com>
    '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
    #   <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
    'F690CBC17BD1F53557290AF51FC17D540D0ADEED'
    # Pellegrino Prevete (dvorak)
    #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
    '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
  )
elif [[ "${_evmfs}" == "false" ]]; then
  validpgpkeys=(
    # Martin Mares <mj@ucw.cz>
    "C466A56CADA981F4297D20C31F3D0761D9B65F0B"
  )
  if [[ "${_git}" == "true" ]]; then
    b2sums=(
      '634c114f928f37e11054c424d0745f8aaa236a342a62e3fae59519619f5d7a1e9f60bb026e5e8949b0b3f636772f62bb9c1743fd73eb97b2a2e3c09d872a2075'
    )
  fi
fi

build() {
  local \
    _make_opts=()
  _make_opts+=(
    OPT="${CFLAGS}"
    ZLIB="no"
    SHARED="no"
    PREFIX="/usr"
    SHAREDIR="/usr/share/hwdata"
    MANDIR="/usr/share/man"
    SBINDIR="/usr/bin"
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}"
    # "lib/libpci.a "
  cp \
    "lib/libpci.a" \
    "${srcdir}"
  make \
    clean
  make \
    "${_make_opts[@]}" \
    all
}

package() {
  local \
    _make_opts=()
  _make_opts+=(
    SHARED="yes"
    PREFIX="/usr"
    SBINDIR="/usr/bin"
    SHAREDIR="/usr/share/hwdata"
    MANDIR="/usr/share/man"
    DESTDIR="${pkgdir}"
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install \
    install-lib
  rm \
    -rf \
    "${pkgdir}/usr/share/hwdata"
}
