# Maintainer: Dāvis Mosāns <davispuh at gmail dot com>

_pkgname=virtualgl
pkgname=$_pkgname-git
pkgver=2.4.r54.ga22ca6c
pkgrel=1
pkgdesc='Redirects 3D commands from an OpenGL application onto a server-side 3D graphics card'
arch=('i686' 'x86_64')
url='http://www.virtualgl.org/'
license=('LGPL')
depends=('libxv' 'glu' 'libjpeg-turbo' 'xcb-util-keysyms')
makedepends=('git')
provides=("$_pkgname")
conflicts=("$_pkgname")
source=("$_pkgname::git+https://github.com/VirtualGL/virtualgl.git")
sha256sums=('SKIP')

pkgver() {
    cd "$srcdir/$_pkgname"
    git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
    cd "$srcdir"
    mkdir -p build
}

build() {
    cd "$srcdir/build"

    cmake "$srcdir/$_pkgname" \
        -DCMAKE_INSTALL_PREFIX=/usr/share \
        -DTJPEG_INCLUDE_DIR=/usr/include \
        -DTJPEG_LIBRARY=/usr/lib/libturbojpeg.so \
        -DVGL_LIBDIR=/usr/lib \
        -DVGL_BINDIR=/usr/bin \
        -DVGL_DOCDIR=/usr/share/doc/${pkgname}

    make
}

package() {
    cd "$srcdir/build"

    make install DESTDIR="$pkgdir"

    mv "$pkgdir"/usr/bin/glxinfo "$pkgdir"/usr/bin/vglxinfo
}
