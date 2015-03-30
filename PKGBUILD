pkgbase=ezgo
pkgname=('grub2-themes-ezgo' 'ezgo-wallpapers' 'ezgo-chem' 'ezgo-doc' 'ezgo-gsyan' 'ezgo-kde' 'ezgo-menu' 'ezgo-misc'
         'ezgo-npa' 'ezgo-phet' 'ezgo-usgs' 'ezgo-wordtest' 'ezgo-tasks')
pkgver=12.0
_ezgover=ezgo12
pkgrel=1
makedepends=()
arch=('x86_64')
_ezgosource="ftp://goodhorse.idv.tw/debian-ezgo"
source=("git://anonscm.debian.org/blends/projects/ezgo.git"
	'50_ezgo.cfg'
	# ezgo-chem elements
	"${_ezgosource}/ezgo-chem/chemstru_${_ezgover}.tar.gz"
	'chemical_struct.desktop'
	# ezgo-doc elements
	"${_ezgosource}/ezgo-doc/${_ezgover}_doc.tar.gz"
	'ezgo_doc.desktop'
	#ezgo-gsyan elements
	"ftp://goodhorse.idv.tw/debian-ezgo/ezgo-gsyan/gsyan_${_ezgover}.tar.gz"
	'gsyan.desktop')
sha1sums=('SKIP'
	  'be1ed0b3f1da77ce9393eea84413193e771ebac2'
	  # ezgo-chem elements
	  'bf477a9e0ed96b16ecb1c99b6ee5272916ed9ec7'
	  'c8c01ff2c8dcb8207fb58543e4711fa935389fb6'
	  # ezgo-doc elements
	  '795eb6326fdbe8b3b98d4cd50d37cd32931acfb1'
	  'c8acee50114fd03aad47dd1d6e5bcb5b34055843'
	  #ezgo-gsyan elements
	  ''
	  '')
# TODO: license all the packages

# FIXME: seperated into ezgo-wallpaper, kde-plasma-themes-ezgo, 
#        kde-ksplash-themes-ezgo, and grub2-themes-ezgo
  
package_ezgo-wallpapers() {
  pkgdesc='Set of wallpapers sepecified for Ezgo project'
  install=${pkgname}.install
  # KDE wallpaper
  # Install images
  cd ${srcdir}/${pkgbase}/${pkgname}/wallpaper
  for px in 1366x768 1920x1080 2560x1600; do
    install -Dm644 ezgo12-wallpaper-${px}.png ${pkgdir}/usr/share/wallpapers/ezgo/contents/images/${px}.png
  done
  # Install metadata
  install -Dm644 ezgo-wallpaper.png.desktop ${pkgdir}/usr/share/wallpapers/ezgo/metadata.desktop
}

package_grub2-themes-ezgo() {
  group=('ezgo-artwork')
  depends=('grub')
  # GRUB2 background
  cd ${srcdir}/${pkgbase}/${pkgname}/grub/
  install -Dm644 ${srcdir}/50_ezgo.cfg ${pkgdir}/etc/grub.d/50_ezgo.cfg
  install -Dm644 ezgo-splash-grub-640.png ${pkgdir}/usr/share/grub/themes/ezgo/ezgo-splash-grub-640.png
  install -Dm644 ezgo-splash-grub.png ${pkgdir}/usr/share/grub/themes/ezgo/ezgo-splash-grub.png
}
  # FIXME: KDM themes
  # TODO: SDDM themes
  # FIXME: Ksplash themes

package_ezgo-chem() {
  pkgdesc='Set of educational software of Chemistry for high school'
  depends=('xdg-utils')
  install -Dm644 ${srcdir}/chemical_struct.desktop ${pkgdir}/usr/share/applications/chemical_struct.desktop
  install -dm755 ${pkgdir}/usr/share/ezgo/ezgo-prt/chemical_structures
  cp -rv ${srcdir}/chemical_structures_ezgo12/* ${pkgdir}/usr/share/ezgo/ezgo-prt/chemical_structures/
}

package_ezgo-doc() {
  pkgdesc='Ezgo manual document'
  depends=('xdg-utils')
  install -Dm644 ${srcdir}/ezgo_doc.desktop
  install -dm755 ${pkgdir}/usr/share/ezgo/ezgo12/
  cp -rv ${srcdir}/ezgo12/* ${pkgdir}/usr/share/ezgo/ezgo12/
}

package_ezgo-gsyan() {
  pkgdesc='Flash tutorial accessories made by G. S. Yan'
  depends=('xdg-utils')
  optdepends=('pepperflashplugin: for chromium-based browsers
	      flashplugin: adobe flash plugin for web browsers')
  install -Dm644 ${srcdir}/gsyan.desktop ${pkgdir}/usr/share/applications/gsyan.desktop
  install -dm755 ${pkgdir}/usr/share/ezgo/ezgo-prt/gsyan
  cp -rv ${srcdir}/gsyan_ezgo12/* ${pkgdir}/usr/share/ezgo/ezgo-prt/gsyan/
}

package_ezgo-kde() {
}