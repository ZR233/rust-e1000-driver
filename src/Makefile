KDIR ?= /lib/modules/`uname -r`/build
FS ?= initrd.img
ROOTFS ?= /home/zhourui/rootfs-ubuntu
MNT = /mnt/rootfs
INSTALL_PATH ?= /home/zhourui/rootfs-ubuntu

default:
	$(MAKE) LLVM=1  -C $(KDIR) M=$$PWD

install:
	$(MAKE) LLVM=1  -C $(KDIR) M=$$PWD INSTALL_MOD_PATH=$(INSTALL_PATH) modules_install

clean:
	$(MAKE) LLVM=1  -C $(KDIR) M=$$PWD clean

qemu: 
	qemu-system-x86_64 -smp 2 -m 2G \
  		-kernel "$(KDIR)/arch/x86_64/boot/bzImage" \
  		-hda initrd.img \
  		-nographic -vga none \
		-append "root=/dev/sda console=ttyS0" -nographic \
  		-no-reboot

rootfs:
	mkdir -p $(MNT)
	dd if=/dev/zero of=$(FS) bs=1M count=1024
	mkfs.ext4 $(FS)
	sudo mount -t ext4 $(FS) $(MNT)
	cp -raf $(ROOTFS)/* $(MNT)
	sudo umount $(MNT)
	sudo chmod 777 $(FS)