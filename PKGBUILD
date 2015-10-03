# Maintainer: Jason R. McNeil <jason@jasonrm.net>
# Based on atlassian-jira: https://aur.archlinux.org/packages/atlassian-jira/

pkgname=atlassian-bitbucket
pkgver=4.0.1
pkgrel=1
pkgdesc="On-premise source code management for Git that's secure, fast, and enterprise grade."
url="https://www.atlassian.com/software/bitbucket"
license=('custom')
arch=('any')
depends=('java-environment>=7', 'java-runtime-jre>=7')
optdepends=('mysql-connector: connect to MySQL'
            'libcups: used by bin/config.sh'
            'fontconfig: used by bin/config.sh')
backup=('etc/conf.d/atlassian-bitbucket')
install='atlassian-bitbucket.install'
replaces=('atlassian-stash')
source=("https://www.atlassian.com/software/stash/downloads/binary/atlassian-bitbucket-${pkgver}.tar.gz"
        'atlassian-bitbucket.conf.d'
        'atlassian-bitbucket.service')
sha256sums=('f59462077fa4ccc522b7bbf1ad6ebef4753cd0e41abf54bc0491d07eea40593d'
            'ce1d7520e3e49e9c4f1e03ed3836339d47f8c7dc3e2734450cded6abf1a99fc0'
            '4f3cb183c1cd8749dc700458909d05f4ef872f72a2eefe0709a33ba983605c94')

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
  install -Dm644 "${srcdir}/atlassian-bitbucket.service" "${pkgdir}/usr/lib/systemd/system"
  install -Dm644 "${srcdir}/atlassian-bitbucket.conf.d" "${pkgdir}/etc/conf.d/atlassian-bitbucket"
}
