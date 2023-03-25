In cryptography, FEAL (the **Fast data Encipherment ALgorithm**) is a block cipher proposed as an alternative to the Data Encryption Standard (DES), and designed to be much faster in software.

This  Feistel based algorithm was first published in 1987 by **Akihiro Shimizu** and **Shoji Miyaguchi**.

The algorithm begins by taking the initial 64-  bit key specified by the user and immediately executes the Key Schedule process. 
The key  schedule process generates a total of 16 subkeys (for an 8 rounds FEAL implementation), each one of 16-bit long. In total, these subkeys conform a 256-bit key.

For the eight round implementation, there is a total of 16 subkeys; one subkey for each  
round (from 0 to 7), as well as eight additional subkeys (from 8 to 15). 
Four of these additional  subkeys (from 8 to 11) are used in the beginning and the last four (from 12 to 15) in the ending  of the encipherment process.

This is better understood looking at these step by step indications:  

1 The 64-bit long plaintext and User Key are accepted as input.  

2 During the key schedule process FEAL takes the 64-bit user key and generates 8  
subkeys plus one subkey for each round (each subkey is 16-bit long).  

3 First phase of the encipherment algorithm uses 4 subkeys (from 8 to 11).  

4 Each Feistel round uses one subkey. Normally, the implementation consists of eight  
rounds and it uses the subkeys from 0 to 7. Our Implementation has a variable number  
of rounds.  

5 Last phase of the encipherment algorithm uses 4 more subkeys (from 12 to 15).  

6 At the end, a random 64-bit ciphertext is returned


To generate the subkeys, the Key Schedule algorithm uses a special function defined by  
the authors and an S-function which adds the inputs and rotates the bits. The FEAL  
encipherment algorithm will output a supposedly random 64-bit ciphertext from the original 64-  bit plaintext. 
This means FEAL needs two 64-bit sequences one for the plaintext and one for the key.

**S-Function**

The S-Function is used within the Fk-Function and F-Function. Fk-Function is used during the  
Key Schedule process and the F-Function is used during the encryption and decryption  
process. Basically, S-Function takes care of implementing the S-Boxes of FEAL. It accepts  
three byte parameters and returns a single byte value. 
The S-Function can be explained  following these steps:  
										byte A  
										byte B  
										byte δ = 0 or 1  
										S(A,B,δ) = RotateL2(T)  
										T = A + B + δ mod 256

#### Fk-Function  
The Fk-Function is used during the Key Schedule process to generate the 16-bit subkeys. It is  important to mention the Fk-Function internally uses the S-Function. It accepts two 
32-bit  parameters and returns a 32-bit value containing two 16-bit subkeys each time is executed.

α and β: 32 bit halves of initial key

![[Pasted image 20230104200930.png]]


**The F-Function**

The F-Function is used during the encryption and decryption processes and accepts two  
parameters. One of the parameters is a 16-bit subkey and the other is a 32-bit text message  
from the Feistel round. The following diagram explains the F-Function:  
										α: 32 bit from Feistel Round  
										β: 16 bit sub-key

![[Pasted image 20230104201705.png]]


#### Key Generation  
The key generation function, also called Key Schedule, takes the original 64-bit User Key as  
input and uses the Fk function to generate the 16-bit subkeys needed by the encryption  
process. The numbers of keys it generates depends on the number of rounds that will be used.  
The number of subkeys follows this formula:  
														nsK = nR+8  
														
Where nsK is the numbers of subkeys needed and nR is the number of rounds. The 8 constant  correspond to the last additional eight subkeys. Four of these subkeys are used in the beginning  and the last four subkeys are used at the end of the encipherment process. This Key  Generation Process in explained in the following Key Schedule diagram:

![[Pasted image 20230104202607.png]]

#### Encryption  
The FEAL encryption process consists of mixing the 64-bit plaintext and key provided by the  user and apply the F-Function to each one of the Feistel rounds. In the beginning, four 16-bit  subkeys from the key schedule are used. In an eight-rounds implementation, these first four  subkeys are from subkey 8 to 11. Then, one 16-bit subkey is used for each Feistel round (from subkey 0 to 7). At the end, the last four 16-bit subkeys (from 12 to 15) are used.
The Encryption diagram below shows the entire process.

![[Pasted image 20230104202955.png]]


#### Decryption  
The FEAL decryption process uses the same approach as the encryption. The only difference in  
this case is the process runs backwards. First, it uses the last four 16-bit subkeys (from 12 to  
15), then one subkey for each round and then the other four 16-bit subkeys (from 8 to 11) to  
recover the plaintext. The Decryption diagram below shows the entire process.

![[Pasted image 20230104203248.png]]



#### Strength 
FEAL working with no parity in an key block is safe from the all-key attack because it is controlled by a 64-bit key, which is more secure than 56-bit DES key.
Regarding cipher randomization, feal is considered safe because the randomization indices are closer to the theoritical values than those of DES

#### Conclusion

FEAL is an encripherment algorithm suitable for software implementation. 
It can be applied widely to small or other existing systems unable to use DES hardware because of the cost
Moreover, FEAL is suitable for hardware implementation, too. 
It can be used as the cryptographic method in all data communication fiield