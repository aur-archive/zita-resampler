# Maintainer : speps <speps at aur dot archlinux dot org>
# Contributor: Philipp Überbacher <murks at lavabit dot com>

pkgname=zita-resampler
pkgver=1.3.0
pkgrel=1
pkgdesc="A C++ library for resampling audio signals."
url="http://kokkinizita.linuxaudio.org/linuxaudio/"
arch=('i686' 'x86_64')
license=('GPL3')
depends=('libsndfile')
source=("${url}downloads/$pkgname-$pkgver.tar.bz2")
md5sums=('74c12e2280008f63ac9f2670fe4cf79b')

build() {
  cd "$srcdir/$pkgname-$pkgver/libs"

  # lib
  make PREFIX=/usr

  # create lib link for building apps
  ln -s lib$pkgname.so.$pkgver lib$pkgname.so

  # apps
  cd ../apps
  CXXFLAGS+=" -I../libs" \
  LDFLAGS+=" -L../libs" \
  make PREFIX=/usr
}

package() {
  cd "$srcdir/$pkgname-$pkgver/libs"

  # lib
  install -Dm755 lib$pkgname.so.$pkgver \
    "$pkgdir/usr/lib/lib$pkgname.so.$pkgver"

  # links
  ln -s lib$pkgname.so.$pkgver \
    "$pkgdir/usr/lib/lib$pkgname.so"

  # headers
  install -d "$pkgdir/usr/include/$pkgname"
  install -Dm644 $pkgname/*.h \
    "$pkgdir/usr/include/$pkgname"

  # apps
  install -d "$pkgdir/usr/bin"
  install -Dm755 ../apps/zre{sample,tune} \
    "$pkgdir/usr/bin"

  # docs
  install -d "$pkgdir/usr/share/doc/$pkgname"
  install -Dm644 ../docs/* \
    "$pkgdir/usr/share/doc/$pkgname"

  # man
  install -d "$pkgdir/usr/share/man/man1"
  install -Dm644 ../apps/zre{sample,tune}.1 \
    "$pkgdir/usr/share/man/man1"
}
