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
# Contributors:
#   Tobias Powalowski
#     <tpowa@archlinux.org>
#   Roman Kyrylych
#     <roman@archlinux.org>
#   Sarah Hay
#     <sarah@archlinux.org>

_os="$(
  uname \
    -o)"
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
fi
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
if [[ ! -v "_git_service" ]]; then
  _git_service="gnupg"
  _git_service="github"
fi
_proj=gnupg
if [[ ! -v "_git_http" ]]; then
  if [[ "${_git_service}" == "github" ]]; then
    _git_http="github.com"
  elif [[ "${_git_service}" == "gitlab" ]]; then
    _git_http="gitlab.com"
  elif [[ "${_git_service}" == "${_proj}" ]]; then
    _git_http="dev.${_proj}.org"
  fi
fi
if [[ ! -v "_ns" ]]; then
  if [[ "${_git_service}" == "github" ]]; then
    _ns="themartiancompany"
  elif [[ "${_git_service}" == "gitlab" ]]; then
    _ns="freepg"
  elif [[ "${_git_service}" == "gnupg" ]]; then
    _ns="sources"
  fi
fi
if [[ ! -v "_git" ]]; then
  if [[ "${_git_service}" == "gnupg" ]]; then
    _git="true"
  else
    _git="false"
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
if [[ "${_os}" == "Android" ]]; then
  _locale="C.UTF-8"
else
  _locale="$(
    locale |
      grep \
        "LANG=" |
        awk \
          -F \
            "=" \
          '{print $1}')"
fi
if [[ ! -v "_en" ]]; then
  _en="true"
  if [[ "${_locale}" == "C.UTF-8" ]]; then
    _en="true"
  fi
fi
if [[ ! -v "_it" ]]; then
  _it="true"
  if [[ "${_locale}" == "it_IT.UTF-8" ]]; then
    _it="true"
  fi
fi
if [[ ! -v "_like" ]]; then
  if [[ "${_it}" == "true" ]]; then
    _like="mo-me-lo-segno"
  fi
  if [[ "${_en}" == "true" ]]; then
    _like="never-gonna-give-you-up"
  fi
fi
if [[ ! -v "_tests" ]]; then
  if [[ "${_os}" == "GNU/Linux" ]]; then
    _tests="true"
  elif [[ "${_os}" == "Android" ]]; then
    _tests="false"
  fi
  _tests="false"
fi
_pkg=gpgme
pkgbase="${_pkg}"
pkgname=(
  "${pkgbase}"
)
pkgver=2.0.1
pkgrel=15
_commit="e4adebe020b07bc47e583817576ce98ca93e9711"
_bundle_commit="63f18298d3f5c5f7551301b1e183890c503c644a"
_gnupg_pkgver=2.5
_libassuan_pkgver=3.0.2
_pkgdesc=(
  'C wrapper library for GnuPG.'
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'aarch64'
  'arm'
  'armv7l'
  'armv8l'
  'i686'
  'mips'
  'pentium4'
  'powerpc'
  'x86_64'
)
url="https://www.${_proj}.org/related_software/${_pkg}"
license=(
  "GPL-2.0-or-later"
  "LGPL-2.0-or-later"
  "LGPL-2.1-or-later"
  "MIT"
)
depends=(
  # I think its very
  # possible it implicitly depends
  # (same as all architecture
  #  dependent packages) on
  # ${_compiler}"
  # ${_libcompiler}"
  "${_libc}"
  "libassuan>=${_libassuan_pkgver}"
  "libassuan.so"
  "libgpg-error"
  # 'libgpg-error.so'
  "gnupg>=${_gnupg_pkgver}"
)
makedepends=(
  "autoconf"
  "automake"
  "libassuan>=${_libassuan_pkgver}"
  "libtool"
  "libgpg-error"
  "${_libc}"
  "${_compiler}"
  "${_libcompiler}"
)
if [[ "${_os}" == "Msys" ]]; then
  makedepends+=(
    "${_libc_headers}"
    "windows-default-manifest"
  )
fi
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    'git'
  )
fi
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs" 
  )
fi
provides=(
  "lib${_pkg}.so"
)
options=(
  '!emptydirs'
)
_http="https://${_git_http}"
_url="${_http}/${_ns}/${_pkg}"
_tag_name="commit"
if [[ "${_tag_name}" == "commit" ]]; then
  _tag="${_commit}"
elif [[ "${_tag_name}" == "tag" ]]; then
  if [[ "${_git_service}" == "gnupg" ]]; then
    _tag="${_pkg}-${pkgver}"
  fi
fi
_tarname="${_pkg}-${_tag}"
_tarfile="${_pkg}-${_tag}.${_archive_format}"
_gitlab_sum="SKIP"
_gitlab_sig_sum="SKIP"
_github_sum="fb66dc0ce1b197f751c47ace83740081164fece8ab7c1a72d07c5f15a1459776"
_github_sig_sum="1b2404370def242a47ec9a6b06beac44fa3a274277261f7bb797d03bf0223ce4"
_bundle_sum="5143c5caf0b19b5907db4b788f5c4bf261a838d158e70aab7303f110a75b20ba"
_bundle_sig_sum="c3d3b354f9e1303847f0cf00b79782490ed8498aa9e2568e3c8e6c3246fa863d"
# that crazy kid address
_kid_ns="0x926acb6aA4790ff678848A9F1C59E578B148C786"
# Dvorak
_dvorak_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
# Tallero
_evmfs_ns="0x6ec7cC56dCeC0a00CB15E97C64B1a5Ec7A31403c"
# Truocolo
_truocolo_ns="0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b"
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _sum="${_bundle_sum}"
    _sig_sum="${_bundle_sig_sum}"
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _sum="${_github_sum}"
      _sig_sum="${_github_sig_sum}"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _sum="${_gitlab_sum}"
      _sig_sum="${_gitlab_sig_sum}"
    fi
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_tag_name}" == "tag" ]]; then
      _sum='SKIP'
    elif [[ "${_tag_name}" == "commit" ]]; then
      _sum="SKIP"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _sum="${_github_sum}"
      _sig_sum="${_github_sig_sum}"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _sum="${_gitlab_sum}"
      _sig_sum="${_gitlab_sig_sum}"
    fi
  fi
fi
_evmfs_ns="${_truocolo_ns}"
_evmfs_sig_ns="${_dvorak_ns}"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  _src="${_evmfs_src}"
  source+=(
    "${_sig_src}"
  )
  sha256sums+=(
    "${_sig_sum}"
  )
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == true ]]; then
    _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}"
    _sum="SKIP"
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
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)
validpgpkeys=(
  # Werner Koch (dist signing 2020)
  '6DAA6E64A76D2840571B4902528897B826403ADA'
  # Niibe Yutaka (GnuPG Release Key)
  'AC8E115BF73E2D8D47FA9908E98E9B2D19C6C8BD'
  # Truocolo
  #   <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  'DD6732B02E6C88E9E27E2E0D5FC6652B9D9A6C01'
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

prepare() {
  cd \
    "${_tarname}"
  sed \
    -i \
    's/-unknown//' \
    "autogen.sh"
  autoreconf \
    -fi
}

build() {
  local \
    _configure_opts=()
  _configure_opts+=(
    --prefix="/usr"
    --disable-fd-passing
    --disable-static
    # This is disabled on GNU too
    --disable-gpgsm-test
  )
  if [[ "${_tests}" == "false" ]]; then
    _configure_opts+=(
      --disable-gpgconf-test
      --disable-gpg-test
      --disable-g13-test
    )
  fi
  cd \
    "${_tarname}"
  ./configure \
    "${_configure_opts[@]}"
  # prevent excessive overlinking due to libtool
  sed \
    -i \
    -e \
    's/ -shared / -Wl,-O1,--as-needed\0/g' \
    "libtool"
  make
}

check() {
  cd \
    "${_tarname}"
  # this test fails with gnupg (FS#66572)
  sed \
    -i \
    's#"t-keylist-secret",##' \
    "tests/json/t-json.c"
  make \
    check
}

package() {
  local \
    _make_opts=()
  _make_opts+=(
    DESTDIR="${pkgdir}"
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install
  # that is not used, no?!
  rm \
    "${pkgdir}/usr/lib/pkgconfig/${_pkg}-glib.pc"
  install \
    -vDm644 \
    "LICENSES" \
    "${pkgdir}/usr/share/licenses/${pkgname}/MIT.txt"
}
