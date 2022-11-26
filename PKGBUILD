_pkgname=bspwm
pkgname=${_pkgname}-git
pkgver=99999.0.9.10
pkgrel=1
pkgdesc='Tiling window manager based on binary space partitioning'
arch=(x86_64)
url='https://github.com/baskerville/bspwm'
license=(BSD)
makedepends=(git)
depends=(xcb-util xcb-util-wm xcb-util-keysyms)
optdepends=('sxhkd: to define keyboard and pointer bindings'
            'xdo: for the example panel')
source=("$pkgname::git+https://github.com/amosbird/${_pkgname}.git")
md5sums=('SKIP')
provides=("${_pkgname}=${pkgver%%.r*}-${pkgrel}")
conflicts=("${_pkgname}")

build() {
  CFLAGS+=' -fcommon' # https://wiki.gentoo.org/wiki/Gcc_10_porting_notes/fno_common
  make -C "$pkgname" PREFIX=/usr
}

package() {
  cd "$pkgname"

  make PREFIX=/usr DESTDIR="$pkgdir" install

  # BSD 2-clause
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

pkgver() {
  cd $pkgname
  echo "99999."$(git describe --long --tags | sed -r 's,^[^0-9]*,,;s,([^-]*-g),r\1,;s,[-_],.,g')
}
