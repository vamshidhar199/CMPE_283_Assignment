# Assignment 4
## Steps to be followed:
- - 1.You would be needing assignment 3 to be completed to be able to proceed with this assignment.
- - 2.Open the nested vm inside the vm and run the the test file to check the output of assignment 3.
- - 3.Note the output as a text file and keep it for reference.
- - 4.Next you need to shut down the vm and run below command to disable nested paging.
- - ![alt](https://github.com/vamshidhar199/VirtualizatioAssignmentVamshidhar/blob/master/Assignment4/assignment4.jpeg)
- - 5.Repeat the same steps as above and record the results.

# Questions:
## 1.For each member in your team, provide 1 paragraph detailing what parts of the lab that member implemented / researched. (You may skip this question if you are doing the lab by yourself).
- - I have done alone
## 2.Include a sample of your print of exit count output from dmesg from “with ept” and “without ept”.
- - Below screenshots include the time and number of exits for each exit number
- -![alt](https://github.com/vamshidhar199/VirtualizatioAssignmentVamshidhar/blob/master/Assignment4/a1.jpg)
- -![alt](https://github.com/vamshidhar199/VirtualizatioAssignmentVamshidhar/blob/master/Assignment4/a2.jpg)
- -![alt](https://github.com/vamshidhar199/VirtualizatioAssignmentVamshidhar/blob/master/Assignment4/a3.jpg)
- -![alt](https://github.com/vamshidhar199/VirtualizatioAssignmentVamshidhar/blob/master/Assignment4/aa1.jpg)
- -![alt](https://github.com/vamshidhar199/VirtualizatioAssignmentVamshidhar/blob/master/Assignment4/aa2.jpg)
- -![alt](https://github.com/vamshidhar199/VirtualizatioAssignmentVamshidhar/blob/master/Assignment4/aa3.jpg)
- -![alt](https://github.com/vamshidhar199/VirtualizatioAssignmentVamshidhar/blob/master/Assignment4/aa4.jpg)
- -![alt](https://github.com/vamshidhar199/VirtualizatioAssignmentVamshidhar/blob/master/Assignment4/aa5.jpg)
- -![alt](https://github.com/vamshidhar199/VirtualizatioAssignmentVamshidhar/blob/master/Assignment4/aa6.jpg)

## 3.What did you learn from the count of exits? Was the count what you expected? If not, why not?
- - The count of number of exits are more in shadow paging compared to that of the nested paging and it is expected because of following reasons.
- - Nested paging is a widely used hardware technique to virtualize memory. The processor has two page table pointers to perform a complete translation: one points to the guest page table (gptr) and the other points to the host page table(hptr). The guest page table holds gVA to gPA translation and the host page table holds gPA to hPA translations.Nested paging allows fast direct updates to both of the page tables without any VMM intervention
- - With shadow paging, the VMM creates a shadow page table by merging the guest and host tables, then holds a complete translation from gVA⇒hPA.This technique does not allow direct updates to the page tables since the shadow page table needs to be kept consistent. Every page table update requires a costly VMM intervention

## 4.What changed between the two runs (ept vs no-ept)?
- - The number of exits in shadow paging are more compared to the nested paging. The number of exits keep increasing in shadow paging.
