KDIR ?= /lib/modules/`uname -r`/build

default:
	$(MAKE) LLVM=1  -C $(KDIR) M=$$PWD

clean:
	$(MAKE) LLVM=1  -C $(KDIR) M=$$PWD clean

qemu: default
	qemu-system-x86_64 -smp 2 -m 1G \
  		-kernel "$(KDIR)/arch/x86_64/boot/bzImage" \
  		-initrd ../../initrd.img \
  		-nographic -vga none \
  		-append console=ttyS0 \
  		-no-reboot -nic tap \
  		-virtfs local,path=/home/ubuntu/git/quinn,mount_tag=quinn,security_model=none
