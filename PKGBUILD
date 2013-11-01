# Maintainer: Simon Gomizelj <simongmzlj@gmail.com>
# Contributor: Daniel Micay <danielmicay@gmail.com>

pkgname=vim-youcompleteme-git
pkgver=951.b288dce
pkgver() {
  cd "YouCompleteMe"
  echo $(git rev-list --count master).$(git rev-parse --short master)
}
pkgrel=1
pkgdesc='A code-completion engine for Vim'

arch=(i686 x86_64)
url='http://valloric.github.com/YouCompleteMe/'
license=('GPL3')
groups=('vim-plugins')
depends=('gvim' 'clang' 'python2')
makedepends=('git' 'cmake')
provides=('vim-youcompleteme')
conflicts=('vim-youcompleteme')
source=('git+https://github.com/Valloric/YouCompleteMe.git'
        'git+https://github.com/bewest/argparse.git'
        'git+https://github.com/davidhalter/jedi.git'
        'git+https://github.com/defnull/bottle.git'
        'git+https://github.com/kennethreitz/requests.git'
        'git+https://github.com/nosami/OmniSharpServer.git')
        'git+https://github.com/Pylons/waitress.git'
        'git+https://github.com/ross/requests-futures.git'
        'git+https://github.com/slezica/python-frozendict.git'
sha1sums=('SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP')
install=install

prepare() {
  cd "$srcdir/YouCompleteMe"
  for s in ${source[@]:1}
  do
    repo=${s##*/}
    repo=${repo/.git}
    echo "s=$s, repo=$repo"
    sed -i -e "/${repo}$/ s|https://github.com/.*|$srcdir/$repo|" .gitmodules
    sed -i -e "/${repo}.git$/ s|https://github.com/.*|$srcdir/$repo|" .gitmodules
  done
  git submodule update --init
}

build() {
  cd "YouCompleteMe/cpp"
  cmake -G "Unix Makefiles" -DUSE_SYSTEM_LIBCLANG=ON
  make ycm_core
  make ycm_support_libs
}

package() {
  mkdir -p "$pkgdir/usr/share/vim/vimfiles"

  cd "$srcdir/YouCompleteMe"
  cp -a autoload doc plugin python third_party "$pkgdir/usr/share/vim/vimfiles"
  ln -sf /usr/lib/llvm/libclang.so "$pkgdir/usr/share/vim/vimfiles/python/"
}

# vim:set ts=2 sw=2 et:
