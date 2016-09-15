# Maintainer: Jason R. McNeil <jason@jasonrm.net>

pkgname=railgun
pkgver=5.2.0
pkgrel=1
pkgdesc="Railgun is a WAN optimization technology developed by CloudFlare and is available to CloudFlare Business and Enterprise customers, as well as Optimized Partners."
arch=('x86_64')
url="https://www.cloudflare.com/docs/railgun/index.html"
license=('custom')
install=railgun.install
depends=()
makedepends=('rpmextract')
backup=('etc/railgun/railgun.conf' 'etc/railgun/railgun-nat.conf')
source=("railgun.rpm::http://pkg.cloudflare.com/pool/el7/railgun/r/railgun-stable-${pkgver}-${pkgrel}.el7.src.rpm/railgun-stable-${pkgver}-${pkgrel}.el7.x86_64.rpm" "railgun.service")
noextract=('railgun.rpm')
sha512sums=('57d9272ffd8831507fce60a16168f5bb8144c475eb3201c169321f2a54e77ee08778cbc933e4d6025d849c5c030e4a87ea57c4a8f12dc2f1f151420929cccd4e'
            '2b765bbeafde2aa6a12ae0cdb5b998c04b2860e48ebf950e3289a02539e966c39918717ff2d43c220db6a7a44523ff10e8b633a0f0651211e4e5a2bc8e6c9dc6')

package() {
  cd "${pkgdir}"

  rpmextract.sh "${srcdir}/railgun.rpm"

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
