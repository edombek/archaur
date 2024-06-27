# Maintainer: Evgeniy Dombek <edombek@yandex.ru>
pkgname=casa6-bin
pkgver=6.6.4
ver_=34
pkgrel=1
pkgdesc="NRAO's Common Astronomy Software Applications package"
url="https://casa.nrao.edu/"
arch=('x86_64')
license=('GPL')
depends=('lsb-release' 'libselinux' 'libxcrypt-compat') 
conflict=("casa")
provides=("casa")
instname="casa-${pkgver}-${ver_}-py3.10.el8"
source=("https://casa.nrao.edu/download/distro/casa/release/rhel/${instname}.tar.xz")
md5sums=("a169b347ffc35d978a6d72b048af6c8a")
instdir="/opt"
options=("!strip")
package() {
  # Copy out files
  mkdir -p "${pkgdir}/${instdir}"
  cp -r  "${srcdir}/${instname}" "${pkgdir}/${instdir}"

  # Symlink executables
  mkdir -p "${pkgdir}/usr/bin/"
  for _executable in casa casaviewer mpicasa; do
    ln -s "${instdir}/${instname}/bin/${_executable}" "${pkgdir}/usr/bin/${_executable}"
  done
  echo "For use with Python, add to your bashrc:"
  echo alias casa-python=${instdir}/${instname}/bin/python3
  echo alias casa-pip=${instdir}/${instname}/bin/pip3
}
