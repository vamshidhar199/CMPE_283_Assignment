# Assignment 2 and 3
- - NOTE: Please use sudo before make command if you face permission errors. To avoid such issues we can add sudo to makes sure everything works fine.
- - This Readme contains details for both Assignment 2 and 3.
- - **Assignment 2** https://github.com/vamshidhar199/CMPE_283_Assignment/edit/master/Assignment2%20and%203/README.md#assignment-2
- - **Assignment 3** https://github.com/vamshidhar199/CMPE_283_Assignment/edit/master/Assignment2%20and%203/README.md#assignment-3
#  Assignment 2:
## Steps to run the assignment
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
				
		ebx = ((atomic64_read(&exit_duration)>>32)  );
		printk("eax = 0x4FFFFFFE \n Total time spent processing all exits in ebx[high 32 bits] = %u", ebx);
			
		ecx = (atomic64_read(&exit_duration) & 0xffffffff);
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

![alt text](https://github.com/vamshidhar199/CMPE_283_Assignment/blob/master/Assignment2%20and%203/assignment2-output.jpg)
#
#
#
#
# Assignment 3
## Steps for assignment 3
### Please follow the similar steps as above in Assignment 2. Now we have to add code for leafs 0xffffffd and 0xffffffc. And compile the kernel with the same commands as above.
#### Screenshots:
![alt text](https://github.com/vamshidhar199/CMPE_283_Assignment/blob/master/Assignment2%20and%203/cpuidExits.jpg)
![alt text](https://github.com/vamshidhar199/CMPE_283_Assignment/blob/master/Assignment2%20and%203/Output2.jpg)
![alt](https://github.com/vamshidhar199/CMPE_283_Assignment/blob/master/Assignment2%20and%203/ox4ffffffcOutput1.jpg)
![alt](https://github.com/vamshidhar199/CMPE_283_Assignment/blob/master/Assignment2%20and%203/ox4ffffffcOutput2.jpg)

# Questions:
## 1.For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched.
- - I have done it alone.
## 2.Describe in detail the steps you used to complete the assignment. Consider your reader to be someone skilled in software development but otherwise unfamiliar with the assignment. Good answers to this question will be recipes that someone can follow to reproduce your development steps.
- - It is as described in detaild in the above description.
## 3.Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail?
- - Approximately 3786079. Number of exits are not stable and keeps changing. It depends on the activities performed on VM.
## 4.Of the exit types defined in the SDM, which are the most frequent? Least?
- - Exit 48:EPT Violation, Exit 1: External Interrupt, Exit 30: IO Interrupt, Exit 32:WRMSR -> Most Frequently occuring.
- - Exit 29: MOV DR, Exit 46: Access to IDTR, Exit 55 XSETBV -> Least Frequently occuring. 
