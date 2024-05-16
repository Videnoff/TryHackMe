Analyze the binary and obtain the flag  

Answer the questions below

| Question           | Answer                                                      |
| ------------------ | ----------------------------------------------------------- |
| What is the flag ? | flag{at_least_this_cafe_wont_leak_your_credit_card_numbers} |


![[Pasted image 20240510203501.png]]


*Using Ghidra:*

Open the main function:

![[Pasted image 20240510204541.png]]

Convert '-0x35010ff3' to decimal:

![[Pasted image 20240510204616.png]]

*Get the flag:*

![[Pasted image 20240510204633.png]]

