1. _grub>_ prompt: GRUB 2 loaded modules but was unable to find the grub.cfg file.
    
2. _grub rescue>_ prompt: GRUB 2 failed to find its _grub_ folder, or failed to load the _normal_ module.
    
3.   [grub>:]() - The _grub_ prompt on a blank screen
	
		- GRUB 2 has found the boot information but has been either unable to locate or unable to use an existing GRUB 2 configuration file (usually _grub.cfg_).
     
4.   [grub rescue>:]() - The rescue mode.
	
		- GRUB 2 is unable to find the _grub_ folder or its contents are missing/corrupted. The _grub_ folder contains the GRUB 2 menu, modules and stored environmental data.
	
5.   [GRUB]() - a single word at the top left of the screen, with no prompt and no cursor.
	  
		- GRUB has failed to find even the most basic information, usually contained in the MBR or boot sector.
	
6.   _Busybox_ or _Initramfs_: 
	
		- GRUB 2 began the boot process but there was a problem passing control to the operating system. Possible causes include an incorrect UUID or _root=_ designation in the 'linux' line or a corrupted kernel.
    
7.    _Frozen_ splash screen, blinking cursor with no _grub>_ or _grub rescue_ prompt. 
	   Possible video issues with the kernel. While these failures are not of GRUB 2's making, it may still be able to help. GRUB 2 allows pre-boot editing of its menu and the user may restore functionality by adding and/or removing kernel options in a _menuentry_ before booting.