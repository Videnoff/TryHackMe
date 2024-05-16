Analyze the binary for the easy password  

Answer the questions below

| Question               | Answer   |
| ---------------------- | -------- |
| What is the password ? | 1337_pwd |

*Try to run the binary:*

![[Pasted image 20240510200243.png]]


*Using Ghidra:*

In Functions, click on 'main':

![[Pasted image 20240510200928.png]]


There is function 'compare_pwd'. Click on it:

![[Pasted image 20240510201014.png]]


ivarl is equal to the function my_secure_test. Analyze my_secure_test function:

![[Pasted image 20240510201446.png]]


![[Pasted image 20240510202304.png]]


![[Pasted image 20240510202319.png]]
