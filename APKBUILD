# Contributor: Paul Merrill <pdm@pdm.me>
# Maintainer:
pkgname=amazon-efs-utils
pkgver=1.29.1
pkgrel=0
pkgdesc="Utilities for Amazon Elastic File System (EFS)"
url="https://github.com/aws/efs-utils"
arch="noarch"
license="MIT"
options="!check"  # some tests are failing
depends="nfs-utils openssl python3 stunnel util-linux"
makedepends="py3-pip"
subpackages="$pkgname-doc"
source="$pkgname-$pkgver.tar.gz::https://github.com/aws/efs-utils/archive/v$pkgver.tar.gz
	0001-Skip-libwrap-for-Alpine-Linux.patch
	amazon-efs-mount-watchdog.initd
	"
builddir="$srcdir/efs-utils-$pkgver"

check() {
	pip3 install -r requirements.txt
	PATH=$HOME/.local/bin:$PATH
	make test
}

package() {
	install -Dpm644 dist/efs-utils.conf \
		"$pkgdir"/etc/amazon/efs/efs-utils.conf
	install -Dpm444 dist/efs-utils.crt \
		"$pkgdir"/etc/amazon/efs/efs-utils.crt
	install -Dpm755 src/mount_efs/__init__.py "$pkgdir"/sbin/mount.efs
	install -Dpm755 src/watchdog/__init__.py \
		"$pkgdir"/usr/bin/amazon-efs-mount-watchdog
	install -Dm755 "$srcdir"/amazon-efs-mount-watchdog.initd \
		"$pkgdir"/etc/init.d/amazon-efs-mount-watchdog
	install -Dm644 man/mount.efs.8 "$pkgdir"/usr/share/man/man8/mount.efs.8
	install -dm644 "$pkgdir"/var/log/amazon/efs
}

sha512sums="36ed20de236d5ce64eb97f0649daebe9ac362ebd864776d63f4627e6d59ffc546ef04f38d0ce84ae32720181a860ddb45f01333b34cf198738884035e01e4dab  amazon-efs-utils-1.29.1.tar.gz
0cb987bf83701af2454c18b512175bfc5566fe7d977443852b7c1f1099b66e700da0fabb4a0fe26d578ac9860e591b6f17589fc23add9c9d227a68889f9ea8e3  0001-Skip-libwrap-for-Alpine-Linux.patch
dd8049a51baca5d06bd7c730ed3560b8a65342995a9ea35d2c567adfdf472610d79d8cd62736f17958d5dd51ca5914ba369316edb352c1b853ac3313dacf8e5d  amazon-efs-mount-watchdog.initd"
