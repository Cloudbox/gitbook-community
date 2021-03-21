So I have a server with 2x3TB and a 480SSD. The SSD was added well after my original Cloudbox install. So when I wiped it and re-installed Ubuntu, it partitioned the SSD into 2 partitions. The goal of this guide is to get rid of those 2 partitions, and have it as 1 partition as btrfs, and mounted.

    lsblk
    NAME    MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
    sdb       8:16   0   2.7T  0 disk
    ├─sdb2    8:18   0   2.7T  0 part
    │ └─md1   9:1    0   5.5T  0 raid0 /
    ├─sdb3    8:19   0     1M  0 part
    └─sdb1    8:17   0   512M  0 part
      └─md0   9:0    0 511.4M  0 raid1 /boot
    sdc       8:32   0 447.1G  0 disk         <----there are 2 partitions, the goal is to remove the 2 and have just 1
    ├─sdc2    8:34   0 446.6G  0 part
    └─sdc1    8:33   0   512M  0 part
    sda       8:0    0   2.7T  0 disk
    ├─sda2    8:2    0   2.7T  0 part
    │ └─md1   9:1    0   5.5T  0 raid0 /
    ├─sda3    8:3    0     1M  0 part
    └─sda1    8:1    0   512M  0 part
      └─md0   9:0    0 511.4M  0 raid1 /boot     

 
    fdisk /dev/sdc

    Welcome to fdisk (util-linux 2.27.1).
    Changes will remain in memory only, until you decide to write them.
    Be careful before using the write command.


    Command (m for help): d
    Partition number (1,2, default 2): 1

    Partition 1 has been deleted.

    Command (m for help): d
    Selected partition 2
    Partition 2 has been deleted.    <-------I did 1 and 2 since I had 2 partitions on it
  
    w for write changes and exit
  
    lsblk
    NAME    MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
    sdb       8:16   0   2.7T  0 disk
    ├─sdb2    8:18   0   2.7T  0 part
    │ └─md1   9:1    0   5.5T  0 raid0 /
    ├─sdb3    8:19   0     1M  0 part
    └─sdb1    8:17   0   512M  0 part
      └─md0   9:0    0 511.4M  0 raid1 /boot
    sdc       8:32   0 447.1G  0 disk   <------notice there are no partitions on this drive
    sda       8:0    0   2.7T  0 disk
    ├─sda2    8:2    0   2.7T  0 part
    │ └─md1   9:1    0   5.5T  0 raid0 /
    ├─sda3    8:3    0     1M  0 part
    └─sda1    8:1    0   512M  0 part
      └─md0   9:0    0 511.4M  0 raid1 /boot

    sudo apt-get install parted
  
    sudo parted /dev/sdc mklabel gpt
    Warning: The existing disk label on /dev/sdc will be destroyed and all data on this disk will be lost. Do you want to
    continue?
    Yes/No? yes
    Information: You may need to update /etc/fstab.

    sudo parted -a opt /dev/sdc mkpart primary btrfs 0% 100%
    Information: You may need to update /etc/fstab.


    lsblk
    NAME    MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
    sdb       8:16   0   2.7T  0 disk
    ├─sdb2    8:18   0   2.7T  0 part
    │ └─md1   9:1    0   5.5T  0 raid0 /
    ├─sdb3    8:19   0     1M  0 part
    └─sdb1    8:17   0   512M  0 part
      └─md0   9:0    0 511.4M  0 raid1 /boot
    sdc       8:32   0 447.1G  0 disk
    └─sdc1    8:33   0 447.1G  0 part     <----notice we have a partition that uses all the space
    sda       8:0    0   2.7T  0 disk
    ├─sda2    8:2    0   2.7T  0 part
    │ └─md1   9:1    0   5.5T  0 raid0 /
    ├─sda3    8:3    0     1M  0 part
    └─sda1    8:1    0   512M  0 part
      └─md0   9:0    0 511.4M  0 raid1 /boot
  
  
    sudo mkfs.btrfs -f -L ssd /dev/sdc1   <------where it says ssd, you can label it what you want. 
    btrfs-progs v4.4
    See http://btrfs.wiki.kernel.org for more information.

    Detected a SSD, turning off metadata duplication.  Mkfs with -m dup if you want to force metadata duplication.
    Performing full device TRIM (447.13GiB) ...
    Label:              ssd
    UUID:               25752801-2f27-47b9-93c8-b1fef9c58655
    Node size:          16384
    Sector size:        4096
    Filesystem size:    447.13GiB
    Block group profiles:
      Data:             single            8.00MiB
      Metadata:         single            8.00MiB
      System:           single            4.00MiB
    SSD detected:       yes
    Incompat features:  extref, skinny-metadata
    Number of devices:  1
    Devices:
       ID        SIZE  PATH
        1   447.13GiB  /dev/sdc1


    sudo lsblk --fs
    NAME    FSTYPE            LABEL    UUID                                 MOUNTPOINT
    sdb
    ├─sdb2  linux_raid_member rescue:1 e0a13d17-c2fb-809f-f4ad-a9362aa21a3f
    │ └─md1 btrfs                      2914349d-42ec-44d1-bcbf-1f9bd5a4744d /
    ├─sdb3
    └─sdb1  linux_raid_member rescue:0 527278e1-eec4-d202-9d2a-fcf3f70ea2be
      └─md0 ext4                       4eefbaac-894a-4f86-8d2d-b3396fea0e40 /boot
    sdc
    └─sdc1  btrfs             ssd      25752801-2f27-47b9-93c8-b1fef9c58655
    sda
    ├─sda2  linux_raid_member rescue:1 e0a13d17-c2fb-809f-f4ad-a9362aa21a3f
    │ └─md1 btrfs                      2914349d-42ec-44d1-bcbf-1f9bd5a4744d /
    ├─sda3
    └─sda1  linux_raid_member rescue:0 527278e1-eec4-d202-9d2a-fcf3f70ea2be
      └─md0 ext4                       4eefbaac-894a-4f86-8d2d-b3396fea0e40 /boot
  
    sudo mkdir -p /mnt/ssd     <----change the /mnt/ssd to however you want to reference the new drive
  
     sudo nano /etc/fstab
 

inside here, put in 

    /dev/sdc1 /mnt/ssd btrfs defaults 0 2   <---change /mnt/ssd to however you referenced it in the mkdir -p command
 CTRL-X      Y
 
     sudo mount -a     <-----you shouldnt get any errors here. If so, double check your fstab.
 
 
    df -h -x tmpfs -x devtmpfs
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/md1        5.5T  1.5G  5.5T   1% /
    /dev/md0        488M   72M  387M  16% /boot
    /dev/sdc1       448G   17M  447G   1% /mnt/ssd        <-----there is out newly added drive/partition

