pkgbase=ezgo
pkgname=('grub2-themes-ezgo' 'ezgo-wallpapers' # Looks and feels of ezgo
         'ezgo-chem' 'ezgo-doc' 'ezgo-gsyan'    # Applications of ezgo
         'ezgo-menu' 'ezgo-misc' 'ezgo-npa' 'ezgo-phet' 'ezgo-usgs' 'ezgo-wordtest' 'ezgo-tasks') # Utilities of ezgo)
pkgver=12.0
_ezgover=ezgo12
pkgrel=1
arch=('x86_64')
_ezgosource="ftp://goodhorse.idv.tw/debian-ezgo"
_phetver=PhET2015
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
	# ezgo-phet elements
	"${_ezgosource}/ezgo-phet/${_phetver}.tar.gz"
	'phet.desktop'
	# ezgo-usgs elements
	'USGS.png'
	'usgs.desktop'
	# ezgo-wordtest elements
	'ezgo-wordtest.tar.gz'
	'ezgo-wordtest.desktop'
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
	  '85b3771e2ce2a177b445137a185cf0a04122aca9'
          '6263a94dc8c07101d9db589c127fe6dc03e168d6'
	  # ezgo-misc
	  # ezgo-npa elements
	  '3d09ac6ebad61ce0f8dd59c183f44bcef92e7e2b'
          'ac61f263705bc3f7d2f080505d7684768eb06c4d'
          # ezgo-phet
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

package_ezgo-phet() {
  pkgdesc=('PhET package')
  depends=('flashplugin')
  optdepends=('pepperflashplugin: for using ppapi version of flash player under chromium')
  install -dm755 ${pkgdir}/usr/share/ezgo/ezgo-prt/PhET
  cp -rv ${srcdir}/${_phetver}/* ${pkgdir}/usr/share/ezgo/ezgo-prt/PhET/
  install -Dm644 ${srcdir}/${pkgbase}/${pkgname}/phet.desktop ${pkgdir}/usr/share/applications/phet.desktop
}

package_ezgo-usgs() {
  pkgdesc=('USGS package')
  depends=('flashplugin')
  optdepends=('pepperflashplugin: for using ppapi version of flash player under chromium')
  install -Dm644 ${srcdir}/usgs.desktop ${pkgdir}/usr/share/applications/usgs.desktop
  install -Dm644 ${srcdir}/USGS.png ${pkgdir}/usr/share/ezgo/icons/USGS.png
  install -dm755 ${pkgdir}/usr/share/ezgo/ezgo-prt/usgs
  
  cd ${pkgdir}/usr/share/ezgo/ezgo-prt
  
  cp -v ${srcdir}/ezgo/ezgo-usgs/usgs_${_ezgover}.tar.gz ${pkgdir}/usr/share/ezgo/ezgo-prt/
  tar xfz usgs_${_ezgover}.tar.gz
  rm -rf ${pkgdir}/usr/share/ezgo/ezgo-prt/usgs
  ln -s ${pkgdir}/usr/share/ezgo/ezgo-prt/usgs_${_ezgover} ${pkgdir}/usr/share/ezgo/ezgo-prt/usgs
  rm -f ${pkgdir}/usr/share/ezgo/ezgo-prt/usgs_${_ezgover}.tar.gz
}

package_ezgo-wordtest() {
  pkgdesc=('Wordtest package')
  depends=('xdg-utils')
  install -dm755 ${pkgdir}/usr/share/ezgo/ezgo-wordtest
  cp -rv ${srcdir}/ezgo-wordtest/* ${pkgdir}/usr/share/ezgo/ezgo-wordtest/
  install -Dm644 ${srcdir}/ezgo-wordtest.desktop ${pkgdir}/usr/share/applications/ezgo-wordtest.desktop
}