# Maintainer: Evgeniy Dombek <edombek@yandex.ru>

pkgname=gildas
pkgver=2024.07.b
pkgver_=jul24b
pkgrel=1
pkgdesc='GILDAS'
arch=('x86_64')
url="https://www.iram.fr/IRAMFR/GILDAS/"
license=('custom')
makedepends=(python python-setuptools python-numpy which)
depends=(gcc-fortran cfitsio gtk2)
optdepends=(python-numpy)

source=("https://www.iram.fr/~gildas/dist/gildas-src-$pkgver_.tar.xz")
sha512sums=('5af9f871399293065531ce70e6f83da3840317ae2d6a2ea1c40d5264bda52520ebb4e98c12523f12b481a4056d11a02b13915c2b89f1972fc062962a6c6b239f')
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
