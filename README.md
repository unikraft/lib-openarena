# OpenArena for Unikraft
This is the port of OpenArena for Unikraft as external library.

## Build
OpenArena depends on the following extern libraries, that need to
be added to `Makefile`:

* `libc`, e.g. `musl`
* compression library, e.g. `libzlib`
* network stack, e.g. `lwip`

Before you proceed to writing your own application, you can use the `main()`
function provided in the Nginx glue code by enabling it in its configuration
menu.

## Root filesystem
### Creating the filesystem
OpenArena needs a filesystem which should contain its configuration files for the server, along with textures files. Therefore, the filesystem needs to be created before
running the VM. You can find an example in the `catalog-core` entry dedicated to OpenArena.

### Using the filesystem
Mounting the filesystem is a transparent operation. All you have to do
is to provide the right Qemu parameters in order for Unikraft to mount
the filesystem.  We will use the cpio support for filesystems and for
this you will need to use the following parameters:

```bash
-initrd initrd.cpio \
-append "vfs.fstab=[\"initrd0:/:extract::ramfs=1:\"]"
```

To enable cpio, you'll need to select the following `Config.uk` entries:

```bash
select LIBUKCPIO
select LIBDEVFS
select LIBDEVFS_AUTOMOUNT
select LIBDEVFS_DEVSTDOUT
select LIBVFSCORE
select LIBVFSCORE_AUTOMOUNT_UP
```

## Further information
Please refer to the `README.md` as well as the documentation in the `docs/`
subdirectory of the main unikraft repository.
