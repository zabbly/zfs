# ZFS builds
Those are ZFS tools and dkms builds made and supported by Zabbly.

They are designed to work reliably with the matching [kernel build](https://github.com/zabbly/linux).

## Availability
Those ZFS packages are built for:

 * Ubuntu 22.04 LTS (`jammy`)
 * Ubuntu 24.04 LTS (`noble`)
 * Debian 11 (`bullseye`) (`x86_64` only)
 * Debian 12 (`bookworm`)
 * Debian 13 (`trixie`)

## Installation

### Add the stable repository 
On any of those, you can add the package repository at `/etc/apt/sources.list.d/zabbly-kernel-stable.sources`:

```
Enabled: yes
Types: deb deb-src
URIs: https://pkgs.zabbly.com/kernel/stable
Suites: DISTRO
Components: zfs
Architectures: ARCH
Signed-By: /etc/apt/keyrings/zabbly.asc
```

Make sure to replace `DISTRO` with one of  `jammy`, `noble`, `bullseye`, `bookworm` or `trixie`
and then replace `ARCH` with one of `amd64` or `arm64`.

If you're already using the kernel builds from the same repository, change the `Components` line to read:
```
Components: main zfs
```

### Add the repository key
After that, add the [GPG keyring](https://pkgs.zabbly.com/key.asc) to `/etc/apt/keyrings/zabbly.asc`. 
Packages provided by the repository are signed. In order to verify the integrity of the packages, you need to import the public key. 
First, verify that the fingerprint your observe on the package repository matches the one listed below:

```sh
curl -fsSL https://pkgs.zabbly.com/key.asc | gpg --show-keys --fingerprint
```

Alternatively using wget (curl is not installed by default on Debian):

```sh
wget -qO- https://pkgs.zabbly.com/key.asc | gpg --show-keys --fingerprint
```

Compare that using your eyes with this authoritative fingerprint:
```sh
pub   rsa3072 2023-08-23 [SC] [expires: 2030-08-17]
      4EFC 5906 96CB 15B8 7C73  A3AD 82CC 8797 C838 DCFD
uid                      Zabbly Kernel Builds <info@zabbly.com>
sub   rsa3072 2023-08-23 [E] [expires: 2030-08-17]
```

If they match, save the key locally:

```sh
mkdir -p /etc/apt/keyrings/
curl -fsSL https://pkgs.zabbly.com/key.asc -o /etc/apt/keyrings/zabbly.asc
```
Alternatively using wget:

```sh
mkdir -p /etc/apt/keyrings/
wget -q https://pkgs.zabbly.com/key.asc -O /etc/apt/keyrings/zabbly.asc
```

### Finally install ZFS
To install ZFS, run: `apt-get install openzfs-zfsutils openzfs-zfs-dkms openzfs-zfs-initramfs`

## Repository
This repository gets actively rebased as new releases come out, DO NOT expect a linear git history.
