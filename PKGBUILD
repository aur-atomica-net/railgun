# Maintainer: Jason R. McNeil <jason@jasonrm.net>

pkgname=railgun
pkgver=latest
pkgrel=1
pkgdesc="Railgun is a WAN optimization technology developed by CloudFlare and is available to CloudFlare Business and Enterprise customers, as well as Optimized Partners."
arch=('x86_64')
url="https://www.cloudflare.com/docs/railgun/index.html"
license=('custom')
install=railgun.install
depends=()
makedepends=('rpmextract')
backup=('etc/railgun/railgun.conf' 'etc/railgun/railgun-nat.conf')
source=("https://www.cloudflare.com/static/misc/railgun/centos/railgun-el7.latest.rpm" "railgun.service")
noextract=('railgun-el7.latest.rpm')
sha512sums=('d30eb7ed7e150df3b5b47783722dc46b301c88a9e7ffd0c2e608add4ab5922261b0b39a70b516206367dada43e8f77bb6be03460ae664151bcf98c78d12cc2e3'
            '2b765bbeafde2aa6a12ae0cdb5b998c04b2860e48ebf950e3289a02539e966c39918717ff2d43c220db6a7a44523ff10e8b633a0f0651211e4e5a2bc8e6c9dc6')

package() {
  cd "${pkgdir}"

  rpmextract.sh "${srcdir}/railgun-el7.latest.rpm"

  # Remove RedHat specific files
  rm -r "${pkgdir}/etc/init.d"
  rm -r "${pkgdir}/etc/sysconfig"

  # Remove var directory
  rm -r "${pkgdir}/var"

  sed -i 's:/var/log:/var/lib:' "${pkgdir}/etc/railgun/railgun.conf"
  sed -i 's:/var/run:/var/lib:' "${pkgdir}/etc/railgun/railgun.conf"

  install -m755 -d "${pkgdir}/var/lib/railgun"

  install -m755 -d "${pkgdir}/usr/lib/systemd/system"
  install -m644  "${srcdir}/railgun.service" "${pkgdir}/usr/lib/systemd/system"
}
