# ws215i

## mmc size

+ 7733248 blocks
+ 3959422976 bytes

```
$ udevadm info -a /dev/mmcblk0

Udevadm info starts with the device specified by the devpath and then
walks up the chain of parent devices. It prints for every device
found, all possible attributes in the udev rules key format.
A rule to match, can be composed by the attributes of the device
and the attributes from one single parent device.

  looking at device '/devices/pci0000:00/0000:00:01.0/0000:01:1b.0/mmc_host/mmc0/mmc0:0001/block/mmcblk0':
    KERNEL=="mmcblk0"
    SUBSYSTEM=="block"
    DRIVER==""
    ATTR{alignment_offset}=="0"
    ATTR{capability}=="10"
    ATTR{discard_alignment}=="0"
    ATTR{ext_range}=="8"
    ATTR{force_ro}=="0"
    ATTR{inflight}=="       0        0"
    ATTR{range}=="8"
    ATTR{removable}=="0"
    ATTR{ro}=="0"
    ATTR{size}=="7733248"
    ATTR{stat}=="    8535     5044   556954    32000    11294    32061   346760    74104        0    47080   106072"

  looking at parent device '/devices/pci0000:00/0000:00:01.0/0000:01:1b.0/mmc_host/mmc0/mmc0:0001':
    KERNELS=="mmc0:0001"
    SUBSYSTEMS=="mmc"
    DRIVERS=="mmcblk"
    ATTRS{cid}=="45010053454d3034473a2a40cb9aa200"
    ATTRS{csd}=="d00f00320f5903fffffffdff8a404000"
    ATTRS{date}=="10/2015"
    ATTRS{enhanced_area_offset}=="18446744073709551594"
    ATTRS{enhanced_area_size}=="4294967274"
    ATTRS{erase_size}=="262144"
    ATTRS{ffu_capable}=="0"
    ATTRS{fwrev}=="0x0"
    ATTRS{hwrev}=="0x0"
    ATTRS{manfid}=="0x000045"
    ATTRS{name}=="SEM04G"
    ATTRS{oemid}=="0x0100"
    ATTRS{preferred_erase_size}=="2097152"
    ATTRS{prv}=="0x3a"
    ATTRS{raw_rpmb_size_mult}=="0x10"
    ATTRS{rel_sectors}=="0x1"
    ATTRS{serial}=="0x2a40cb9a"
    ATTRS{type}=="MMC"

  looking at parent device '/devices/pci0000:00/0000:00:01.0/0000:01:1b.0/mmc_host/mmc0':
    KERNELS=="mmc0"
    SUBSYSTEMS=="mmc_host"
    DRIVERS==""

  looking at parent device '/devices/pci0000:00/0000:00:01.0/0000:01:1b.0':
    KERNELS=="0000:01:1b.0"
    SUBSYSTEMS=="pci"
    DRIVERS=="sdhci-pci"
    ATTRS{broken_parity_status}=="0"
    ATTRS{class}=="0x080501"
    ATTRS{consistent_dma_mask_bits}=="32"
    ATTRS{d3cold_allowed}=="0"
    ATTRS{device}=="0x070b"
    ATTRS{dma_mask_bits}=="32"
    ATTRS{driver_override}=="(null)"
    ATTRS{enable}=="1"
    ATTRS{irq}=="32"
    ATTRS{local_cpulist}=="0-3"
    ATTRS{local_cpus}=="f"
    ATTRS{msi_bus}=="1"
    ATTRS{numa_node}=="-1"
    ATTRS{subsystem_device}=="0x0000"
    ATTRS{subsystem_vendor}=="0x0000"
    ATTRS{vendor}=="0x8086"

  looking at parent device '/devices/pci0000:00/0000:00:01.0':
    KERNELS=="0000:00:01.0"
    SUBSYSTEMS=="pci"
    DRIVERS==""
    ATTRS{broken_parity_status}=="0"
    ATTRS{class}=="0x060401"
    ATTRS{consistent_dma_mask_bits}=="32"
    ATTRS{d3cold_allowed}=="0"
    ATTRS{device}=="0x0700"
    ATTRS{dma_mask_bits}=="32"
    ATTRS{driver_override}=="(null)"
    ATTRS{enable}=="1"
    ATTRS{irq}=="0"
    ATTRS{local_cpulist}=="0-3"
    ATTRS{local_cpus}=="f"
    ATTRS{msi_bus}=="1"
    ATTRS{numa_node}=="-1"
    ATTRS{subsystem_device}=="0x0000"
    ATTRS{subsystem_vendor}=="0x0000"
    ATTRS{vendor}=="0x8086"

  looking at parent device '/devices/pci0000:00':
    KERNELS=="pci0000:00"
    SUBSYSTEMS==""
    DRIVERS==""
```
## kernel build (barcelona-4.3.3)

```
sudo apt-get install build-essential linux-source kernel-package libncurses5-dev fakeroot
cd barcelona-4.3.3
make -j16
make-kpkg --rootcmd=fakeroot --initrd --jobs=8 --append-to-version=.001 --revision=001 kernel_image kernel_headers
```
## post install

```
. /lib/chroot-setup.sh
chroot_setup
chroot /target /overlay/post_install
chroot_cleanup
```
