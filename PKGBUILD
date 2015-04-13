# $Id$
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Jens Pranaitis <jens@jenux.homelinux.org>

pkgname=busybox
pkgver=1.23.2
pkgrel=1
pkgdesc="Utilities for rescue and embedded systems"
arch=("i686" "x86_64")
url="http://www.busybox.net"
license=('GPL')
makedepends=("make" "gcc" "sed" "ncurses" "musl" "kernel-headers-musl")
provides=('coreutils' 'grep' 'sed' 'findutils' 'diffutils' 'awk' 'util-linux' 'util-linux-ng' 'sysvinit' 'sysvinit-tools' 'which' 'tar' 'wget' 'psmisc' 'procps-ng' 'less' 'kmod')
install=busybox.install
source=("$url/downloads/$pkgname-$pkgver.tar.bz2"
	"config"
	ifplugd.patch)

md5sums=('7925683d7dd105aabe9b6b618d48cc73'
         '6eac4452039fdf4275a401ea501ac2fa'
         '187adc8319e45be12d79e8db2c514d74')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  patch -p1 <$srcdir/ifplugd.patch
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  cp $srcdir/config .config
  sed '1,1i#include <sys/resource.h>' -i include/libbb.h
  # if you want to run menuconfig uncomment the following line:
  # make menuconfig ; return 1
  make CC=musl-gcc
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make CONFIG_PREFIX="${pkgdir}" install
}
