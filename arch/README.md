Installation on Arch/Manjaro (tested only on kernel 4.19 and 5.4):

Download and unpack zip or "git clone https://github.com/misiektw/rcraid-dkms.git"

From inside "arch" directory:

  makepkg -si
  
This will compile sources and install package for current running kernel. If you need 
to make package for different kernel then you can use KVERS option.
After installing edit /etc/mkinitcpio.conf and add
  
  MODULES=(rcraid?)

then rebuild your initrd f.e.:

  mkinitcpio -p linux54

Sources for this install were forked from https://github.com/thopiekar/rcraid-dkms
I left original debian folder as im using many distros and its handy.

Note: If you just planning on switching to rcraid, my advice is: don't. 
Support from AMD for Promontory raid on Linux is pretty much non-existent. 
You will be way better off sticking with mdadm, zfs or lvm. 

If you REALLY want this to dual-boot Linux/Win, also don't. Setting up virtualization 
with KVM with GPU Passtrough today is really simple, and you will not need to 
boot Windows directly on your hardware ever again.

Sidenote: If you decide to use rcraid regardless you might want to also install RAIDXpert. 
Web interface isn't working properly on Manjaro, but rcadm is more or less is.

Sidenote2: If you ever decide to switch from rcraid to something else, you may find it useful 
to know that deleting arrays only removes metadata. Partitions are still there, and can be
recovered with gdisk, gpart etc. I found out that offset for partitions is 1069056 sectors (512B).
So if you have partition starting at usual 2048 it will be at 1071104 after array deletion.
