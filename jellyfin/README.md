# Jellyfin
Jellyfin is a Free Software Media System that puts you in control of managing and streaming your media.

## Proxmox iGPU Passthrough(optional)
nano /etc/default/grub
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on i915.enable_gvt=1"
### Modules required for PCI passthrough
/etc/modules
vfio
vfio_iommu_type1
vfio_pci
vfio_virqfd

### Modules required for Intel GVT
kvmgt
#exngt
#vfio-mdev
root@pve:~# 

/etc/modprobe.d/vfio.conf
#options i915 enable_gvt=1 fastboot=1 enable_guc=0
-> Nicht gebraucht