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
        'git+https://github.com/Pylons/waitress.git'
        'git+https://github.com/ross/requests-futures.git'
        'git+https://github.com/slezica/python-frozendict.git'
sha1sums=('SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP')
install=install

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

  cd "$srcdir"
  cp -a argparse bottle python-frozendict jedi requests requests-futures waitress \
    "$pkgdir/usr/share/vim/vimfiles/third_party/"
}

# vim:set ts=2 sw=2 et:
