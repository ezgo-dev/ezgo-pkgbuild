pkgbase=ezgo
pkgname=('grub2-themes-ezgo' 'ezgo-wallpapers' 'kde-ksplash-themes-ezgo' 'kde-kdm-themes-ezgo' # Looks and feels of ezgo
         'ezgo-chem' 'ezgo-doc' 'ezgo-gsyan'    # Applications of ezgo
         'ezgo-menu' 'ezgo-misc' 'ezgo-npa' 'ezgo-phet' 'ezgo-usgs' 'ezgo-wordtest' 'ezgo-tasks') # Utilities of ezgo)
pkgver=12.0
_ezgover=ezgo12
pkgrel=1
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
	# ezgo-gsyan elements
	"${_ezgosource}/ezgo-gsyan/gsyan_${_ezgover}.tar.gz"
	'gsyan.desktop'
	# ezgo-misc
	"7z.desktop"
	# ezgo-npa elements
	"${_ezgosource}/ezgo-npa/npa_${_ezgover}.tar.gz"
	'npa.desktop'
	)
sha1sums=('SKIP'
	  'be1ed0b3f1da77ce9393eea84413193e771ebac2'
	  # ezgo-chem elements
	  'bf477a9e0ed96b16ecb1c99b6ee5272916ed9ec7'
	  'c8c01ff2c8dcb8207fb58543e4711fa935389fb6'
	  # ezgo-doc elements
	  '795eb6326fdbe8b3b98d4cd50d37cd32931acfb1'
	  'c8acee50114fd03aad47dd1d6e5bcb5b34055843'
	  # ezgo-gsyan elements
	  # ezgo-misc
	  # ezgo-npa elements
	  '02d31b9ae4502d55953362ea34c92589'
	  )
# TODO: licensing all the packages

prepare() {
  msg  'extract 7zip archive'
  cd ${srcdir}
  tar xf ${srcdir}/ezgo/misc/7zip.tar.gz
}
package_ezgo-wallpapers() {
  pkgdesc='Set of wallpapers sepecified for Ezgo project'
  install=${pkgname}.install
  # KDE wallpaper
  # Install images
  cd ${srcdir}/${pkgbase}/${pkgbase}-artwork/wallpaper
  for px in 1366x768 1920x1080 2560x1600; do
    install -Dm644 ${_ezgover}-wallpaper-${px}.png ${pkgdir}/usr/share/wallpapers/ezgo/contents/images/${px}.png
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
  # TODO: SDDM themes
package_kde-ksplash-themes-ezgo() {
  group=('ezgo-artwork' 'ezgo-kde')
  install -dm755 ${pkgdir}/usr/share/apps/ksplash/Themes/ezgo
  cp -rv ${srcdir}/${pkgbase}/ezgo-kde/ksplash-ezgo-theme/* ${pkgdir}/usr/share/apps/ksplash/Themes/ezgo/
  mv ${pkgdir}/usr/share/apps/ksplash/Themes/ezgo/ksplashrc ${pkgdir}/usr/share/apps/ksplash/Themes/ezgo/Theme.rc
}

package_kde-kdm-themes-ezgo() {
  group=('ezgo-artwork' 'ezgo-kde')
  depends=('kde-workspace')
  install=${pkgname}.install
  install -dm755 ${pkgdir}/usr/share/kde4/apps/kdm/themes/ezgo
  cp -rv ${srcdir}/${pkgbase}/ezgo-kde/kdm-theme/ezgo/* ${pkgdir}/usr/share/kde4/apps/kdm/themes/ezgo/
  rm -v ${pkgdir}/usr/share/kde4/apps/kdm/themes/ezgo/30_ezgo
}

package_ezgo-chem() {
  pkgdesc='Set of educational software of Chemistry for high school'
  depends=('xdg-utils')
  install -Dm644 ${srcdir}/chemical_struct.desktop ${pkgdir}/usr/share/applications/chemical_struct.desktop
  install -dm755 ${pkgdir}/usr/share/ezgo/ezgo-prt/chemical_structures
  cp -rv ${srcdir}/chemical_structures_${_ezgover}/* ${pkgdir}/usr/share/ezgo/ezgo-prt/chemical_structures/
}

package_ezgo-doc() {
  pkgdesc='Ezgo manual document'
  depends=('xdg-utils')
  install -Dm644 ${srcdir}/ezgo_doc.desktop ${pkgdir}/usr/share/applications/ezgo_doc.desktop
  install -dm755 ${pkgdir}/usr/share/ezgo/${_ezgover}/
  cp -rv ${srcdir}/${_ezgover}/* ${pkgdir}/usr/share/ezgo/${_ezgover}/
}

package_ezgo-gsyan() {
  pkgdesc='Flash tutorial accessories made by G. S. Yan'
  depends=('xdg-utils')
  optdepends=('pepperflashplugin: for chromium-based browsers
	      flashplugin: adobe flash plugin for web browsers')
  install -Dm644 ${srcdir}/gsyan.desktop ${pkgdir}/usr/share/applications/gsyan.desktop
  install -dm755 ${pkgdir}/usr/share/ezgo/ezgo-prt/gsyan
  cp -rv ${srcdir}/gsyan_${_ezgover}/* ${pkgdir}/usr/share/ezgo/ezgo-prt/gsyan/
}

package_ezgo-misc() {
  # TODO: This is a big package bundled with several utilities that aren't belonging to the repo.
  #       Maybe, we should make this a meta package?
  pkgdesc=('Misc utilities for ezgo project - meta package')
  depends=('flashplugin' 'openjdk' 'chromium' 'skype' 'wine')
  optdepends=('pepperflashplugin: for using ppapi version of flash player under chromium')
  
  msg 'Installing media pack'
  echo 'We may not need all these utilities'
  # TODO: we've included most of the free codecs in Chakra
  msg 'install ktuberling sound theme'
  install -dm755 ${srcdir}/${pkgname}/ktuberling/zh_TW/ ${pkgdir}/usr/share/apps/ktuberling/sounds/zh_TW/
  install -Dm644 ${srcdir}/${pkgname}/ktuberling/zh_TW.soundtheme ${pkgdir}/usr/share/apps/ktuberling/sounds/zh_TW.soundtheme
  
  msg 'Installing 7zipFM.exe (requires wine)'
  install -dm755 ${srcdir}/7zip ${pkgdir}/opt/7zip
  install -Dm644 ${srcdir}/7z.desktop ${pkgdir}/usr/share/applications/7z.desktop
  
  msg 'Install MIME type values'
  install -Dm644 ${srcdir}/${pkgname}/mimeapps.list ${pkgdir}/usr/share/applications/mimeapps.list
}

package_ezgo-npa() {
  pkgdesc=('NPA package')
  depends=('flashplugin')
  optdepends=('pepperflashplugin: for using ppapi version of flash player under chromium')
  install -dm755 ${pkgdir}/usr/share/ezgo/ezgo-prt/npa
  cp -rv ${srcdir}/npa_${_ezgover}/* ${pkgdir}/usr/share/ezgo/ezgo-prt/npa/
  install -Dm644 ${srcdir}/${pkgbase}/${pkgname}/npa.desktop ${pkgdir}/usr/share/applications/npa.desktop
}