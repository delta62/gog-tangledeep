# Maintainer: Sam Noedel <sam.noedel@gmail.com>

pkgname=gog-tangledeep
pkgver=1.15.21663
pkgrel=1
pkgdesc="16-bit Roguelike Dungeon Crawler!"
url="http://tangledeep.com/"
license=('custom')
arch=('i686' 'x86_64')
depends=()
source=("gog://${pkgname//-/_}_${pkgver}.sh"
        "${pkgname}.desktop")
sha256sums=('20f03318bff7363a83f861261ea7b0675e6e6a0a380de33c527bb4d03ff936d8'
            '76d360091cded2763f07075f0fbf53de460208885ae0bf2ab584597ff2d97f2f')

# You need to download the gog.com installer file manually or with lgogdownloader.
DLAGENTS+=("gog::/usr/bin/echo %u - This is is not a real URL, you need to download the GOG file manually to \"$PWD\" or setup a gog:// DLAGENT. Read this PKGBUILD for more information.")

prepare() {
  unzip "${pkgname//-/_}_${pkgver}.sh" || :
  cd "${srcdir}/data/noarch"

  sed -r -i \
  's/(CURRENT_DIR="\$\( cd "\$\( dirname )'`
    `'"\$\{BASH_SOURCE\[0\]\}"(.*$)'`
    `'/\1$( readlink -nf "${BASH_SOURCE[0]}" )\2/' \
  "start.sh"
}

package() {
  cd "${srcdir}/data/noarch"
  # Install game
  install -d "${pkgdir}/opt/${pkgname}/"
  install -d "${pkgdir}/opt/${pkgname}/support"
  install -d "${pkgdir}/usr/bin/"
  cp -r "game/" "${pkgdir}/opt/${pkgname}"
  install -Dm755 "start.sh" "${pkgdir}/opt/${pkgname}/"
  install -Dm755 support/*.{sh,shlib} -t \
    "${pkgdir}/opt/${pkgname}/support"

  # Desktop integration
  install -Dm 644 "support/icon.png" \
    "${pkgdir}/usr/share/pixmaps/${pkgname}.png"
  install -Dm644 "docs/End User License Agreement.txt" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -Dm 644 "${srcdir}/${pkgname}.desktop" \
    "${pkgdir}/usr/share/applications/${pkgname}.desktop"
  ln -s "/opt/${pkgname}/start.sh" "${pkgdir}/usr/bin/${pkgname}"
}
