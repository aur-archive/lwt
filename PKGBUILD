pkgname=lwt
pkgver=20150425
pkgrel=1
pkgdesc="Lightweight terminal emulator based on the VTE and GTK libraries."
arch=('i686' 'x86_64')
url="https://github.com/mewkiz/lwt"
license=('public domain')
depends=('gtk3' 'vte3')
makedepends=('git')

_gitroot="git://github.com/mewkiz/lwt.git"
_gitname="lwt"

build() {
	cd "$srcdir"
	msg "Connecting to GIT server...."

	if [ -d $_gitname ] ; then
		cd $_gitname && git pull origin
		msg "The local files are updated."
	else
		git clone $_gitroot $_gitname
	fi

	msg "GIT checkout done or server timeout"
	msg "Starting make..."

	rm -rf "$srcdir/$_gitname-build"
	git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
	cd "$srcdir/$_gitname-build"

	#
	# BUILD HERE
	#

	msg "Starting make..."
	make || return 1
}

package() {
	cd "$srcdir/$_gitname-build"
	make DESTDIR="$pkgdir/usr" install || return 1
}
