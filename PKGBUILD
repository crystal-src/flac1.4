# Maintainer: Eric Belanger <eric@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>

pkgname=flac
pkgver=1.2.1
pkgrel=1
pkgdesc="Free Lossless Audio Codec"
arch=('i686' 'x86_64')
url="http://flac.sourceforge.net/"
license=('custom:Xiph' 'LGPL' 'GPL' 'FDL')
depends=('glibc' 'libogg')
makedepends=('nasm' 'xmms')
options=('!libtool' '!makeflags')
source=(http://downloads.sf.net/sourceforge/$pkgname/$pkgname-$pkgver.tar.gz flac-1.2.1-gcc-4.3-includes.patch)
md5sums=('153c8b15a54da428d1f0fadc756c22c7' 'b9d245422bbc547b18a72897366bea77')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  patch -Np1 -i "${srcdir}/flac-1.2.1-gcc-4.3-includes.patch" || return 1
  ./configure --prefix=/usr --enable-shared --disable-sse \
    --disable-rpath --with-pic || return 1
  make || return 1
  make DESTDIR="${pkgdir}" install || return 1

  # install license
  install -Dm0644 COPYING.Xiph "${pkgdir}/usr/share/licenses/${pkgname}/COPYING.Xiph" || return 1
}
