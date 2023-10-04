% VHOST-DEVICE-SCMI(1) Version 0.1.0 | rust-vmm/vhost-device

NAME
====

**vhost-device-scmi** — vhost-user backend for a VirtIO SCMI device

SYNOPSIS
========

| **vhost-device-scmi** **-s**|**\-\-socket-path** _path_ \[**-d**|**\-\-device** _spec_]
| **vhost-device-scmi** \[**-h**|**\-\-help**]

DESCRIPTION
===========

This program is a vhost-user backend for a VirtIO SCMI device.
It provides SCMI access to various entities on the host; not
necessarily only those providing an SCMI interface themselves.

It is tested with QEMU's `-device vhost-user-scmi-pci` but should work
with any virtual machine monitor (VMM) that supports vhost-user. See
*EXAMPLES* section below.

Options
-------

-h, \-\-help

:   Print help.

-s, \-\-socket-path=PATH

:   Location of the vhost-user Unix domain sockets.

-d, \-\-device=SPEC

:   SCMI device specification in the format `ID,PROPERTY=VALUE,...`.
    For example: `-d iio,path=/sys/bus/iio/devices/iio:device0,channel=in_accel`.
    Can be used multiple times for multiple exposed devices.
    If no device is specified then no device will be provided to the
    guest OS but VirtIO SCMI will be still available there.

\-\-help-devices

:   List help on all the available devices.

EXAMPLES
========

The daemon should be started first:

```
host# vhost-device-scmi --socket-path=scmi.sock --device fake,name=foo
```

The QEMU invocation needs to create a chardev socket the device can
use to communicate as well as share the guests memory over a memfd:

```
host# qemu-system \
   -chardev socket,path=scmi.sock,id=scmi \
   -device vhost-user-scmi-pci,chardev=vscmi,id=scmi \
   -machine YOUR-MACHINE-OPTIONS,memory-backend=mem \
   -m 4096 \
   -object memory-backend-file,id=mem,size=4G,mem-path=/dev/shm,share=on \
   ...
```

ENVIRONMENT
===========

**RUST_LOG**

:   Logging level. Set to `debug` for maximum output.

BUGS
====

See GitHub Issues: <https://github.com/rust-vmm/vhost-device/issues>

AUTHOR
======

Milan Zamazal <mzamazal@redhat.com>

SEE ALSO
========

**qemu(1)**
