pkgname=archivedir
pkgver=0.1.4
pkgrel=1
pkgdesc="Archive directories per configuration"
arch=('any')
license=('MIT')
depends=('bash' 'findutils' 'coreutils' 'grep')
source=(
  $pkgname
  ${pkgname}-runner
  ${pkgname}.service
  ${pkgname}.timer
)
md5sums=(
  'SKIP'
  'SKIP'
  'SKIP'
  'SKIP'
)
package() {
  mkdir -p $pkgdir/etc/archivedirtab.d
  mkdir -p $pkgdir/usr/bin/
  install -Dm755 ${pkgname} $pkgdir/usr/bin/${pkgname}
  install -Dm755 ${pkgname}-runner $pkgdir/usr/bin/${pkgname}-runner
  mkdir -p $pkgdir/etc/systemd/system/timers.target.wants

  install -Dm644 ${pkgname}.service $pkgdir/usr/lib/systemd/system/${pkgname}.service
  install -Dm644 ${pkgname}.timer $pkgdir/usr/lib/systemd/system/${pkgname}.timer

  mkdir -p $pkgdir/etc/systemd/system/timers.target.wants
  ln -sf /usr/lib/systemd/system/${pkgname}.timer $pkgdir/etc/systemd/system/timers.target.wants
}
