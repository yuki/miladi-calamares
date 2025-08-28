# Based on https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=calamares
# by Maintainer: Rustmilian Rustmilian@proton.me
# Modifications by: Rubén Gómez rugoli@gmail.com

pkgname=('calamares')

pkgver=3.4.0
pkgrel=1
pkgdesc='Distribution-independent installer framework'
arch=($CARCH)
url="https://codeberg.org/Calamares/calamares"

license=('BSD-2-Clause'
    'CC-BY-4.0'
    'CC0-1.0'
    'GPL-3.0-or-later'
    'LGPL-2.1-only'
    'LGPL-3.0-or-later'
    'MIT')

depends=(
    'efibootmgr'
    'gtk-update-icon-cache'
    'hwinfo'
    'icu'
    'kconfig>=5.246'
    'kcoreaddons>=5.246'
    'ki18n>=5.246'
    'kiconthemes>=5.246'
    'kio>=5.246'
    'kpmcore>=24.01.75'
    'libpwquality'
    'mkinitcpio-openswap'
    'polkit-qt6>=0.175.0'
    'qt6-base>=6.6.0'
    'qt6-svg>=6.6.0'
    'solid>=5.246'
    'squashfs-tools'
    'yaml-cpp'
    'ckbcomp'
)

makedepends=('extra-cmake-modules' 'qt6-tools' 'git')

backup=('usr/share/calamares/modules/bootloader.conf'
    'usr/share/calamares/modules/displaymanager.conf'
    'usr/share/calamares/modules/initcpio.conf'
    'usr/share/calamares/modules/unpackfs.conf')

source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")

sha256sums=('45de0214f4a16095374e2ed3982032c34f0f2c2104987089152e4b928dd0548f')


build() {
    cd "${srcdir}/${pkgname}" || return
    mkdir -p build
    cd build || return
    cmake .. \
        -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_INSTALL_LIBDIR=lib \
        -DWITH_QT6=ON \
        -DWITH_PYTHONQT=OFF \
        -DWITH_KF5DBus=OFF \
        -DBoost_NO_BOOST_CMAKE=ON \
        -DWEBVIEW_FORCE_WEBKIT=OFF \
        -DSKIP_MODULES="webview \
                        tracking \
                        interactiveterminal \
                        initramfs \
                        initramfscfg \
                        dracut \
                        dracutlukscfg \
                        dummyprocess \
                        dummypython \
                        dummycpp \
                        dummypythonqt \
                        services-openrc \
                        keyboardq \
                        localeq \
                        welcomeq"
    make
}

package_calamares() {
    cd "${srcdir}/${pkgname}/build" || return
    make DESTDIR="$pkgdir" install
    install -Dm644 "${srcdir}/${pkgname}/calamares.desktop" "$pkgdir/etc/xdg/autostart/calamares.desktop"
}
