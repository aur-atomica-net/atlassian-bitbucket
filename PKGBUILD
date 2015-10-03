# Maintainer: Jason R. McNeil <jason@jasonrm.net>
# Based on atlassian-jira: https://aur.archlinux.org/packages/atlassian-jira/

pkgname=atlassian-bitbucket
pkgver=4.0.1
pkgrel=2
pkgdesc="On-premise source code management for Git that's secure, fast, and enterprise grade."
url="https://www.atlassian.com/software/bitbucket"
license=('custom')
arch=('any')
depends=('java-environment>=7', 'java-runtime-jre>=7')
optdepends=('mysql-connector: connect to MySQL'
            'libcups: used by bin/config.sh'
            'fontconfig: used by bin/config.sh')
backup=('etc/conf.d/bitbucket')
install='bitbucket.install'
replaces=('atlassian-stash')
source=("https://www.atlassian.com/software/stash/downloads/binary/atlassian-bitbucket-${pkgver}.tar.gz"
        'bitbucket.conf.d'
        'bitbucket.service')
sha256sums=('f59462077fa4ccc522b7bbf1ad6ebef4753cd0e41abf54bc0491d07eea40593d'
            'ce1d7520e3e49e9c4f1e03ed3836339d47f8c7dc3e2734450cded6abf1a99fc0'
            '5f0a6db521caf9af4026dadd25c0927aa05dbd83c090b3940940d97ab6422714')

package() {
  cd "${srcdir}"
  mkdir -p "${pkgdir}/opt/atlassian-bitbucket/"
  cp -r "${srcdir}/atlassian-bitbucket-$pkgver/"* "${pkgdir}/opt/atlassian-bitbucket/"

  # remove unneeded *.bat files
  find "${pkgdir}/opt/atlassian-bitbucket/bin" -name '*.bat' -type f -exec rm "{}" \;

  # Bitbucket Home
  install -dm755 "${pkgdir}/var/lib/atlassian-bitbucket"

  # Setup systemd service and configuration
  install -dm755 "${pkgdir}/usr/lib/systemd/system"
  install -Dm644 "${srcdir}/bitbucket.service" "${pkgdir}/usr/lib/systemd/system"
  install -Dm644 "${srcdir}/bitbucket.conf.d" "${pkgdir}/etc/conf.d/bitbucket"
}
