# Maintainer: Gabriel Peixoto <gabrielrcp@gmail.com>
# Contributer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributer: judd <jvinet@zeroflux.org>

pkgname=lib32-tcp_wrappers-lib
pkgver=7.6
pkgrel=3
pkgdesc="Monitors and Controls incoming TCP connections - Libraries for 32 bits"
arch=('x86_64')
url="ftp://ftp.porcupine.org/pub/security/index.html"
license=('custom')
depends=('lib32-glibc')
makedepends=('gcc-multilib' 'gcc-libs-multilib')
source=(ftp://ftp.porcupine.org/pub/security/tcp_wrappers_${pkgver}.tar.gz
	http://archlinux-stuff.googlecode.com/files/tcp-wrappers-${pkgver}%2B.patch.gz)
md5sums=('e6fa25f71226d090f34de3f6b122fb5a'
         '3e786669e16b78ba726f948ddb73c9db')

build() {
  cd "$srcdir/tcp_wrappers_${pkgver}"

  patch -p1 <"$srcdir/tcp-wrappers-${pkgver}%2B.patch"

  # Install in /usr/lib32 instead of /usr/lib
  sed 's,/usr/lib/,/usr/lib32/,g' -i Makefile

  make CC='gcc -m32' REAL_DAEMON_DIR=/usr/sbin STYLE=-DPROCESS_OPTIONS linux
}

package(){
  cd "$srcdir/tcp_wrappers_${pkgver}"

  make DESTDIR="$pkgdir" install-lib
  install -D -m644 DISCLAIMER "$pkgdir/usr/share/licenses/$pkgname/license.txt"
}
