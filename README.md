Workaround fixing no A2DP when BT headphone reconnects automatically (after being paired)
===

## updated 2019/03/30: This workaround might be no longer needed

I found [bluez-git](https://aur.archlinux.org/packages/bluez-git/) has upgraded to [the version that this issue no longer exists (5.50.r295.g9e6da22ed-1 > 5.50-264-g750a26cd9)](https://github.com/EHfive/pulseaudio-modules-bt/issues/14#issuecomment-462039332)

Now we can remove this and install [bluez-git](https://aur.archlinux.org/packages/bluez-git/):

```
yay -R fix-bt-a2dp
rm /etc/.fix-bt-a2dp.device-profiles /etc/.fix-bt-a2dp.user
yay -S bluez-git
```

after installing [bluez-git](https://aur.archlinux.org/packages/bluez-git/), please check out [my comments below](https://aur.archlinux.org/packages/bluez-git/#comment-688092)...there is a problem I have to fixed manually.

> Original README.md below

---

On my ArchLinux KDE plasma setup, BT headphone will use A2DP only when connected by pairing; after disconnect and reconnect, only HSP/HFP is available

> According to https://github.com/EHfive/pulseaudio-modules-bt/issues/14#issuecomment-462039332, this should soon become unnecessary

this workaround deploys a [`udev-rules`](https://wiki.archlinux.org/index.php/udev) to detect changes of BT dev and [`systemctl start fix-bt-a2dp`](https://wiki.archlinux.org/index.php/systemd) to call `fix-bt-a2dp.rb` in background with correct user

> basically a rewrite from https://gist.github.com/EHfive/c4f1218a75f95b076f0387403246de78, mainly because I want to avoid slowing down connecting of other BT devs

## Usage

install this AUR first:

```
yay -S fix-bt-a2dp
```

run this command with root to set GUI session owner:

```
/usr/bin/fix-bt-a2dp set-user [user]
```

## When used with `pulseaudio-modules-bt`

recently [pulseaudio-modules-bt](https://github.com/EHfive/pulseaudio-modules-bt) has added codec name after `a2dp_sink` profile, and `pacmd list-cards` tells that my MDR-1ABT only supports AptX...so I finally came up with a solution by telling `fix-bt-a2dp` what profile should be used for a device manually...(so `fix-bt-a2dp` will set card profile to what you assigned when connected)

```shell
bluetoothctl devices
# => Device 10:4F:A8:CE:DB:D2 MDR-1ABT
fix-bt-a2dp set-device-profile MDR-1ABT a2dp_sink_ldac
# currently known profiles are
#   a2dp_sink_sbc a2dp_sink_aac a2dp_sink_aptx a2dp_sink_aptx_hd a2dp_sink_ldac
```

---

