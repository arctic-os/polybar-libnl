# Maintainer: Patrick Ziegler <p.ziegler96@gmail.com>
pkgname=polybar-wireless
pkgorg=polybar
pkgver=3.5.7
pkgrel=2
pkgdesc="A fast and easy-to-use status bar"
arch=("i686" "x86_64")
url="https://github.com/polybar/polybar"
license=("MIT")
depends=("cairo" "wireless_tools" "xcb-util-image" "xcb-util-wm" "xcb-util-xrm" "xcb-util-cursor"
         "alsa-lib" "libpulse" "libmpdclient" "libnl" "jsoncpp" "curl")
optdepends=("i3-wm: i3 module support"
            "ttf-unifont: Font used in example config"
            "siji-git: Font used in example config"
            "xorg-fonts-misc: Font used in example config")
makedepends=("cmake" "python" "pkg-config" "python-sphinx" "python-packaging" "i3-wm")
conflicts=("polybar-git" "polybar")
install="${pkgname}.install"
source=(${url}/releases/download/${pkgver}/${pkgorg}-${pkgver}.tar.gz)
sha256sums=('73210e6d74217acb953b253990b4302343b7b6a7870fe1da9a1855daa44123db')
_dir="${pkgorg}-${pkgver}"

prepare() {
  mkdir -p "${_dir}/build"
}

build() {
  cd "${_dir}/build" || exit 1
  # Force cmake to use system python (to detect xcbgen)
  cmake -DWITH_LIBNL=OFF -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release -DPYTHON_EXECUTABLE=/usr/bin/python3 ..
  cmake --build .
}

package() {
  cmake --build "${_dir}/build" --target install -- DESTDIR="${pkgdir}"
  install -Dm644 "${_dir}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgorg}/LICENSE"
}
