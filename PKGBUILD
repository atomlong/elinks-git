# Contributor: Kyle Keen <keenerd@gmail.com>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Andrea Scarpino <andrea@archlinux.org>
# Contributor: damir <damir@archlinux.org>
# Contributor: Ben <contrasutra@myrealbox.com>
# Maintainer: ferreum <code.danielk at gmail com>

_pkgname=elinks
pkgname=${_pkgname}-git
pkgver=v0.14.1.r0.g9e0c85e5
pkgrel=1
pkgdesc="An advanced and well-established feature-rich text mode web browser. Git version."
arch=("i686" "x86_64" "arm" "armv6h" "armv7h" "aarch64")
url="https://github.com/rkd77/elinks"
provides=(${_pkgname})
license=('GPL')
conflicts=(${_pkgname})
depends=('bzip2' 'expat>=2.0' 'gpm>=1.20.4' 'openssl' 'lua51' 'libidn' 'gc' 'tre' 'zlib')
source=("git+https://github.com/rkd77/elinks#branch=elinks-0.14")
md5sums=('SKIP')

pkgver() {
  cd "$srcdir/$_pkgname"
  git describe --tags --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd "${_pkgname}"

  # not needed when using autoreconf
  #[ -x configure ] || sh autogen.sh

  # autoreconf to allow compiling on arm (project's config is outdated (updated 2004)?)
  autoreconf -ifv

  ./configure --prefix=/usr --mandir=/usr/share/man \
              --sysconfdir=/etc \
              --with-zlib \
              --without-lzma \
              --without-bzlib \
              --without-x \
              --without-spidermonkey \
              --enable-cgi \
              --enable-leds \
              --disable-smb \
              --disable-sm-scripting \
              --enable-256-colors \
              --enable-html-highlight \
              --enable-exmode
  make
}

package() {
  cd "${_pkgname}"
  make DESTDIR="$pkgdir" install
  rm -f "$pkgdir/usr/share/locale/locale.alias"
}

# vim:set sw=2 sts=0 et:
