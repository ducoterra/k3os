# Configuration Settings

## Requirements

1. Install kustomize

    ```bash
    brew install yq
    ```

2. Configure vault variables

    ```bash
    vault kv put secret/k3os-alpha.dnet/agent token=<token> server_url=<server_url>
    ```

3. Template your server or agent

    ```bash
    # server
    HOSTNAME=<HOSTNAME>; yq e ".hostname = \"$HOSTNAME\" | .k3os.token = \"$(vault kv get -field=token secret/k3os-alpha.dnet/agent)\" | .k3os.server_url = \"$(vault kv get -field=server_url secret/k3os-alpha.dnet/agent)\"" k3os_server.yaml > templates/$HOSTNAME.yaml

    # agent
    HOSTNAME=<HOSTNAME>; yq e ".hostname = \"$HOSTNAME\" | .k3os.token = \"$(vault kv get -field=token secret/k3os-alpha.dnet/agent)\" | .k3os.server_url = \"$(vault kv get -field=server_url secret/k3os-alpha.dnet/agent)\"" k3os_agent.yaml > templates/$HOSTNAME.yaml
    ```

4. Save the template to /var/lib/rancher/k3os/config.yaml

## Draining

```bash
kubectl --context mainframe-admin drain mainframe --force --ignore-daemonsets --delete-local-data
```

## Upgrading

```bash
kubectl label node k3os-alpha k3os.io/upgrade=enabled --overwrite
```

## Mounting

```bash
mount UUID='62A28E6D-EDC1-4825-BCD9-1F58601B5E36' /local
```

## Network

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
