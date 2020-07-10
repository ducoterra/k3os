# Configuration Settings

## Upgrade

```bash
kubectl label node mainframe plan.upgrade.cattle.io/k3os-latest=enabled --overwrite
```

## Mounting

```bash
mount UUID='62A28E6D-EDC1-4825-BCD9-1F58601B5E36' /local
```

## Draining

```bash
kubectl drain mainframe --force --ignore-daemonsets --delete-local-data
```

## Network

https://help.ui.com/hc/en-us/articles/115013212107-UFiber-Enabling-Ubiquiti-SFP-and-SFP-Modules-on-Third-Party-Devices

```bash
ip addr add 6.0.22.1/30 dev eth1
ip link set eth1 up
ifconfig eth1 down && ifconfig eth1 up
```

ifconfig ix0 6.0.22.2 netmask 255.255.255.0 broadcast 6.0.22.255
ifconfig ix0 down && ifconfig ix0 up

ifconfig eth1 6.0.22.1/30 broadcast 6.0.22.3
ifconfig eth1 down && ifconfig eth1 up

## Testing


### Disk

```bash
dd if=/dev/zero of=/media/nfs/output bs=16k count=100k; dd if=/media/nfs/output of=/dev/null; rm -f /media/nfs/output
```

dd if=/dev/zero of=/mnt/enc0/kube/output bs=16k count=100k; dd if=/mnt/enc0/kube/output of=/dev/null; rm -f /mnt/enc0/kube/output

1,073,741,824

ix0
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-60.00  sec  6.58 GBytes   942 Mbits/sec                  receiver

ix1
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-60.00  sec  6.57 GBytes   941 Mbits/sec                  receiver