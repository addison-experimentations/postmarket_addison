# Reference: <https://postmarketos.org/devicepkg>
pkgname=device-motorola-addison
pkgdesc="Motorola Moto Z Play"
pkgver=0.1
pkgrel=0
url="https://postmarketos.org"
license="MIT"
arch="aarch64"
options="!check !archcheck"
depends="
	linux-motorola-addison
	mkbootimg
	postmarketos-base
"
makedepends="devicepkg-dev"
source="
	deviceinfo
	modules-initfs
"

build() {
	devicepkg_build $startdir $pkgname
}

package() {
	devicepkg_package $startdir $pkgname
}

sha512sums="(run 'pmbootstrap checksum device-motorola-addison' to fill)"
