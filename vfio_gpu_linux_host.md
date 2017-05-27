* check if your CPU supports VT-d http://ark.intel.com
* modify GRUB cnfig

```
the GRUB_CMDLINE_LINUX line and within the quotes add either intel_iommu=on or amd_iommu=on, depending on whether your platform is Intel or AMD.  You may also want to add the option iommu=pt, which sets the IOMMU into passthrough mode for host devices.  This reduces the overhead of the IOMMU for host owned devices, but also removes any protection the IOMMU may have provided again errant DMA from devices.  If you weren't using the IOMMU before, there's nothing lost.  Regardless of passthrough mode, the IOMMU will provide the same degree of isolation for assigned devices.
```

http://vfio.blogspot.com/2015/05/vfio-gpu-how-to-series-part-1-hardware.html
https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF
https://symless.com/synergy
https://www.se7ensins.com/forums/threads/how-to-setup-a-gaming-virtual-machine-with-gpu-passthrough-qemu-kvm-libvirt-and-vfio.1371980/
