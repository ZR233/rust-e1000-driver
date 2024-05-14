KDIR ?= /lib/modules/`uname -r`/build
FS ?= initrd.img
ROOTFS ?= /home/zhourui/rootfs-debian
MNT = /mnt/rootfs
INSTALL_PATH ?= /home/zhourui/rootfs-debian

default:
	$(MAKE) LLVM=1  -C $(KDIR) M=$$PWD

install:
	$(MAKE) LLVM=1  -C $(KDIR) M=$$PWD INSTALL_MOD_PATH=$(INSTALL_PATH) modules_install

clean:
	$(MAKE) LLVM=1  -C $(KDIR) M=$$PWD clean

qemu: 
	sudo qemu-system-x86_64 -smp 2 -m 2G \
  		-kernel "$(KDIR)/arch/x86_64/boot/bzImage" \
  		-hda initrd.img \
  		-nographic -vga none \
		-append "root=/dev/sda console=ttyS0" -nographic \
		-no-reboot \
		-nic tap,id=net0,ifname=tap0,script=no,downscript=no
		-device e1000, netdev=net0,mac=52:54:00:12:34:56
		# -no-reboot -nic tap 

rootfs:
	rm $(FS)
	mkdir -p $(MNT)
	dd if=/dev/zero of=$(FS) bs=1M count=1524
	mkfs.ext4 $(FS)
	sudo mount -t ext4 $(FS) $(MNT)
	sudo cp -raf $(ROOTFS)/* $(MNT)
	sudo umount $(MNT)
	sudo chmod 777 $(FS)



qemu2: 
	sudo qemu-system-x86_64 -smp 2 -m 2G \
  		-kernel "/home/zhourui/Documents/e1000/e1000-origin/bzImage" \
  		-hda initrd.img \
  		-nographic -vga none \
		-append "root=/dev/sda console=ttyS0" -nographic \
		-no-reboot \
		-nic tap,id=net0,ifname=tap0,script=no,downscript=no
		-device e1000, netdev=net0,mac=52:54:00:12:34:56