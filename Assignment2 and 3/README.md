# Assignment 2
### Set up the environment:
#### 1.First thing is to build the kernel and before starting the process of building make sure the environment is setup with all the required packages installed.
- - use this link https://askubuntu.com/questions/718381/how-to-compile-and-install-custom-mainline-kernel
- - Next is to run few commands to build the kernel
- - - sudo make -j 6 modules
- - - sudo make -j 6
- - - sudo make modules_install && sudo make install
#### 2. Now the Kernel is build. Reboot the machine using sudo reboot
#### 3. Now we have to make changes to the cpuid.c and vmx.c file, and add code to report data for the leaf nodes we have 

	``` if(eax==0x4fffffff){
		eax=atomic64_read(&exit_counters);
		printk("eax is 0x4fffffff \n Total exits eax=%u",eax); 
	}
	else if(eax==0x4ffffffe){
		//kvm_cpuid(vcpu, &eax, &ebx, &ecx, &edx, true);
				
		ebx = ((atomic64_read(&exit_duration)>>32) & 0xfffffffe );
		printk("eax = 0x4FFFFFFE \n Total time spent processing all exits in ebx[high 32 bits] = %u", ebx);
			
		ecx = (atomic64_read(&exit_duration) & 0xfffffffe);
		printk("eax = 0x4ffffffe \n Total time spent processing all exits in ecx[low 32 bits] = %u", ecx);
		
		printk("eax = 0x4ffffffe \n Total Cycles spent in exit = %llu", atomic64_read(&exit_duration));
	
	}```
- - - The above code is for 0xffffffe and oxfffffff. Build the kernel again.

#### 4. Now we need to install virtual manager and for that we need to install kvm and virt-manager
- - - Use this link to follow steps needed: https://help.ubuntu.com/community/KVM/Installation
- - - Now install virt manager using `sudo apt-get install virt-manager`
- - - Use the link for more details https://help.ubuntu.com/community/KVM/VirtManager
#### 5. Now to check the output, we need a nested vm which we have created in the previous step. Install cpuid package and the test can be done using this package.
#### Screenshots of the outputs


# Assignment 3
