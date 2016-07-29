# Maintainer: Jason R. McNeil <jason@jasonrm.net>
# Based on atlassian-jira: https://aur.archlinux.org/packages/atlassian-jira/

pkgname=atlassian-bitbucket
pkgver=4.8.3
pkgrel=1
pkgdesc="On-premise source code management for Git that's secure, fast, and enterprise grade."
url="https://www.atlassian.com/software/bitbucket"
license=('custom')
arch=('any')
depends=('java-environment>=7')
optdepends=('mysql-connector: connect to MySQL'
            'libcups: used by bin/config.sh'
            'fontconfig: used by bin/config.sh')
backup=('etc/conf.d/bitbucket')
install='bitbucket.install'
replaces=('atlassian-stash')
source=("https://www.atlassian.com/software/stash/downloads/binary/atlassian-bitbucket-${pkgver}.tar.gz"
        'bitbucket.conf.d'
        'bitbucket.service')
sha256sums=('8f5544e8b9e6cb444df6ce401425ec308c380e317618c40d8895f6ebb2aa6328'
            '21f68198f0339463a9816bb46766df71f50cb388cf176c4af8519d4e1010b561'
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
