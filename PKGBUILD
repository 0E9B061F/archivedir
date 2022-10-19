pkgname=archivedir
pkgver=0.2.2
pkgrel=1
pkgdesc="Archive files in a target directory older than a given age"
arch=('any')
license=('MIT')
depends=('bash' 'findutils' 'coreutils' 'grep')
source=(
  $pkgname
  ${pkgname}-runner
  ${pkgname}.service
  ${pkgname}.timer
)
md5sums=('f152e0b4685b3955d6ea14bf6ecdef76'
         '5a330e8e84afc7c1bd5cd860ce1f3e33'
         '9000ec705af46ea5fd1d49176b325590'
         '280de9bea28be2b60022dde715d7a3f2')
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
