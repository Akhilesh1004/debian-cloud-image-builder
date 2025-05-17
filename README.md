# debian-cloud-image-builder
Use Debian/Ubuntu local or VM(ubunut recommand use 22.04 version)

Install required tools
```
apt update
apt install libguestfs-tools -y
```

Fetch Official Debian Cloud image(if needed)
```
wget https://cloud.debian.org/images/cloud/bookworm/latest/debian-12-genericcloud-amd64.qcow2
```

Convert To raw format(Optional)
```
apt install qemu-utils
qemu-img convert -O raw debian-12-generic-amd64-daily-20250504-2102.qcow2 debian-12-cloud.raw
```

customize image
```
virt-customize -a debian-12-genericcloud-amd64.qcow2 \
  --install qemu-guest-agent,sudo,vim,nano,btop,mtr \
  --run-command "apt-get -y autoremove --purge && apt-get -y clean" \
  --run-command 'truncate -s 0 /etc/machine-id' \
  --run-command 'rm -f /var/lib/dbus/machine-id'
```
