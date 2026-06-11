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
_pkg=pciutils
pkgbase="${_pkg}"
pkgname=(
  "${pkgbase}"
)
pkgver=3.15.0
pkgrel=1
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
_http="https://git.kernel.org"
_ns="pub/scm/utils/pciutils"
_url="${_http}/${_ns}/${_pkg}"
source=(
  "git+${_url}.git#tag=v${pkgver}?signed"
)
validpgpkeys=(
  # Martin Mares <mj@ucw.cz>
  "C466A56CADA981F4297D20C31F3D0761D9B65F0B"
)
b2sums=(
  '634c114f928f37e11054c424d0745f8aaa236a342a62e3fae59519619f5d7a1e9f60bb026e5e8949b0b3f636772f62bb9c1743fd73eb97b2a2e3c09d872a2075'
)

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
    "${pkgname}"
  make \
    "${_make_opts[@]}" \
    "lib/libpci.a "
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
    "${pkgname}"
  make \
    "${_make_opts[@]}" \
    install \
    install-lib
  rm \
    -rf \
    "${pkgdir}/usr/share/hwdata"
}
