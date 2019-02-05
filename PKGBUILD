# Maintainer: PastLeo <chgu82837@gmail.com>
pkgname=fix-bt-a2dp
pkgver=0.1
pkgrel=1
pkgdesc="Fix Bluetooth A2DP using systemd and udev rule"
arch=('any')
url="https://github.com/pastleo/fix-bt-a2dp"
license=('MIT')
depends=('ruby' 'bluez' 'bluez-utils' 'pulseaudio' 'pulseaudio-bluetooth')
optdepends=('libnotify')
source=(
  'fix-bt-a2dp.rb'
  'fix-bt-a2dp.service'
  'fix-bt-a2dp.udev-rules'
)
md5sums=(
  'f63057d641cb3c2e005653acdd6a4af9'
  '24aa8ecab3f87b3cd6f8a318d314b27d'
  '53997fa84224bae44cdd1c4b5f88550f'
)

package() {
  install -D -m755 ./fix-bt-a2dp.rb "$pkgdir/usr/bin/fix-bt-a2dp"
  install -D -m644 ./fix-bt-a2dp.service "$pkgdir/usr/lib/systemd/system/fix-bt-a2dp.service"
  install -D -m644 ./fix-bt-a2dp.udev-rules "$pkgdir/usr/lib/udev/rules.d/90-fix-bt-a2dp.rules"
}