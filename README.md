# encryption-decryption
Arm Assembly , Raspberry PI 4. 

The program uses command line arguments to determine what to do. It accepts two argument values. 
The first is the word encrypt or decrypt to specify the operation.
The second is a string of lowercase letters representing the key for the algorithm.
If I do not get exactly two arguments of the correct form I print an error message and quit the program.

For this program, I read from stdin and
redirect the contents of a file as input on the command line. Similarly, rather 
than opening a file for output, I write to stdout and redirect this output to a file on the command line.

When the encryption option is chosen I transform the data first using Autokey, and then with double columnar transposition. 
When decrypting with the same keyword, I  do the transposition cipher first and follow that with Autokey substitution. 

The columnar tranposition cipher (you can read about it here: 
https://crypto.interactive-maths.com/columnar-transposition-cipher.html). 
Essentially the text of the block is first placed into a square table (the size of the table is 
the same as the length of the keyword) row by row. Then it is extracted column by column, where the ordering of t
he columns is determined by the alphabetical ordering of the letters in the keyword. 
When processing the final block, which will be undersized,
I fill out the remaining portion of the table with spaces. 
This process is repeated again to increase the level of security.

 The substitution cipher known as the Autokey cipher (you can read about it 
 here: https://crypto.interactive-maths.com/autokey-cipher.html). A 2D lookup
 table is used to perform the substitution for each letter, where the letters
 of the key are used in the beginning for one dimension of the table, then being followed by the plain text. 
 The plain text letters are used for the other dimension of the table. Each letter pairing picks a 
 replacement character from the corresponding entry in the table. This process is basically reversed for
 decryption. Rather than simply hard-coding this table in the data area, 
 I wrote a function that automatically fills in an appropriate sized memory area with the letters.
 
 
 Compile code:

gcc -g -o  encrypdecrypt encrypdecrypt.s

Run Encryption Command

./encrypdecrypt encrypt king < file.txt >  output.txt

Run Decryption Command

./encrypdecrypt Decrypt king < file.txt >  output.txt


| Method        | Key           | File.txt content  | First Encryption/Decryption | Output.txt ( Second Encryption/Decryption)
| ------------- | ------------- | ------------------| ----------------------------| ----------------------------------------
| Encrypt       | king          | MEETMEATTHECORNER | WMRZYIEMFLEVHYRGF           | ZMVGMILYWYFHFREER
| Decrypt       | king          | ZMVGMILYWYFHFREER | WMRZYIEMFLEVHYRGF           | MEETMEATTHECORNER

In case of encryption, First encryption is vigenere and second encryption is double columnar tranpsotion resulting in output.txt

In case of decryption, First decryption is done using tranposition and then second decryption done
using vigenere resulting in output.txt
