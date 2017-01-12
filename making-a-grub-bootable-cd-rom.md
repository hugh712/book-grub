GRUB也可以直接由CD-ROM或是USB上驅動，




```
root@hugh-VirtualBox:/home/hugh# apt-get install xorriso

root@hugh-VirtualBox:/home/hugh# mkdir -p iso/boot/grub

root@hugh-VirtualBox:/home/hugh# cp /boot/grub/grub.cfg iso/boot/grub/


root@hugh-VirtualBox:/home/hugh# grub-mkrescue -o grub.iso iso
xorriso 1.4.2 : RockRidge filesystem manipulator, libburnia project.

Drive current: -outdev 'stdio:grub.iso'
Media current: stdio file, overwriteable
Media status : is blank
Media summary: 0 sessions, 0 data blocks, 0 data, 9512m free
Added to ISO image: directory '/'='/tmp/grub.HVxC3C'
xorriso : UPDATE : 281 files added in 1 seconds
Added to ISO image: directory '/'='/home/hugh/iso'
xorriso : UPDATE : 284 files added in 1 seconds
xorriso : NOTE : Copying to System Area: 512 bytes from file '/usr/lib/grub/i386-pc/boot_hybrid.img'
ISO image produced: 2540 sectors
Written to medium : 2540 sectors at LBA 0
Writing to 'stdio:grub.iso' completed successfully.
```


