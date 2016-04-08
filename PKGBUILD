pkgbase=ezgo
pkgname=('grub2-themes-ezgo' 'ezgo-wallpapers' # Looks and feels of ezgo
         'ezgo-chem' 'ezgo-doc' 'ezgo-gsyan'    # Applications of ezgo
         'ezgo-misc' 'ezgo-npa' 'ezgo-phet' 'ezgo-usgs' 'ezgo-wordtest' # Utilities of ezgo
         # Metapackage for ezgo
         'ezgo-accessories' 'ezgo-education' 'ezgo-games' 'ezgo-common'
         'ezgo-graphics' 'ezgo-lang-zh_TW-desktop'
         'ezgo-multimedia' 'ezgo-network' 'ezgo-office')
pkgver=12.0
_ezgover=ezgo12
pkgrel=1
arch=('x86_64')
_ezgosource="ftp://goodhorse.idv.tw/debian-ezgo"
_phetver=PhET2015
groups=("$pkgbase")
source=("git+https://anonscm.debian.org/git/blends/projects/ezgo.git"
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
	'ezgo-wordtest.desktop'
	)
sha1sums=('SKIP'
          'be1ed0b3f1da77ce9393eea84413193e771ebac2'
          'bf477a9e0ed96b16ecb1c99b6ee5272916ed9ec7'
          'c8c01ff2c8dcb8207fb58543e4711fa935389fb6'
          '795eb6326fdbe8b3b98d4cd50d37cd32931acfb1'
          'c8acee50114fd03aad47dd1d6e5bcb5b34055843'
          '85b3771e2ce2a177b445137a185cf0a04122aca9'
          '6263a94dc8c07101d9db589c127fe6dc03e168d6'
          '51039c479ef138409fcc864f35e379e25ec0415f'
          '3d09ac6ebad61ce0f8dd59c183f44bcef92e7e2b'
          'ac61f263705bc3f7d2f080505d7684768eb06c4d'
          '605e02fd58133e4029fcb7950066245216cbe2e3'
          '26ff8b02cc75783f931179cecf6ef5e562e06dba'
          '3254f9a55159e1bbf2c411e9b1e9130497d95a14'
          '907f0a1dea4c117b9b20da75d4c50ff5c1354d65'
          'd0ebe36fcbe82bd81bad8b340d0ddf468d944d15')
# TODO: licensing all the packages

prepare() {
  # some of the tarballs come within the git repo
  msg 'Moving tarballs from git repo'
  mv -v ${srcdir}/ezgo/ezgo-misc/7zip.tar.gz ${srcdir}
  mv -v ${srcdir}/ezgo/ezgo-usgs/usgs_${_ezgover}.tar.gz ${srcdir}
  msg  'extract 7zip archive'
  cd ${srcdir}
  tar xf 7zip.tar.gz
  msg 'extract ezgo-usgs'
  tar xf usgs_${_ezgover}.tar.gz
}
package_ezgo-wallpapers() {
  pkgdesc='Set of wallpapers sepecified for Ezgo project'
  groups+=('ezgo-artwork' 'ezgo-tasks')
  # KDE wallpaper
  # Install images
  cd ${srcdir}/${pkgbase}/${pkgbase}-artwork/wallpaper
  install -dm755 ${pkgdir}/usr/share/wallpapers/
  cp -rv ezgo ${pkgdir}/usr/share/wallpapers/
  cp -rv ezgo-walter ${pkgdir}/usr/share/wallpapers/
}

package_grub2-themes-ezgo() {
  groups+=('ezgo-artwork' 'ezgo-tasks')
  depends=('grub')
  # GRUB2 background
  cd ${srcdir}/${pkgbase}/${pkgbase}-artwork/grub/
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
  optdepends=('pepperflashplugin: for chromium-based browsers'
	      'flashplugin: adobe flash plugin for web browsers')
  install -Dm644 ${srcdir}/gsyan.desktop ${pkgdir}/usr/share/applications/gsyan.desktop
  install -dm755 ${pkgdir}/usr/share/ezgo/ezgo-prt/gsyan
  cp -rv ${srcdir}/gsyan_${_ezgover}/* ${pkgdir}/usr/share/ezgo/ezgo-prt/gsyan/
}

package_ezgo-misc() {
  # TODO: This is a big package bundled with several utilities that aren't belonging to the repo.
  #       Maybe, we should make this a meta package?
  pkgdesc=('Misc utilities for ezgo project - meta package')
  depends=('flashplugin' 'openjdk' 'chromium' 'skype' 'wine' 'sound-theme-freedesktop')
  optdepends=('pepperflashplugin: for using ppapi version of flash player under chromium')
  
  msg 'Installing media pack'
  echo 'We may not need all these utilities'
  # NOTE: we've included most of the free codecs in Chakra
 
  msg 'Installing 7zipFM.exe (requires wine)'
<<<<<<< HEAD
  install -dm755 ${pkgdir}/opt/7zip
  mv -v ${srcdir}/7-Zip ${pkgdir}/opt/7zip
=======
  cp -vrP ${srcdir}/7-Zip ${pkgdir}/opt/7zip
>>>>>>> c1a1f674733b6d52ed666ba1be16251d7bfa1ba8
  install -Dm644 ${srcdir}/7z.desktop ${pkgdir}/usr/share/applications/7z.desktop
  
  msg 'Install MIME type values'
  install -Dm644 ${srcdir}/${pkgbase}/${pkgname}/mimeapps.list ${pkgdir}/usr/share/applications/mimeapps.list
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
  cp -vrf ${srcdir}/usgs_${_ezgover}/* ${pkgdir}/usr/share/ezgo/ezgo-prt/usgs/
}

package_ezgo-wordtest() {
  pkgdesc=('Wordtest package')
  depends=('xdg-utils' 'python2')
  install -dm755 ${pkgdir}/usr/share/ezgo/ezgo-wordtest
  cp -rv ${srcdir}/ezgo/ezgo-wordtest/* ${pkgdir}/usr/share/ezgo/ezgo-wordtest/
  install -Dm644 ${srcdir}/ezgo-wordtest.desktop ${pkgdir}/usr/share/applications/ezgo-wordtest.desktop
  install -Dm755 ${srcdir}/ezgo/ezgo-wordtest/wordtest.sh ${pkgdir}/usr/bin/wordtest
}

package_ezgo-accessories() {
  pkgdesc=('Extra accessory packages for ezgo - meta package')
  depends=('convertall' 'kate' 'kcalc' 'kmag')
  groups+=('ezgo-tasks')
  echo "This is a ezgo-accessories meta package."
}

package_ezgo-common() {
  pkgdesc=('Common packages for ezgo - meta package')
  depends=('mesa' 'bash-completion' 'openssh')
  groups+=('ezgo-tasks')
  echo "This is a ezgo-common meta package."
}
# NOTE: these are standard Chakra packages

package_ezgo-education() {
  pkgdesc=('Educational packages for ezgo - meta package')
  depends=('kdeedu' 'wxmaxima' 'avogadro' 'stellarium' 'gcompris' 'ktuberling' 'anki')
  groups+=('ezgo-tasks')
  echo "This is a ezgo-education meta package."
}

package_ezgo-games() {
  pkgdesc=('Game packages selected by ezgo - meta package')
  depends=('supertux' 'pingus' 'supertuxkart' 'kdegames-ksudoku' 'picmi' 'kblocks' 'kdegames-palapeli' 'kdegames-kubrick'
           'ksquares' 'knetwalk' 'kblackbox' 'kdegames-kigo' 'kdegames-kreversi' 'kfourinline' 'bovo' 'ktuberling')
  groups+=('ezgo-tasks')
  msg 'install ktuberling sound theme'
  cd ${srcdir}/${pkgbase}/ezgo-misc/ktuberling
  install -dm755 ${pkgdir}/usr/share/apps/ktuberling/sounds/zh_TW/
  pwd
  for files in $(ls zh_TW); do
  pwd
  install -Dm644 zh_TW/${files} ${pkgdir}/usr/share/apps/ktuberling/sounds/zh_TW/${files}
  done
  install -Dm644 zh_TW.soundtheme ${pkgdir}/usr/share/apps/ktuberling/sounds/zh_TW.soundtheme
}

package_ezgo-graphics() {
  pkgdesc=('Graphical packages for ezgo - meta package')
  depends=('kdegraphics-kolourpaint' 'tuxpaint' 'inkscape' 'scribus' 'digikam' 'gwenview' 'blender' 'fotowall'
           'hugin' 'krita' 'freecad' 'kruler' 'kdegraphics-kolourpaint' 'kamoso' 'librecad')
  groups+=('ezgo-tasks')
  echo "This is a ezgo-graphics meta package."
}

package_ezgo-lang-zh_TW-desktop() {
  pkgdesc=('Zh_TW localized packages for ezgo desktop - meta package')
  depends=('otc-source-han-sans' 'kde-l10n-zh_TW')
  groups+=('ezgo-tasks')
  echo "This is a ezgo-lang-zh_TW-desktop meta package."
}

package_ezgo-multimedia() {
  pkgdesc=('Multimedia packages for ezgo - meta package')
  depends=('amarok' 'vlc' 'audacity' 'tuxguitar' 'rosegarden' 'kdenlive' 'k3b' 'musescore' 'kodi' 'lmms' 'hydrogen'
           'winff' 'ardour' 'timidity++')
  groups+=('ezgo-tasks')
  echo "This is a ezgo-multimedia meta package."
}

package_ezgo-network() {
  pkgdesc=('Meta package to pull all ezgo-network related packages')
  depends=('pidgin' 'kdenetwork-kopete' 'qftp' 'filezilla' 'kdenetwork-krdc')
  groups+=('ezgo-tasks')
  echo "This is a ezgo-network meta package."
  # FIXME: Consider rolling to ktp instead of kopete, which is unmaintained for long
}

package_ezgo-office() {
  pkgdesc=('Meta package to pull all ezgo-office related packages')
  depends=('okular' 'scribus' 'calibre')
  groups+=('ezgo-tasks')
  echo "This is a ezgo-officek meta package."
}
