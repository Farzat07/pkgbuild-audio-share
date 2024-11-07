# Maintainer: A Farzat <a@farzat.xyz>
# Contributor: Zhanibek Adilbekov <zhnaibek.adilbekov@proton.me>
# shellcheck disable=2034,2154
pkgname=audio-share
pkgver=0.2.0
pkgrel=1
pkgdesc="Audio Share can share computer's audio to Android phone over network, so your phone becomes the speaker of computer"
arch=('x86_64')
url='https://github.com/mkckr0/audio-share'
license=('Apache-2.0')
depends=('libpipewire')
makedepends=('vcpkg' 'cmake' 'git')
source=("$pkgname-$pkgver.tar.gz::https://github.com/mkckr0/audio-share/archive/refs/tags/v${pkgver}.tar.gz"
        "git+https://github.com/microsoft/vcpkg")
b2sums=('58acad53ceed9d7250cf42dcbf8b7d524498b25dcdb3a6858438d46f9563c0d4badca6459224916a5031194e863a403790ccca4180bc2e4c8cd400f586f28c4f'
        'SKIP')

build() {
  export VCPKG_ROOT="$PWD/vcpkg"
  vcpkg install --downloads-root="$PWD/cache" --vcpkg-root="$VCPKG_ROOT" --binarysource=clear asio protobuf spdlog cxxopts
  cd "$pkgname-$pkgver/server-core"
  cmake --preset linux-Release
  cmake --build --preset linux-Release
}

package() {
  install -Dm755 "$srcdir/$pkgname-$pkgver/server-core/out/install/linux-Release/bin/as-cmd" "$pkgdir/usr/bin/as-cmd"
}

# vim: ts=2 sw=2 et
