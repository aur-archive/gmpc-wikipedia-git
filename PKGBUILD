#Contributor: DarkJesus <priestoftime@gmail.com>

pkgname=gmpc-wikipedia-git
provides=gmpc-wikipedia
conflicts=('gmpc-wikipedia' 'gmpc-wikipedia-svn')
pkgver=20080409
pkgrel=1
pkgdesc="A plugin for gmpc that shows embedded information on the current artist from wikipedia"
url="http://sarine.nl/gmpc"
license="GPL"
arch=('i686' 'x86_64')
depends=('gmpc-git')
makedepends=('git' 'intltool' 'gob2' 'pkgconfig')
options=('!libtool')
source=()
md5sums=()

_gitroot="git://repo.or.cz/gmpc-wikipedia.git"
_gitname="gmpc-wikipedia"
build() {
	cd $startdir/src
	msg "Connecting to $_gitroot server..."

	if [ -d $startdir/src/$_gitname ] ; then
		cd $_gitname && git-pull origin
		msg "The local files are updated."
	else
		git clone $_gitroot
	fi

	msg "GIT checkout done or server timeout"
	msg "Starting make..."

	cp -r $startdir/src/$_gitname $startdir/src/$_gitname-build
	cd $startdir/src/$_gitname-build

	./autogen.sh --prefix=/usr
	make || return 1
	make DESTDIR=$startdir/pkg install

	find $startdir/pkg -type f -name "*.la" -exec rm {} \;
}
