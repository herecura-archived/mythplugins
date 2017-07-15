# $Id: PKGBUILD 219145 2017-03-26 17:09:12Z alucryd $
# Maintainer:
# Contributor: Jonathan Conder <jonno.conder@gmail.com>
# Contributor: Giovanni Scafora <giovanni@archlinux.org>

pkgbase=mythplugins
pkgname=('mythplugins-mytharchive'
         'mythplugins-mythbrowser'
         'mythplugins-mythgallery'
         'mythplugins-mythgame'
         'mythplugins-mythmusic'
         'mythplugins-mythnetvision'
         'mythplugins-mythnews'
         'mythplugins-mythweather'
         'mythplugins-mythweb'
         'mythplugins-mythzoneminder')
pkgver=0.28.1
pkgrel=4
epoch=1
arch=('i686' 'x86_64')
url="http://www.mythtv.org"
license=('GPL')
makedepends=('cdrtools' 'dvdauthor' 'dvd+rw-tools' 'ffmpeg' 'flac' 'libexif'
             'libvorbis' 'mesa' 'mesa-libgl' 'mythtv'
             'perl-datetime-format-iso8601' 'perl-date-manip' 'perl-image-size'
             'perl-json' 'perl-libwww' 'perl-soap-lite' 'perl-xml-sax'
             'perl-xml-simple' 'perl-xml-xpath' 'python2-oauth' 'python2-pillow'
             'python2-pycurl' 'zlib' 'gdb')
source=("mythtv-$pkgver.tar.gz::https://github.com/MythTV/mythtv/archive/v$pkgver.tar.gz"
        "mythweb-$pkgver.tar.gz::https://github.com/MythTV/mythweb/archive/v$pkgver.tar.gz"
        'cdparanoia.patch')
sha256sums=('f59688bbb69ef8830cfe76c826ec89027ed0a9bbb75cc97935fc664225b89dee'
            'bbd82992230d3571eba55a26a91cc3f2dcddfa631d1822ce58e1bf99f2537244'
            '004f1e4734830709d2ab5ebb804560514f2bf525abc2f11142501a81eba0754c')

prepare() {
  cd "$srcdir/mythtv-$pkgver/$pkgbase"

  find . -name '*.py' -type f | xargs sed -i 's@^#!.*python$@#!/usr/bin/python2@'
  patch -Np1 -i "$srcdir/cdparanoia.patch"

  cd "$srcdir/mythweb-$pkgver"

  sed -re 's@/usr/local.*/usr/share@/usr/share@' -i 'mythweb.php'
}

build() {
  cd "$srcdir/mythtv-$pkgver/$pkgbase"

  ./configure --prefix=/usr \
              --enable-all \
              --python=python2
  qmake-qt5 mythplugins.pro
  make -s
}

package_mythplugins-mytharchive() {
  pkgdesc="Create DVDs or archive recorded shows in MythTV"
  depends=('cdrtools' 'dvdauthor' 'dvd+rw-tools' 'ffmpeg' 'mythtv'
           'python2-pillow')

  cd "$srcdir/mythtv-$pkgver/$pkgbase/mytharchive"
  make INSTALL_ROOT="$pkgdir" install
}

package_mythplugins-mythbrowser() {
  pkgdesc="Mini web browser for MythTV"
  depends=('mythtv')

  cd "$srcdir/mythtv-$pkgver/$pkgbase/mythbrowser"
  make INSTALL_ROOT="$pkgdir" install
}

package_mythplugins-mythgallery() {
  pkgdesc="Image gallery plugin for MythTV"
  depends=('libexif' 'mythtv')

  cd "$srcdir/mythtv-$pkgver/$pkgbase/mythgallery"
  make INSTALL_ROOT="$pkgdir" install
}

package_mythplugins-mythgame() {
  pkgdesc="Game emulator plugin for MythTV"
  depends=('mythtv')

  cd "$srcdir/mythtv-$pkgver/$pkgbase/mythgame"
  make INSTALL_ROOT="$pkgdir" install
}

package_mythplugins-mythmusic() {
  pkgdesc="Music playing plugin for MythTV"
  depends=('mythtv' 'libcdio-paranoia')

  cd "$srcdir/mythtv-$pkgver/$pkgbase/mythmusic"
  make INSTALL_ROOT="$pkgdir" install
}

package_mythplugins-mythnetvision() {
  pkgdesc="MythNetvision plugin for MythTV"
  depends=('mythtv' 'python2-oauth')

  cd "$srcdir/mythtv-$pkgver/$pkgbase/mythnetvision"
  make INSTALL_ROOT="$pkgdir" install
}

package_mythplugins-mythnews() {
  pkgdesc="News checking plugin for MythTV"
  depends=('mythtv')

  cd "$srcdir/mythtv-$pkgver/$pkgbase/mythnews"
  make INSTALL_ROOT="$pkgdir" install
}

package_mythplugins-mythweather() {
  pkgdesc="Weather checking plugin for MythTV"
  depends=('mythtv' 'perl-date-manip' 'perl-json' 'perl-soap-lite'
           'perl-xml-sax' 'perl-xml-simple' 'perl-xml-xpath' 'perl-image-size'
           'perl-datetime-format-iso8601')

  cd "$srcdir/mythtv-$pkgver/$pkgbase/mythweather"
  make INSTALL_ROOT="$pkgdir" install
}

package_mythplugins-mythweb() {
  pkgdesc="Web interface for the MythTV scheduler"
  depends=('mythtv')
  optdepends=('lighttpd'
              'php-apache')
  install='mythplugins-mythweb.install'

  mkdir -p "$pkgdir/var/lib/mythtv/mythweb"/{image_cache,php_sessions}
  cp -R "$srcdir/mythweb-$pkgver"/* "$pkgdir/var/lib/mythtv/mythweb"
  chown -R http:http "$pkgdir/var/lib/mythtv/mythweb"
  chmod g+rw "$pkgdir/var/lib/mythtv/mythweb"/{image_cache,php_sessions}
}

package_mythplugins-mythzoneminder() {
  pkgdesc="View CCTV footage from zoneminder in MythTV"
  depends=('mythtv')
  install='mythplugins-mythzoneminder.install'

  cd "$srcdir/mythtv-$pkgver/$pkgbase/mythzoneminder"
  make INSTALL_ROOT="$pkgdir" install
}
