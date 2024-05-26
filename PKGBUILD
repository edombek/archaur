# Maintainer: Evgeniy Dombek <edombek@yandex.ru>
# Maintainer: Dan McCurry <dan.mc at protonmail dot com>
# Maintainer: Ethan Best <ethan at totalsecond dot com>
# with special thanks to deadlte for version 3.07.1

pkgname=libsdrplay
pkgver=3.15.1
pkgrel=1
pkgdesc="Modules for the SDRplay receiver"
arch=('aarch64' 'x86_64')
url="http://www.sdrplay.com"
license=('custom:EULA')
depends=('libusb>=1.0')
source=("http://www.sdrplay.com/software/SDRplay_RSP_API-Linux-${pkgver}.run"
		"sdrplay.service"
		"66-sdrplay.rules")
sha256sums=('093732bf5d17cfd1b62ea1e1e2a396f6d28111c07eaf3b44d91ef12485384014'
			'69935539fad9b7cf2cd1feb4017974cfaf164c37dfd01adfb0086ea7512e6ce7'
			'60ab1774bdf810d2019178486f1ef40960fb04f0d84f976e4bf1990ea8427d65')

prepare() {
	cd ${srcdir}

	msg2 "Extracting makeself archive..."
	sh SDRplay_RSP_API-Linux-${pkgver}.run --tar xf
}

package() {
	cd "${srcdir}"
	
	msg2 "Getting API version..."
	_apivers=$(sed -n 's/^VERS="\(.*\)"/\1/p' install_lib.sh)
	msg2 "API version: ${_apivers}"

	# These commands are equivalent to the scripts used in the supplied
	# run file
	install -D -m644 sdrplay_license.txt "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
	install -D -m644 "${CARCH}/libsdrplay_api.so.${_apivers}" 		"${pkgdir}/usr/lib/libsdrplay_api.so.${_apivers}"
	install -D -m755 "${CARCH}/sdrplay_apiService" "${pkgdir}/usr/bin/sdrplay_apiService"
	install -D -m644 "sdrplay.service" "${pkgdir}/etc/systemd/system/sdrplay.service"

	(cd inc && find . -type f -exec install -D -m644 "{}" "${pkgdir}/usr/include/{}" \;)
		
	install -D -m644 66-sdrplay.rules "${pkgdir}/etc/udev/rules.d/66-sdrplay.rules"

	cd "${pkgdir}/usr/lib"
	ln -s libsdrplay_api.so.${_apivers} libsdrplay_api.so.2
	ln -s libsdrplay_api.so.${_apivers} libsdrplay_api.so
	
}
