# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Eric Bélanger <eric@archlinux.org>

pkgname=flac1.4
pkgver=1.4.3
pkgrel=1
pkgdesc='Free Lossless Audio Codec'
url='https://xiph.org/flac/'
arch=('x86_64')
license=('BSD' 'GPL')
depends=('gcc-libs' 'libogg')
makedepends=('nasm' 'cmake' 'ninja' 'doxygen')
source=(https://github.com/xiph/flac/releases/download/${pkgver}/flac-${pkgver}.tar.xz)
b2sums=('c4f441aeaa0493433347b8a110ca01865fd40d5b21150174372af2fee4fa5c3397a67add31138e92999eab9d9abe6c46a5ac29e13cbac60093fbff6d7a672ad3')

# https://github.com/xiph/flac/releases
sha256sums=('6c58e69cd22348f441b861092b825e591d0b822e106de6eb0ee4d05d27205b70')

prepare() {
  cd flac-${pkgver}

  # Shorten tests
  sed -i 's/FLAC__TEST_LEVEL=1/FLAC__TEST_LEVEL=0/' test/CMakeLists.txt
}

build() {
  cmake -S flac-${pkgver} -B build -G Ninja \
    -DCMAKE_BUILD_TYPE=None \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DBUILD_PROGRAMS=OFF \
    -DBUILD_EXAMPLES=OFF \
    -DBUILD_TESTING=OFF \
    -DBUILD_DOCS=OFF \
    -DBUILD_SHARED_LIBS=ON \
    -DINSTALL_MANPAGES=OFF \
    -DINSTALL_PKGCONFIG_MODULES=OFF \
    -DINSTALL_CMAKE_CONFIG_MODULE=OFF \
    -DWITH_STACK_PROTECTOR=OFF \
    -DNDEBUG=ON
  cmake --build build
}

package() {
  provides=('libFLAC.so.12' 'libFLAC++.so.10')

  DESTDIR="${pkgdir}" cmake --install build
  rm -rf "${pkgdir}/usr/lib/libFLAC.so" "${pkgdir}/usr/lib/libFLAC++.so" "${pkgdir}/usr/include"
}

# vim:set sw=2 sts=-1 et:
