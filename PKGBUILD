# Maintainer: Caribpa <caribpa dot git at outlook dot com>

pkgname=kmodcache-git
pkgver=1
pkgrel=1
pkgdesc="Temporarily backups the current kernel's modules after a kernel upgrade to keep allowing loading modules without rebooting"
arch=('any')
license=('GPL3')
conflicts=('kmodcache'
           'kernel-modules-hook'
           'saved-kernel-modules')
install=kmodcache.install

# Uncomment this and comment ${optdepends} if we will always have rsync installed
# depends=('rsync')

# Comment ${depends} and this if we won't ever install rsync
optdepends=('rsync')

source=('kmodcache'
        'kmodcache.hook'
        'kmodcache.sh'
        'rsync.patch'
        'no-rsync.patch')
sha256sums=('3a8e41b2e694071fa407e2b4b2721de5e637b434ded5c28d2f08751cfff88602'
            '878d3fe3ae660b29555962c05f5a87639dcc909b3a0ca04ba13a91d0f6c024e2'
            '88d0f32880c5ac4d85ff57c8a3ede0d929207226356a31f2940ceca68635fef2'
            '146a8a0716daa6be23c055a451b5e1c9a1ee878da56eea11073c41a53728460d'
            '7a15511f6b47b9e5511154406d5313f75482e48105e895240c4d0e32c3b43302')

prepare() {
    if [ -n "${depends}" ]; then
        patch --follow-symlinks -p1 -i rsync.patch
    elif [ -z "${optdepends}" ]; then
        patch --follow-symlinks -p1 -i no-rsync.patch
    fi
}

package() {
	  install -m 755 -d \
            "${pkgdir}"/usr/lib/modules \
            "${pkgdir}"/etc/pacman.d/hooks \
            "${pkgdir}"/etc/pacman.d/hooks/files \
            "${pkgdir}"/run/kmods \
            "${pkgdir}"/etc/profile.d
	  install -m 755 kmodcache "${pkgdir}"/etc/pacman.d/hooks/files
	  install -m 755 kmodcache.sh "${pkgdir}"/etc/profile.d
	  install -m 644 kmodcache.hook "${pkgdir}"/etc/pacman.d/hooks/0_kmodcache.hook
    ln -s /run/kmods "${pkgdir}"/usr/lib/modules/cached
}
