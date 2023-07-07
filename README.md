Cloudflare Warp client (system container)
=========================================

System(d) container for use with Podman Machine, MicroShift, OpenShift Local and Podman Desktop installations, etc.


### Usage

#### Container creation
Start the system container. You can choose between the following options: [Debian](./#debian-based), [Fedora](./#fedora-based) or [RHEL UBI9](./#rhel-ubi9-based)

##### Debian-based
```
$ podman run -d --name=cloudflarewarp \
        --hostname $HOSTNAME-cloudflarewarp \
        --network=host --systemd=always \
        ghcr.io/spotsnel/cloudflare-client:latest
```

##### Fedora-based
```
$ podman run -d --name=cloudflarewarp \
        --hostname $HOSTNAME-cloudflarewarp \
        --network=host --systemd=always \
        ghcr.io/spotsnel/cloudflare-client/fedora:latest
```

##### RHEL UBI9-based
```
$ podman run -d --name=cloudflarewarp \
        --hostname $HOSTNAME-cloudflarewarp \
        --network=host --systemd=always \
        ghcr.io/spotsnel/cloudflare-client/ubi9:latest
```

#### Client registration
Register the client with 
```
$ podman exec -it cloudflarewarp warp-cli register 
```

or using a team account with 

```
$ podman exec -it cloudflarewarp warp-cli teams-enroll 
```
per instructions at https://github.com/spotsnel/cloudflare-client/discussions/1

Use the CLI, Podman Desktop or Cockpit terminal to do so.

#### Systemd
The lifecycle of the container can be maintained by the host using a systemd service unit:

```
$ (cd $HOME/.config/systemd/user && podman generate systemd --name --files cloudflarewarp 
$ systemctl --user enable --now container-cloudflarewarp
$ loginctl enable-linger $USER
```