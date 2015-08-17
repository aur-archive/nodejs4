# $Id$
# Maintainer:  Bartłomiej Piotrowski <nospam@bpiotrowski.pl>
# Contributor: Thomas Dziedzic < gostrc at gmail >
# Contributor: James Campos <james.r.campos@gmail.com>
# Contributor: BlackEagle < ike DOT devolder AT gmail DOT com >
# Contributor: Dongsheng Cai <dongsheng at moodle dot com>
# Contributor: Masutu Subric <masutu.arch at googlemail dot com>
# Contributor: TIanyi Cui <tianyicui@gmail.com>

pkgname=nodejs4
pkgver=0.4.12
pkgrel=1
pkgdesc='Evented I/O for V8 javascript'
arch=('i686' 'x86_64')
url='http://nodejs.org/'
license=('MIT')
depends=('python2')
checkdepends=('curl') # curl used for check()
optdepends=('openssl: TLS support')
options=('!emptydirs')
source=("http://nodejs.org/dist/node-v${pkgver}.tar.gz")
md5sums=('a6375eaa43db5356bf443e25b828ae16')

build() {
  cd node-v${pkgver}

  msg 'fixing for python2 name'
  find -type f -exec sed -e 's_^#!/usr/bin/env python$_&2_' -e 's_^\(#!/usr/bin/python2\).[45]$_\1_' -e 's_^#!/usr/bin/python$_&2_' -e "s_'python'_'python2'_" -i {} \;
  find test -type f -exec sed -e "s|python |python2 |" -i {} \;
  sed -i "s|cmd_R = 'python |cmd_R = 'python2 |" wscript
  sed -i "s|python |python2 |" Makefile
  find test -type f -exec sed -e 's/python/&2/' -i {} \;
  sed -i "s/python/&2/" configure

  export PYTHON=python2

  ./configure \
    --prefix=/opt/nodejs4

  make
}

check() {
  cd node-v${pkgver}

  # test failures in 0.6 are known
  # specifically https://github.com/joyent/node/pull/1699
  make test || true
}

package() {
  cd node-v${pkgver}

  make DESTDIR=${pkgdir} install
}

# vim:set ts=2 sw=2 et:
