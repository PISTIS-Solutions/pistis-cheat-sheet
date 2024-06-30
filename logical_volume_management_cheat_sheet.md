# LINUX - LOGICAL VOLUME MANAGER (LVM) CHEATSHEET
Linux Logical Volume Manager commands for managing storage on a Linux system.

<br />

### LVM SCHEMA
[LVM_schema](https://media.cheatography.com/uploads/leszekt_1669906975_01-linux-lvm-logical-volume-manager.jpg)

Example of an LVM layout

<br />

### LVM - termin­ology
```markdown
#PE - physical extents
The smallest unit of disk space that can be managed by LVM. It's set when you create a volume group. It determines the "­gra­nul­ari­ty" of of disk space alloca­tio­n. All physical volumes in a volume group will use the same extent size.
#LE - logical extents
The same as PE but for Logical Volumes
#PV - physical volume
Disks, partit­ions, RAID volumes
#VG - volume group
Group of one or more physical volumes
#LV - logical volume
Entity that contains inform­ation, store on physical volumes, grouped within a volume group
```

### LVM - commands and components
| | |
| ---------- | ---------- |
**lvm** | pseudo shell for LVM |
**lvmconfig** | prints LVM config­uration from /etc/l­vm/­lvm.conf
**lvmdis­kscan** | prints devices that could be used as physical volumes
**lvmdump** | dumps LVM config­uration to tar file
**lvmetad** | caching service for LVM metadata
<br />

### LVM - important files
| | |
| ---------- | ---------- |
**/etc/lvm/** | LVM config­uration directory
**/etc/l­vm/­lvm.conf** | LVM config­uration file
**/etc/l­vm/­{ar­chi­ve|­backup}** | Backup and archive of LVM config­uration
**/etc/l­vm/­profile** | A set of selected custom­izable config­uration settings that can be used to achieve certain charac­ter­istics in various enviro­nments or uses. Normally, the name of the profile should reflect that enviro­nment or use. An LVM profile overrides existing config­ura­tion.
<br />

### LVM - Physical Volume
| | |
| ---------- | ---------- |
**pvcreate** | create PV
**pvchange** | change attributes of PV
**pvs&#124;pv­display** | display inform­ation about PV
**pvmove** | moves extents from one PV to another
**pvremove** | removes a PV
**pvresize** | resizes a PV
**pvscan** | scans for changes in PV config­uration and size
<br />

### LVM - Volume Group
| | |
| ---------- | ---------- |
| **vgs&#124;vg­display** | displays VG inform­ation
| **vgmknodes** | create the special files for VG devices in /dev
**vgck** | check VG consis­tency
**vgcfgb­ackup** | make a backup of VG metadata 
**vgcfgr­estore** | restore VG metadata from backup
**vgrename** | rename a VG
**vgsplit** | move PVs to a new or existing VG
**vgconvert** | change VG metadata format
**vgimport** | register exported VG in the system
**vgexport** | unregister VG from the system
**vgimpo­rtclone** | import a VG from cloned PVs
**vgcreate** | create VG from one or more PVs
**vgremove** | remove VG
**vgreduce** | remove PVs from VG
**vgchange** | change VG attributes
**vgextend** | extend VG with one or more PVs
**vgmerge** | merge VGs
**vgscan** | scan VGs for changes in metadata and size
<br />

### LVM - Logical Volume
| | |
| ---------- | ---------- |
**lvs&#124;lv­display** | print LV metadata
**lvchange** | change attributes of LV
**lvcreate** | create a new LV
**lvextend** | extend size of LV
**lvreduce** | reduce size of LV (offline!)
**lvresize** | change size of LV
**lvrename** | rename a LV
**lvconvert** | change layout of LVM
**lvscan** | scan LVs for metadata changes and size
**lvremove** | remove LV
<br />

### LVM - create PV
| | |
| ---------- | ---------- |
**pvcreate /dev/<­dis­k_d­evi­ce>** | create a new PV from device
```markdown
pvcreate /dev/sdb
```
To create a PV you need a usable storage device.
Try **lvmdis­kscan** command.

<br />

### LVM - create VG
| | |
| ---------- | ---------- |
**vgcreate `<VG> <PV> <PV>`** | create a volume groups that consists of one or more PVs
```markdown
vgcreate data_vg /dev/sdb /dev/sdc
```
To create a VG you need one or more PVs.

<br />

### LVM - create LV
| | |
| ---------- | ---------- |
**lvcreate -n `<LV­_NA­ME> -L <SI­ZE> <VG>`** | create a LV of a given size in a VG
```markdown
lvcreate -n data_lv -L 100G data_vg
```
| | |
| ---------- | ---------- |
**lvcreate -n <LV­_NA­ME> -l 100%FREE `<VG>`** | create a LV that fills 100% of free space in VG
```markdown
lvcreate -n data_lv -l 100%FREE data_vg
```
To create an LV you need a volume group.

<br />

### LVM - Snapshots
| | |
| ---------- | ---------- |
**lvcreate -L <SI­ZE> -s -n <NA­ME_­OF_­SNA­PSH­OT> <PA­TH_­TO_­LV>** | Create a snapshot of an LV
```markdown
lvcreate -L 4G -s -n data_l­v-s­napshot /dev/m­­­a­p­p­­e­­r/­­­da­t­­­a-­­-­v­­g_­­­d­at­­­a--lv
```
| | |
| ---------- | ---------- |
**lvremove <PA­TH_­TO_­SNA­PSH­OT>** | Remove snapshot
```markdown
lvremove /dev/m­­­a­p­p­­e­­r/­­­da­t­­­a-­­-­v­­g_­­­d­at­­­a--lv
```
| | |
| ---------- | ---------- |
**lvextend -L <SI­ZE> <PA­TH_­TO_­LV>** | Extend snapshot
```markdown
lvextend -L +10G /dev/m­­­a­p­p­­e­­r/­­­da­t­­­a-­­-­v­­g_­­­d­at­­­a--lv
```
| | |
| ---------- | ---------- |
**lvconvert --merge <PA­TH_­TO_­SNA­PSH­OT>** | Restore data from snapshot
```markdown
lvconvert --merge /dev/m­­­a­p­p­­e­­r/­­­da­t­­­a-­­-­v­­g_­­­d­at­­­a--lv
```
| | |
| ---------- | ---------- |
modify **snapsh­ot_­aut­oex­ten­d_t­reshold and snapsh­ot_­aut­oex­ten­d_p­ercent** in lvm.conf | Enable automatic extension of snapshots by adjusting the values

Snapshots contain differ­ences from the point a given LV has been created - not the real data.
If the size of a snapshot is exceeded it becomes useless and there is no way to restore data from it.
Old state of an LV can be restored from a snapshot, but please remember to unmount the filesystem first.

<br />

### Useful storage commands (Bonus)
| | |
| ---------- | ---------- |
**lsblk -o name,m­oun­tpo­int­,la­bel­,si­ze,uuid** | List block devices with useful inform­ation
**multipathd show maps status** | Print path status of multipath devices
**lvs -o +devices** | Print LVs, VGs and device paths
**vgs -o +lv_si­ze,­lv_name** | Print inform­ation about LVs, VGs, sizes and attributes
**mkfs.ext4 `<FS>`** | Format a filesystem for EXT4
**mkfs.xfs `<FS>`** | Format a filesystem for XFS
**mount <PA­TH_­TO_­LV> <MO­UNT­POI­NT>** | Mount a filesystem in a given location
**mount -a** | Mount all filesy­stems listed in /etc/fstab

Useful in many situations when you need to manipulate storage devices and layout.

<br />

### LVM - extend PV
| | |
| ---------- | ---------- |
**rescan­-sc­si-­bus.sh­&#124;echo 1 > /sys/b­loc­k/<­DEV­ICE­>/d­evi­ce/­rescan** | Rescan underlying storage to detect change in disk size
```markdown
rescan­-sc­si-­bus.sh­|echo 1 > /sys/b­loc­k/s­db/­dev­ice­/rescan
```
| | |
| ---------- | ---------- |
**partprobe** | Detect changes in partition size (if necessary)
**pvresize `<PV>`** | Resize PV to the maximum possible size of partition or disk/LUN
```markdown
pvresize /dev/sdb
```
---
To resize a PV you'll need to know the underlying storage and know how to rescan its size.
All steps can be performed online.

<br />

### LVM - Extend VG
| | |
| ---------- | ---------- |
**vgextend `<VG> <PV> <PV>`** | Extend existing VG with one or more PVs
```markdown
vgextend data_vg /dev/sdb /dev/sdc
```
To extend a VG you need a VG and one or more PVs that are not assigned to any PVs yet.

<br />

### LVM - extend LV
| | |
| ---------- | ---------- |
**lvextend -L <SI­ZE> /dev/m­app­er<­PAT­H_T­O_L­V>** | extend logical volume by given size (add 10GB to existing size)
```markdown
lvextend -L +10G /dev/m­app­er/­dat­a--­vg_­dat­a--lv
```
| | |
| ---------- | ---------- |
**lvextend -r -L <SI­ZE> /dev/m­app­er<­PAT­H_T­O_L­V>** | extend logical volume and its filesystem by given size (add 10GB to existing size)
```markdown
lvextend -r -L +10G /dev/m­app­er/­dat­a--­vg_­dat­a--lv
```
To extend an LV you need its path. Use `df` command.
In most cases you'll also want to extend the underlying filesy­stem, so use `-r` option to do it.

<br />

### Extend filesystem (bonus)
| | |
| ---------- | ---------- |
**umount `<FS>`** | Unmount filesystem
```markdown
umount /data
```
| | |
| ---------- | ---------- |
**e2fsck -f <PA­TH_­TO_­LV>** | Check and fix potential errors
```markdown
e2fsck -f /dev/m­­ap­p­e­r/­­dat­­a-­-­v­g_­­dat­­a--lv
```
| | |
| ---------- | ---------- |
**resize2fs <PA­TH_­TO_­LV> <SI­ZE>** | Reduce size of filesystem
```markdown
resize2fs /dev/m­­ap­p­e­r/­­dat­­a-­-­v­g_­­dat­­a--lv 10G
```
| | |
| ---------- | ---------- |
**lvreduce -L <SI­ZE> <PA­TH_­TO_­LV>** | Reduce size of LV
```markdown
lvreduce -L 10G /dev/m­­ap­p­e­r/­­dat­­a-­-­v­g_­­dat­­a--lv
```
| | |
| ---------- | ---------- |
**e2fsck -f <PA­TH_­TO_­LV>** | Check for errors once more
```markdown
e2fsck -f /dev/m­­ap­p­e­r/­­dat­­a-­-­v­g_­­dat­­a--lv
```
| | |
| ---------- | ---------- |
**mount `<FS>`** | Mount filesystem
```markdown
mount /data
```
Remember to make sure the size of both: FS (files­ystem) and LV (logical volume) are the same and there are no errors. Reducing the size can ONLY be done OFFLINE. The filesystem must be unmounted. Not all filesy­stems can be reduced at 