# Maintainer: Isaac C. Aronson <i@pingas.org>

pkgname=bro
pkgver=20130209
pkgrel=1
pkgdesc="A highly configurable IDS"
arch=('i686' 'x86_64' 'armv6h')
url="http://bro-ids.org/"
backup=(etc/bro/{broccoli.conf,broctl.cfg,networks.cfg,node.cfg})
license=('BSD')
depends=('libpcap' 'ruby' 'file' 'geoip' 'python2')
makedepends=('cmake' 'swig')
options=('emptydirs')
optdepends=('gperftools: Faster malloc() and useful diagnostic utilites (recompile after installing)')
_gitroot="git://git.bro-ids.org/bro.git"
_gitname="bro"

build() {
  cd $srcdir
  if [ -d "$srcdir/$_gitname" ] ; then 
      cd $_gitname && git pull origin && git submodule update --recursive --init
      msg "Local files are up-to-date"
  else
      git clone --recursive $_gitroot
      cd $_gitname
      git checkout && git pull
  fi

  msg "GIT checkout done or server timeout"
  cd "$srcdir/$_gitname"
  ./configure --prefix="/usr" --conf-files-dir="/etc/bro" --with-python=/usr/bin/python2
  make DESTDIR="$pkgdir"
}

package() {
  cd $srcdir/$_gitname
  make DESTDIR="$pkgdir/" install
}
