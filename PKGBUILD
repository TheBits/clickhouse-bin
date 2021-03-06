# Maintainer: Sergey Mezentsev <thebits@yandex.ru>
pkgname=('clickhouse-client' 'clickhouse-common-static' 'clickhouse-server')
pkgver=20.3.8.53
pkgrel=1
provides=('clickhouse')
pkgdesc="ClickHouse is a fast open-source OLAP database management system"
arch=('x86_64')
url="https://clickhouse.tech/"
license=('Apache')
source=(
	"https://repo.yandex.ru/clickhouse/tgz/stable/clickhouse-client-$pkgver.tgz"
	"https://repo.yandex.ru/clickhouse/tgz/stable/clickhouse-common-static-$pkgver.tgz"
	"https://repo.yandex.ru/clickhouse/tgz/stable/clickhouse-server-$pkgver.tgz"
	"clickhouse.sysusers"
	"clickhouse-server.service"
)
sha512sums=(
	# client
	'80637af63fabb626782d5fce53b780e48029cc666c044c91860da271d62cb35300583dbd389061a3ac173be6a5c601667941137a1e5c99549faf21d7065603e1'
	# common
	'ee4b09de39cc25dbf1692cb13f456cb258ed0eafe014a5da87ba5e847392719ba141ab1fd5447eed7fafbdb49c985bec4a4bc6ed7dec89c137bd01ac3761925f'
	# server
	'0f0d6f950cfa87beda90b643b6477992a73b88a8c88ef80480257da8a007436e449d46e07e81145b0c8fbbf7e6229d5e9e255d376c44f65bf29e8a6c722cf3af'
	# sysusers
	'70af4456ded1a1bb5cf29d2d3b29086aedc7875ef673e8817f389243f0c79eb491c9ce715b94542cbe16eb7489d97411ff0ab4a1a7f6c9b9120c659b87ea25b7'
	# service
	'f70fb1fc8d26e1d6c8b4f5c808b373d464cd20ace363cfd735703d1af0f6ec6196a0c7c905d804fad789eb51acab4896397e70b64a0b61cdcd7457a6694fc4b3'
)


package_clickhouse-client() {
	depends=('clickhouse-common-static')
	backup=('etc/clickhouse-client/config.xml')
	pkgdesc="ClickHouse client and other client-related tools."

  	cd "$pkgname-$pkgver"
  	cp -r etc usr $pkgdir
}

package_clickhouse-common-static() {
	# options and directives overrides
	pkgdesc="ClickHouse compiled binary files."
	backup=('etc/security/limits.d/clickhouse.conf')

  	cd "$pkgname-$pkgver"
  	cp -r etc usr $pkgdir
}

package_clickhouse-server() {
	# options and directives overrides
	pkgdesc="ClickHouse server and default configuration."
	depends=('clickhouse-common-static')
	backup=(
		'etc/clickhouse-server/config.xml'
		'etc/clickhouse-server/users.xml'
	)

  	cd "$pkgname-$pkgver"
	cp -r usr "$pkgdir/"
	cp -r lib "$pkgdir/usr"
	mkdir -p "$pkgdir/etc/clickhouse-server"
	cp -r etc/clickhouse-server "$pkgdir/etc"
	install -D "$srcdir/clickhouse.sysusers" "${pkgdir}/usr/lib/sysusers.d/clickhouse.conf"
	install -D "$srcdir/clickhouse-server.service" "${pkgdir}/usr/lib/systemd/system/clickhouse-server.service"
}
