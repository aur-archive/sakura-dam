# Maintainer: SiD / sidious <miste78 at web de>
# (d)on't (a)sk (m)e ;)

pkgname=sakura-dam
_pkgname=sakura
pkgver=2.4.2
pkgrel=1
pkgdesc="A terminal emulator based on GTK and VTE with disabled really close question"
arch=('i686' 'x86_64')
url="http://pleyades.net/david/sakura.php"
license=('GPL')
depends=('vte' 'libxft' 'desktop-file-utils')
makedepends=('cmake')
provides=('sakura')
conflicts=('sakura')
source=(http://pleyades.net/david/projects/$_pkgname/$_pkgname-$pkgver.tar.bz2 closequestion.patch)
install=sakura.install

md5sums=('46669519c77f7402b2de24cdefe251bb'
         '356403228a2c0da2f31c4c848c041c0f')

build() {
  cd $srcdir/${_pkgname}-${pkgver}

  # Set default font size a bit smaller
  sed -i 's|#define DEFAULT_FONT "Bitstream Vera Sans Mono 14"|#define DEFAULT_FONT "Bitstream Vera Sans Mono 10"|g' src/sakura.c

  # Disable "really close question"
  patch -Np0 -i ${srcdir}/closequestion.patch
   
  # build & install	
  cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=RELEASE . 
  make 
}

package() {
  cd $srcdir/${_pkgname}-${pkgver}

  make DESTDIR=${pkgdir} install 
  # extract the keybindings from the installed documentation, rest is only relevant during build time
  awk '/^Keybindings/{f="'${pkgdir}'/usr/share/doc/'${_pkgname}'/KEYBINDINGS"} f{print > f} /^END/' \
        ${pkgdir}/usr/share/doc/${_pkgname}/INSTALL
  rm ${pkgdir}/usr/share/doc/${_pkgname}/INSTALL
}

