# Maintainer: Jason R. McNeil <jason@jasonrm.net>
# Based on atlassian-jira: https://aur.archlinux.org/packages/atlassian-jira/

pkgname=atlassian-stash
pkgver=3.10.0
pkgrel=1
pkgdesc="On-premise source code management for Git that's secure, fast, and enterprise grade."
url="https://www.atlassian.com/software/stash"
license=('custom')
arch=('any')
depends=('java-environment>=7', 'java-runtime-jre>=7')
optdepends=('mysql-connector: connect to MySQL'
            'libcups: used by bin/config.sh'
            'fontconfig: used by bin/config.sh')
backup=('etc/conf.d/stash')
install='stash.install'
source=("https://www.atlassian.com/software/stash/downloads/binary/atlassian-stash-${pkgver}.tar.gz"
        'stash.conf.d'
        'stash.service')
sha256sums=('ab7fecb10e6650fb5b94a20b22463771d7ab0f69a0971272d1a066dd2430f048'
            '5a6a87f08d78587d8202ecf15abcfdc0e6e77533566dd093c2b246b110bb971c'
            'ed3a0f928b956ab7427ffb7c44fcbb93522b168073e44670e7f62002fb7c9e7c')

package() {
  cd "${srcdir}"
  mkdir -p "${pkgdir}/opt/atlassian-stash/"
  cp -r "${srcdir}/atlassian-stash-$pkgver/"* "${pkgdir}/opt/atlassian-stash/"

  # remove unneeded *.bat files
  find "${pkgdir}/opt/atlassian-stash/bin" -name '*.bat' -type f -exec rm "{}" \;

  # Stash Home
  install -dm755 "${pkgdir}/var/lib/atlassian-stash"

  # Setup systemd service
  install -dm755 "${pkgdir}/usr/lib/systemd/system"
  install -Dm644 "${srcdir}/stash.service" "${pkgdir}/usr/lib/systemd/system"
  install -Dm644 "${srcdir}/stash.conf.d" "${pkgdir}/etc/conf.d/stash"
}
