# Maintainer: Evgeniy Dombek <edombek@yandex.ru>

pkgname=gildas
pkgver=2024.05.a
pkgver_=may24a
pkgrel=1
pkgdesc='GILDAS'
arch=('x86_64')
url="https://www.iram.fr/IRAMFR/GILDAS/"
license=('custom')
makedepends=(python python-setuptools python-numpy which)
depends=(gcc-fortran cfitsio gtk2)
optdepends=(python-numpy)

source=("https://www.iram.fr/~gildas/dist/gildas-src-$pkgver_.tar.xz")
sha512sums=('313d35c9ecb72b17f645fb782cf41a4872172ded6c57bf52d2e08d5afdb02438c9e2f3107047a26f571f2c13f3e89b28190d985b8861b9f26710c6e4aa995e18')
options=('!strip')

build() {
    cd ${srcdir}/gildas-src-$pkgver_
    source admin/gildas-env.sh
    make
}

package() {
    cd ${srcdir}/gildas-src-$pkgver_
    source admin/gildas-env.sh
    make install
    
    target="opt/gildas-exe-$pkgver_"
    cd "$pkgdir"
    mkdir opt
    cp -r ${srcdir}/gildas-exe-$pkgver_ $target
    
    #Ading /etc/profile
    mkdir -p etc/profile.d
    echo export GAG_ROOT_DIR=/opt/gildas-exe-$pkgver_ >> etc/profile.d/gildas.sh
    echo export GAG_EXEC_SYSTEM=$GAG_EXEC_SYSTEM >> etc/profile.d/gildas.sh
    echo source /opt/gildas-exe-$pkgver_/etc/bash_profile >> etc/profile.d/gildas.sh
    chmod +x etc/profile.d/gildas.sh
}
