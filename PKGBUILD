# Based on Arch's PKGBUILD by Laurent Carlier <lordheavym@gmail.com>
# Modified by Tk-Glitch <ti3nou at gmail dot com> to target git instead of tagged releases

pkgname=vulkan-headers-tkg-git
pkgver=1.3.288.r6.ge3c37e6
pkgrel=1
pkgdesc="Vulkan header files"
arch=(any)
url="https://www.khronos.org/vulkan/"
license=('APACHE')
makedepends=(cmake git ninja)
provides=("vulkan-hpp=${pkgver}" "vulkan-headers=${pkgver}")
conflicts=("vulkan-headers")
groups=(vulkan-devel)
source=("${pkgname}::git+https://github.com/KhronosGroup/Vulkan-Headers.git")
sha256sums=('SKIP')

prepare() {
  cd "${pkgname}"
  git checkout main
}

pkgver() {
  cd "${pkgname}"
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g;s/^v//;s/\.rc/rc/;s/^wine\.//'
}

build() {
  cd "$srcdir/${pkgname}" && rm -rf build

  cmake -G Ninja -B build \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=Release \
    -Wno-dev
  cmake --build build
}

package() {
  cd "$srcdir/${pkgname}"

  DESTDIR="${pkgdir}" cmake --install build
  install -Dm644 -t "$pkgdir"/usr/share/licenses/$pkgname LICENSES/MIT.txt
}
