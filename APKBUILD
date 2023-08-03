# Reference: <https://postmarketos.org/vendorkernel>
# Kernel config based on: arch/arm64/configs/(CHANGEME!)

pkgname=linux-motorola-addison
pkgver=3.18.140
pkgrel=0
pkgdesc="Motorola Moto Z Play kernel fork"
arch="aarch64"
_carch="arm64"
_flavor="motorola-addison"
url="https://kernel.org"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native"
makedepends="
	bash
	bc
	bison
	devicepkg-dev
	findutils
	flex
	openssl-dev
	perl
	dtbtool
"

# Source
_repository="android_kernel_motorola_msm8953"
_commit="4039a83a7c2d0b145dbb14044867a60382d15744"
_config="config-$_flavor.$arch"
source="
	$pkgname-$_commit.tar.gz::https://github.com/sounddrill31/$_repository/archive/$_commit.tar.gz
	$_config
	
"
builddir="$srcdir/$_repository-$_commit"
_outdir="out"

prepare() {
	default_prepare
	. downstreamkernel_prepare
}

build() {
	unset LDFLAGS
	make O="$_outdir" ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION="$((pkgrel + 1 ))-postmarketOS"
}

package() {
	downstreamkernel_package "$builddir" "$pkgdir" "$_carch" \
		"$_flavor" "$_outdir"

	# Master DTB (deviceinfo_bootimg_qcdt)
	dtbTool -p scripts/dtc/ -o "$_outdir/arch/$_carch/boot"/dt.img "$_outdir/arch/$_carch/boot/"
	install -Dm644 "$_outdir/arch/$_carch/boot"/dt.img "$pkgdir"/boot/dt.img

}

sha512sums="
5524feefd1cc08a1fbd1c5a72043c243bb4b7a5835b5d7b63ab66379e77ad3b895cc8acf5a7020807341322ae5058b26fa46080b03ccb2f7c763dc6020daae46  linux-motorola-addison-4039a83a7c2d0b145dbb14044867a60382d15744.tar.gz
2d4e26d92a8d8f444f1110af3f2bb46c1f063167cad8a961de06d676a6903dee14bf55adcecd71826370813f3fdda5be3e1aa5a651183272acfe66b8d1bf04b1  config-motorola-addison.aarch64
"
