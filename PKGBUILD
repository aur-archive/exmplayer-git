# Maintainer: rtfreedman  <rob<d0t>til<d0t>freedman< T>googlemail<d0t>com>
#
pkgname=exmplayer-git
pkgver=50.91ecf82
pkgrel=2
url='http://exmplayer.sourceforge.net/'
pkgdesc='MPlayer GUI with thumbnail seeking, 3D Video support, ... (git version)'
license=('GPL')
#
arch=('i686' 'x86_64')
depends=('mplayer')
makedepends=('git')
#
provides=('exmplayer')
conflicts=('exmplayer')
#
install="${pkgname}.install"

source=("exmplayer-git::git+https://github.com/rupeshs/ExMplayer.git"
		'qtlocalpeer.patch')
		
md5sums=('SKIP'
         '4c19c035d06183681aa785e6a3bf56a4')

pkgver() {
  cd "${pkgname}"
  echo $(git rev-list --count master).$(git rev-parse --short master)
}

prepare() {
	cd "${pkgname}"
	patch -p0 -i "$srcdir/qtlocalpeer.patch"
#	sed -i 's/QMAKE=qmake/QMAKE=qmake-qt4/' Makefile
}

build() {
  cd "${pkgname}/src"
  qmake-qt4
  make 
}

package() {
  cd "${pkgname}"
  install -Dm755 src/exmplayer "$pkgdir"/usr/bin/exmplayer
  #
  install -dm755 "$pkgdir"/usr/share/applications
  install -m644 exmplayer.desktop exmplayer_enqueue.desktop "$pkgdir"/usr/share/applications
  install -Dm644 debian/exmplayer.png "$pkgdir"/usr/share/pixmaps/exmplayer.png
  #
  install -dm755 "$pkgdir"/etc/exmplayer
  install -m644 linux_build/{sc_default.xml,fmts} "$pkgdir"/etc/exmplayer
  #
  install -dm755 "$pkgdir"/usr/share/exmplayer
  # use native installed ffmpeg 
  ln -s /usr/bin/ffmpeg  "$pkgdir"/usr/share/exmplayer/ffmpeg
  # or bundled ffmpeg
  #install -m755 linux_build/ffmpeg "$pkgdir"/usr/share/exmplayer
}
