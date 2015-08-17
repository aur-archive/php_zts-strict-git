# Maintainer: Boris Momčilović <boris.momcilovic@gmail.com>

pkgname=php_zts-strict-git
pkgver=v0.4.0.r0.gc08a1e3
pkgrel=1
pkgdesc="Strict sclar parameter hints for PHP5 + PHP7"
arch=('i686' 'x86_64')
url="https://github.com/krakjoe/strict"
license=('PHP')
depends=('php_zts')
makedepends=('git')
source=("$pkgname"::'git://github.com/krakjoe/strict.git')
md5sums=('SKIP')
_ininame="strict.ini"
_inifile="etc/php-zts/conf.d/$_ininame"
backup=("$_inifile")

pkgver() {
  cd "$srcdir/$pkgname"
  ( set -o pipefail
    git describe --long | sed -r 's/([^-]*-g)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

build() {
  cd "$srcdir/$pkgname"

  /usr/bin/php-zts/phpize
  ./configure --with-php-config=/usr/bin/php-zts/php-config --prefix=/usr
  make
  #TEST_PHP_EXECUTABLE=`which php` php run-tests.php
}

package() {
  cd "$srcdir/$pkgname"
  make PREFIX=/usr INSTALL_ROOT="$pkgdir" install
  echo ";zend_extension=strict.so" > "$_ininame"
  install -vDm644 "$_ininame" "$pkgdir/$_inifile"
}
