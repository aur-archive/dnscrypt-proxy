# Maintainer: Techlive Zheng <techlivezheng at gmail dot com>
# Contributor: peace4all <markspost at rocketmail dot com>

pkgname=dnscrypt-proxy
pkgver=1.3.1
pkgrel=1
pkgdesc="A tool for securing communications between a client and a DNS resolver"
arch=('i686' 'x86_64')
url="http://dnscrypt.org/"
license=('custom')
depends=(libsodium)
source=(http://download.dnscrypt.org/$pkgname/$pkgname-$pkgver.tar.bz2 
	conf.d.file 
	dnscrypt-proxy.service)
backup=(etc/conf.d/dnscrypt-proxy)
conflicts=(dnscrypt-proxy-git)

build() {
	cd $srcdir/$pkgname-$pkgver
	CFLAGS="$CFLAGS -fPIC" ./configure --prefix=/usr --sbindir=/usr/bin
	make -j2
}

package() {
	cd $srcdir/$pkgname-$pkgver
	make DESTDIR=$pkgdir install
	mkdir -p $pkgdir/{usr/share/{licenses,doc}/$pkgname,etc/conf.d,usr/lib/systemd/system}
	install -m 644 COPYING $pkgdir/usr/share/licenses/$pkgname
	install -m 644 AUTHORS NEWS README README.markdown $pkgdir/usr/share/doc/$pkgname
	install -m 644 $srcdir/conf.d.file $pkgdir/etc/conf.d/$pkgname
	install -m 644 $srcdir/dnscrypt-proxy.service $pkgdir/usr/lib/systemd/system
	rm -rf $pkgdir/usr/{lib/*.{l,}a,include}
}

md5sums=('dee03b8cbbc1e6a38c1bea0af474dee8'
         '4d486b3c2a4d47d4f998ed75c5033f77'
         '8ddf884ce05f706f913eab3c5b235f45')
