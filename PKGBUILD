# Maintainer: Davorin Učakar <davorin.ucakar@gmail.com>
# Contributor: Sven-Hendrik Haase <sh@lutzhaase.com>
# Contributor: Stefan Husmann <stefan-husmann@t-online.de>
# Contributor: Mihai Militaru <mihai.militaru@gmx.com>
# Contributor: scippio <scippio@berounet.cz>

pkgname=mingw32-freeimage
pkgver=3.15.4
pkgrel=2
pkgdesc="Library project for developers who would like to support popular graphics image formats (mingw32)."
arch=('any')
license=('GPL' 'custom:FIPL')
url="http://freeimage.sourceforge.net/"
depends=('mingw32-runtime' 'freeimage')
makedepends=('mingw32-gcc')
options=(!strip !buildflags)
source=("http://downloads.sourceforge.net/sourceforge/freeimage/FreeImage${pkgver//./}.zip"
        'openexr.patch')
sha1sums=('1d30057a127b2016cf9b4f0f8f2ba92547670f96'
          '48cc72441ab9aa0d3ace8fe1c1959908871c1bd0')

prepare() {
  cd "${srcdir}/FreeImage"
  
  patch -p1 -i "${srcdir}/openexr.patch"
}

build() {
  cd "${srcdir}/FreeImage"
  
  unset LDFLAGS
  make \
    CC="i486-mingw32-gcc" \
    CXX="i486-mingw32-g++" \
    LD="i486-mingw32-g++" \
    RC="i486-mingw32-windres" \
    AR="i486-mingw32-ar" \
    DLLTOOL="i486-mingw32-dlltool" \
    -f Makefile.mingw
}

package() {
  cd "${srcdir}/FreeImage"

  install -Dm644 Dist/FreeImage.dll "${pkgdir}/usr/i486-mingw32/bin/FreeImage.dll"
  install -Dm644 Dist/FreeImage.lib "${pkgdir}/usr/i486-mingw32/lib/FreeImage.lib"
  install -Dm644 Dist/FreeImage.h   "${pkgdir}/usr/i486-mingw32/include/FreeImage.h"

  i486-mingw32-strip "${pkgdir}"/usr/i486-mingw32/bin/*.dll
}
