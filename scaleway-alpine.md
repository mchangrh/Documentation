# Scaleway Alpine Linux Conversion

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
6. Set up repositories
    ```
    echo http://dl-cdn.alpinelinux.org/alpina/v3.10/main/ > /mnt/etc/apk/repositories
    ```
7. Enter chroot
    ```
    chroot /mnt /bin/sh
    ```
8. Add appropiate packages
    ```
    apk update
    apk add blkid busybox-initscripts \
        chrony curl \
        dhclient dosfstools \
        e2fsprogs grub-efi \
        iptables ip6tables \
        openrc openssh \
        rsyslog util-linux \
        bash linux-vanilla
    apk upgrade openssl
    ```
9. add base files
    1. image-tools
    ```
    wget https://github.com/scaleway/image-tools/archive/master.tar.gz \
        -O image-tools.tar.gz
    tar xvzf image-tools.tar.gz -C /tmp/image-tools
    cp /tmp/image-tools/bases/overlay-common/* / -r
    cp /tmp/image-tools/bases/overlay-openrc/* / -r
    ```
    2. image-alpine
    ```
    wget https://github.com/scaleway/image-alpine/archive/master.tar.gz \
        -O image-alpine.tar.gz
    tar xvzf image-alpine.tar.gz -C /tmp/image-alpine
    cp /tmp/image-alpine/latest/overlay/* / -r
    cp /tmp/image-alpine/latest/overlay-arm64/* / -r
    ```
10. configure all rc-scripts
    ```
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
    ```
11. remove network configuration so it's generated at first boot
    ```
    > /etc/network/interfaces
    ```
12. Enable IPv6
    ```
    echo "ipv6" >> /etc/modules
    ```
13. Allow login from ttyS0 and ttyAMA0
    ```
    echo -e "ttyS0\nttyAMA0\n" >> /etc/securetty
    ```
14. Fix Permissions
    ```
    chmod 0755 /etc /usr /usr/local /usr/local/bin /usr/local/sbin
    chmod 0750 /root
    ```

Source:

[Scaleway Community Forum](https://community.scaleway.com/t/alpine-linux-on-arm64/6022)

[Scaleway Github Dockerfile](https://github.com/scaleway/image-alpine/blob/master/latest/Dockerfile)