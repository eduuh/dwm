# Homelab

This is the companion configuration that goes with the video from [Dreams of Autonomy](https://youtu.be/2yplBzPCghA).

This project is split into different directories depending on each service used.

## Requirements

To use this, you'll need the following installed on your sysetm

- nix
- kubectl
- helmfile
- helm
- git

Additionally, you'll also want to make changes to the user information found in the `nixos/configuration.nix`

## DevTools

- rust
- make (c & c++) tools
- typescript & js tools
- My custom nvim config

## nixos

This directory contains the nixos configuration for setting
up each node with k3s.

The configuration makes use of nix flakes under the hood, with each node configuration being:
```
homelab-0  - Arch
homelab-1  - Nix
```
## Future

```
- homelab-2   -Nix
- homelab-3  - Nix
```

To set up a node from fresh, you can use [nixos-anywhere](https://github.com/nix-community/nixos-anywhere). This requires loading the nixos installer and then booting the node into it. You can then install remotely once you've set the nodes password using the `passwd` command. 

The command I use is as follows:

```shell
nix run github:nix-community/nixos-anywhere \
--extra-experimental-features "nix-command flakes" \
-- --flake '.#homelab-0' nixos@192.168.1.100
```

make sure to replace with your own ip.

## helm

This directory is used to store the helm configuration of the node and is managed using [helmfile](https://github.com/helmfile/helmfile), which is a declarative spec for defining helm charts.

To install this on your cluster, you can simply use the following command.

```
helmfile apply
```
## kustomize

Kustomize allows you to manage multiple manifest files in a `Kustomize.yaml`, which also allows you to override values if you need to.

I don't use Kustomize that much in the video, but it's a tool I do often use and is available in `kubectl`.


## Todo



### Skills

#### Connect to wifi from cli

1. Check if wifi is enabled

```
nmcli radio wifi
```

2. if not enabled, you can do this.

```
nmcli radio wifi on
```

3. check network status

```
nmcli dev status

```

4. Check available connections

```
sudo dev wifi list
```

5. Connect using SSID: Enter the password

```
sudo nmcli --ask dev wifi connect eduuh_local
```
#### Use Mac Address to bind ip address to router

1. Check mac address: Mac address is Layer 2 of OSI
2. Bind mac address to router-ip


#### Arch: Install K3s

1. Kubectl:

```
sudo pacman -S kubectl
```

2. Kustomize

```
sudo pacman -S kustomize
