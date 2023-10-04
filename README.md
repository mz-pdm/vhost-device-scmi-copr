# vhost-device-scmi-copr

This is a git repository to specify
[vhost-device-scmi](https://github.com/rust-vmm/vhost-device/tree/main/crates/vhost-device-scmi)
builds for
[Copr](https://copr.fedorainfracloud.org/coprs/mzamazal/vhost-device-scmi/).

As the upstream project doesn't provide man pages, the man page for
the package binary is provided here, in the form of a
[markdown file](vhost-device-scmi.1.md).  It can be converted to a man
page as follows:
```
pandoc vhost-device-scmi.1.md -s -t man -o vhost-device-scmi.1
```
