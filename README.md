# Configuration Settings

## Draining

```bash
kubectl --context mainframe-admin drain mainframe --force --ignore-daemonsets --delete-local-data
```

## Upgrading

```bash
kubectl label node mainframe plan.upgrade.cattle.io/k3os-latest=enabled --overwrite
```

## Mounting

```bash
mount UUID='62A28E6D-EDC1-4825-BCD9-1F58601B5E36' /local
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
