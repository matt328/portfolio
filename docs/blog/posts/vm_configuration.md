---
date: 2023-10-01
categories:
  - k8s
---

# Virtual Machine Setup for k3s Nodes

With my homelab setup, physical machines are at a premium, as such I only have two so far. They have 8 core CPUs and decently large amounts of RAM though, making them great candidates to spin up a bunch of VMs to use for k3s nodes. This post documents how I configured each VM.

<!-- more -->

Since I have two physical machines to use for this, it made sense to me to set up an HA cluster with a k3s master node on each machine, as well as as many 2 vCPU, 3GB VMs as would reasonably fit on each to use as worker nodes. A larger constraint turns out to be disk space. Turns out I could only reasonably dedicate around 24GB for each VM. I decided to split this into 2 12GB volumes for each VM. The k8s node would use one volume for ephemeral storage, and the other for persistent volumes. The persistent volumes will be managed by Longhorn.

When creating the VMs, for the ephemeral storage, I'll just let that use the root partition of the guest OS, but will need to mount and additional virtual disk image. I used the Virtual Box UI to create the additional virtual disks, and there were a few things to be done inside the guest OS to permanently mount them. I go through the standard procedure of creating a VM and installing Ubuntu Server 23.04, using the minimal installation. There's probably more lightweight guest OS's I could use, but I am comfortable enough with it that it eliminates a large class of potential issues.

Once the OS has been installed, and the virtual disk image created and attached to the VM, ssh into the VM. First we need to prepare the mount point. I make them all the same since it makes Longhorn's configuration significantly simpler.

```bash
sudo mkdir /storage0
```

Next find where the device exists in the filesystem, in my case it was always `/dev/sdb` and format it with the ext4 filesystem.

```bash
sudo mkfs -t ext4 /dev/sdb
```

Once that's done, we need to mount it permanently, and this is done by updating `/etc/fstab`. We need to refer to the drive by its UUID, and in order to get that we run

```bash
lsblk -o NAME,FSTYPE,UUID,MOUNTPOINTS
```

Then add a line to /etc/fstab of the form:

```
UUID=<uuid from lsblk output>       /storage0       ext4    defaults        0       0
```

Instead of just yoloing changes to `etc/fstab` which, if done incorrectly, could result in things as serious as the system not booting, you can run this command to double check things.

```bash
sudo findmnt --verify
```

If there are no errors, you should `sudo reboot` to have the mount take effect. There's probalby a way without rebooting, but a reboot will make sure it works and avoid many questions later if it doesn't.

That about wraps up preparing the VM instances themselves. Now is a good time to snapshot the VM or otherwise back it up so that you can return each to this state in case something goes horribly wrong later on.
