# Contributor: Thomas Schneider <blacklotus@jenux.homelinux.org>

pkgname=com-on-air-tools
pkgver=102
pkgrel=1
pkgdesc="Com on air linux driver and userspace tools. Dect pcmcia card."
url="https://dedected.org/cgi-bin/trac.cgi/wiki/COM-ON-AIR-Linux"
arch=('i686' 'x86_64')
license=('GPL2')
depends=()
makedepends=('subversion' 'gcc')
conflicts=('com-on-air')
provides=()
source=()
md5sums=()
_svntrunk=https://dedected.org/svn/trunk/com-on-air_cs-linux
_svnmod=com-on-air_cs-linux
build() {
  cd ${srcdir}
  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi
  msg "SVN checkout done or server timeout"
  msg "Starting make..."
  cd $_svnmod
  make -C tools || return 1
# make node || return 1
  mkdir -p ${pkgdir}/usr/bin -m 755
  cd tools
  install coa_syncsniff -D ${pkgdir}/usr/bin -m 755
  install dect_cli -D ${pkgdir}/usr/bin -m 755
  install pcap2cchan -D ${pkgdir}/usr/bin -m 755
  install pcapstein -D ${pkgdir}/usr/bin -m 755
  cd dectshark 
  make || return 1
  install dectshark -D ${pkgdir}/usr/bin -m 755
}
