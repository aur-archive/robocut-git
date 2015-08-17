# Maintainer: Alex Ozer <spunko@yahoo.com>

pkgname=robocut-git
pkgver=20120810
pkgrel=1
pkgdesc="Utility to control Graphtec cutting plotters"
arch=('i686' 'x86_64')
url="https://gitorious.org/robocut"
license=('GPL3')
depends=('qt4' 'libusbx')
makedepends=('git')
install=robocut-git.install

_gitroot="git://gitorious.org/robocut/robocut.git"
_gitname="robocut"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  qmake-qt4
  make
}

package() {
  cd "$srcdir/$_gitname-build"
  mkdir -p $pkgdir/usr/bin/
  mv ./Robocut $pkgdir/usr/bin/
  ln -s $pkgdir/usr/bin/Robocut $pkgdir/usr/bin/robocut
}
