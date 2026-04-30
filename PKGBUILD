# Maintainer: Tércio Martins <echo dGVyY2lvd2VuZGVsQGdtYWlsLmNvbQo= | base64 -d>

pkgname=epsonscan2
pkgver=6.7.87.0
_pkgver="$pkgver-1"
pkgrel=1
arch=('armv7h' 'x86_64')
pkgdesc="Epson scanner management utility"
url="https://support.epson.net/linux/en/epsonscan2.php"
license=('GPL-3.0-or-later')
depends=('libjpeg-turbo' 'libpng' 'libtiff' 'libusb' 'qt5-base' 'sane' 'zlib')
makedepends=('boost' 'cmake' 'qt5-singlecoreapplication' 'rapidjson')
optdepends=('epsonscan2-non-free-plugin: OCR support and wireless scanning')
options=('!buildflags')
source=('https://download-center.epson.com/f/module/1ef33427-5366-4a18-9726-c44197b04301/epsonscan2-6.7.87.0-1.src.tar.gz'
        '0002-Fix-crash.patch'
        '0003-Use-XDG-open-to-open-the-directory.patch'
        '0004-Fix-a-crash-on-an-OOB-container-access.patch'
        '0005-Fix-crash-no-serial-number.patch'
        '0006-Fix-folder-creation-crash.patch'
        '0007-Fix-scanner-connect-crash.patch')
DLAGENTS=(
  "https::/usr/bin/curl -A 'Mozilla' -fLC - --retry 3 --retry-delay 3 -o %o %u"
)
b2sums=('0e9ce73d830532e3c0bc188e066fea6df3900bbfb9dd0b9c7179f6baf98b282344b6a51589e408dbafda91b59404e9cca58b787258a5aa8fc33e003d553a0c13'
        '9637be5374f6406b79b0004486764d4b6f8b3c113ac880df7c6baf87808807463627fc3d365d164ffc77644daf04d936b7a60e1f9514c36941e94c77377d2be7'
        '0709b3fa136fb06d630e1140856c48243fe1f49d01c5c193b690acd04d75d41527162a3e006b452285f11e557726a4405682d1a4153241a5c94bb53c959e3179'
        'f788de817d7543efaa43e7fdf56a00f168f74777fdf2ccbdee509c4786cbd1fdbed6deb65d8caa85159eb2c333323fb2a392d60ad202e22d2bc1353c344fb7f1'
        '282a18ad086446f290d795141d63235e67416cea894945d2c65dac7ffa36b3288ef920ef627df349f06e5f482b16e8fa6dbd0064db4b701437a01b913bd8a3fb'
        '4561d42cbbd6ae12ac62808e6cdc3d81c7f412a7bd67daaf0c1ca250bfd4da4886192145627146185f55016bfe73daebd23e0884563bf70279d1bbb9fbdf63cc'
        '9293ba06edd38b48f0222240d6c956fa731afe0a2c49221bb3604b44cee64be60c091f54d1cbe1be4275f0e16f690e05625e96a2287058fcb9bbcd6167b9ccca')

prepare() {
  sed -i 's|/lib/udev|${CMAKE_INSTALL_PREFIX}/lib/udev|' \
         "$srcdir/$pkgname-$_pkgver/CMakeLists.txt"

  sed -i '1 i #include "zlib.h"' \
         "$srcdir/$pkgname-$_pkgver/src/CommonUtility/DbgLog.cpp"
 
  sed -i '/zlib/d' \
         "$srcdir/$pkgname-$_pkgver/src/Controller/CMakeLists.txt"

  # Stability improvements from Flatpak maintainers
  # https://github.com/flathub/net.epson.epsonscan2
  for file in 0002-Fix-crash \
              0003-Use-XDG-open-to-open-the-directory \
              0004-Fix-a-crash-on-an-OOB-container-access \
              0005-Fix-crash-no-serial-number \
              0006-Fix-folder-creation-crash \
              0007-Fix-scanner-connect-crash
  do
    patch --directory="$srcdir/$pkgname-$_pkgver" --forward --binary --strip=1 --input="$srcdir/$file.patch"
  done

  # Remove Boost setting in CMake config that crashes the package build
  find "$srcdir/$pkgname-$_pkgver" -type f -name CMakeLists.txt \
       -exec sed -i '/BOOST_NO_CXX11_RVALUE_REFERENCES/d' {} \;

  for file in Standalone/lastusedsettings.cpp \
              Standalone/defaultsettings.cpp \
              CommonUtility/ESCommonTypedef.h \
              Controller/Src/KeysValues/Key.hpp \
              Controller/Src/KeysValues/KeyMgr.hpp
  do
    sed -i '/BOOST_NO_CXX11_RVALUE_REFERENCES/d' \
           "$srcdir/$pkgname-$_pkgver/src/$file"
  done

  # Remove support for older versions of CMake in the configuration scripts
  # (needed to build the package)
  for dir in . \
             src \
             src/Standalone \
             src/ScanSDK \
             src/ScanSDK/Src/SDK/SCANSDKsample_C++ \
             src/DetectAlert
  do
    sed -Ei '/cmake_minimum_required/ s/2\.([0-9]+|\.)+/4.0/' \
            "$srcdir/$pkgname-$_pkgver/$dir/CMakeLists.txt"
  done

  # Fix compilation failure caused by GCC 15
  sed -i '/SET.*FLAGS/ s/")/ -Wno-template-body")/' \
         "$srcdir/$pkgname-$_pkgver/src/ES2Command/Linux/CMakeLists.txt"
}

build() {
  cmake $pkgname-$_pkgver \
        -B build \
        -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DEPSON_OCR_INSTALL_PATH="/usr/share/epsonscan2-ocr" \
        -DQT_VERSION_MAJOR=5
        
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build

  install -Dm644 "$srcdir/$pkgname-$_pkgver/desktop/rpm/i686/$pkgname.desktop" \
                 "$pkgdir/usr/share/applications/$pkgname.desktop"

  install -d $pkgdir/usr/lib/sane ; cd $pkgdir/usr/lib/sane
}
