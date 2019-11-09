# Scaleway Alpine Linux Conversion
- boot to rescue mode

- follow the guide here
https://community.scaleway.com/t/alpine-linux-on-arm64/6022

1. Boot to rescue mode
2. Format the hard drive
    ```
    mkfs.ext4 /dev/vda
    ```
3. mount the hard drive
    ```
    mount /dev/vda /mnt
    ```
4. Download & extract apk-tools-static
    ```
    wget http://dl-cdn.alpinelinux.org/alpine/v3.10/main/aarch64/apk-tools-static-2.10.4-r2.apk 
    tar xvzf apk-tools-static-2.10.4-r2.apk
    ```
5. Bootstrap Alpine Linux
    ```
    ./sbin/apk.static --arch aarch64 -X http://dl-cdn.alpinelinux.org/alpine/v3.10/main/ -U --allow-untrusted --root /mnt --initdb add alpine-base
    ```
- boostrap alpine linux

- skip everything else
- set up repositories
- chroot

- follow dockerfile instructions
apk update
apk add \
  blkid \
  busybox-initscripts \
  chrony \
  curl \
  dhclient \
  dosfstools \
  e2fsprogs \
  grub-efi \
  iptables \
  ip6tables \
  openrc \
  openssh \
  rsyslog \
  util-linux \
  bash \
  linux-vanilla
apk upgrade \
  openssl
  
add base files
- image-tools files
https://github.com/scaleway/image-tools/archive/master.tar.gz
cp /image-tools/bases/overlay-common/* / -r
cp /image/tools/bases/overlay-openrc/* / -r
- image-alpine files
https://github.com/scaleway/image-alpine/archive/master.tar.gz
cp /image-alpine/latest/overlay/* / -r
cp /image-alpine/latest/overlay-arm64/* / -r

configure all autostart packages
rc-update add sshd default\
  && rc-update add iptables default \
  && rc-update add ip6tables default \
  && rc-update add chronyd default \
  && rc-update add hostname default \
  && rc-update add sysctl default \
  && rc-update add rsyslog default \
  && rc-update add loopback default \
  && rc-update add scw-update-motd default \
  && rc-update add scw-generate-net-config default \
  && rc-update add scw-net-ipv6 default \
  && rc-update add scw-signal-booted default \
  && rc-update add scw-ssh-keys default \
  && rc-update add scw-initramfs-shutdown shutdown \
  && rc-update add scw-sync-kernel-extra default \
  && rc-update add scw-set-hostname default \
  && rc-update add scw-gen-machine-id default \
  && rc-update add scw-gen-root-passwd default \
  && rc-status
  
follow the rest of dockerfile
  # Remove the network configuration so it's generated at first boot
RUN > /etc/network/interfaces

# enable IPv6

RUN echo "ipv6" >> /etc/modules

# Allow login from ttyS0 (x86_64) and ttyAMA0 (ARM64)
RUN echo -e "ttyS0\nttyAMA0\n" >> /etc/securetty

# Update permissions
RUN chmod 700 /root

https://community.scaleway.com/t/alpine-linux-on-arm64/6022