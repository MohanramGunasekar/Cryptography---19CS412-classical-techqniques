# Cryptography---19CS412-classical-techqniques
# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.


## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

1.	In Ceaser Cipher each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.
2.	For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.
3.	The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the   
    scheme, A = 0, B = 1, Z = 25.
4.	Encryption of a letter x by a shift n can be described mathematically as,
                       En(x) = (x + n) mod26
5.	Decryption is performed similarly,
                       Dn (x)=(x - n) mod26


## PROGRAM:
```
#include<stdio.h>
#include <string.h>
#include<conio.h>
#include <ctype.h>
int main()
{
char plain[10], cipher[10];
int key,i,length;
int result;
printf("\n Enter the plain text:");
scanf("%s", plain);
printf("\n Enter the key value:");
scanf("%d", &key);
printf("\n \n \t PLAIN TEXt: %s",plain);
printf("\n \n \t ENCRYPTED TEXT: ");
for(i = 0, length = strlen(plain); i < length; i++)
{
cipher[i]=plain[i] + key;
if (isupper(plain[i]) && (cipher[i] > 'Z'))
cipher[i] = cipher[i] - 26;
if (islower(plain[i]) && (cipher[i] > 'z'))
cipher[i] = cipher[i] - 26;
printf("%c", cipher[i]);
}
printf("\n \n \t AFTER DECRYPTION : ");
for(i=0;i<length;i++)
{
plain[i]=cipher[i]-key;
if(isupper(cipher[i])&&(plain[i]<'A'))
plain[i]=plain[i]+26;
if(islower(cipher[i])&&(plain[i]<'a'))
plain[i]=plain[i]+26;
printf("%c",plain[i]);
}
return 0;
}
```

## OUTPUT:

![Screenshot 2024-09-02 102404](https://github.com/user-attachments/assets/faeaaae7-23b6-469f-ad8f-afc6f0b37c75)


## RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.

 
## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

ALGORITHM DESCRIPTION:
The Playfair cipher uses a 5 by 5 table containing a key word or phrase. To generate the key table, first fill the spaces in the table with the letters of the keyword, then fill the remaining spaces with the rest of the letters of the alphabet in order (usually omitting "Q" to reduce the alphabet to fit; other versions put both "I" and "J" in the same space). The key can be written in the top rows of the table, from left to right, or in some other pattern, such as a spiral beginning in the upper-left-hand corner and ending in the centre.
The keyword together with the conventions for filling in the 5 by 5 table constitutes the cipher key. To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. Then apply the following 4 rules, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter. Encrypt the new pair and continue. Some   
   variants of Playfair use "Q" instead of "X", but any letter, itself uncommon as a repeated pair, will do.
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively (wrapping 
   around to the left side of the row if a letter in the original pair was on the right side of the row).
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively (wrapping around 
   to the top side of the column if a letter in the original pair was on the bottom side of the column).
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of 
   corners of the rectangle defined by the original pair. The order is important – the first letter of the encrypted pair is the one that 
    lies on the same row as the first letter of the plaintext pair.
To decrypt, use the INVERSE (opposite) of the last 3 rules, and the 1st as-is (dropping any extra "X"s, or "Q"s that do not make sense in the final message when finished).


## PROGRAM:
```
#include<stdio.h>
#include<conio.h>
#include<string.h>
#include<ctype.h>
#define MX 5
void playfair(char ch1,char ch2, char key[MX][MX])
{
int i,j,w,x,y,z;
FILE *out;
if((out=fopen("cipher.txt","a+"))==NULL)
{
printf("File Corrupted.");
}
for(i=0;i<MX;i++)
{
for(j=0;j<MX;j++)
{
if(ch1==key[i][j])
{
w=i;
x=j;
}
else if(ch2==key[i][j])
{
y=i;
z=j;
}}}
//printf("%d%d %d%d",w,x,y,z);
if(w==y)
{
x=(x+1)%5;z=(z+1)%5;
printf("%c%c",key[w][x],key[y][z]);
fprintf(out, "%c%c",key[w][x],key[y][z]);
}
else if(x==z)
{
w=(w+1)%5;y=(y+1)%5;
printf("%c%c",key[w][x],key[y][z]);
fprintf(out, "%c%c",key[w][x],key[y][z]);
}
else
{
printf("%c%c",key[w][z],key[y][x]);
fprintf(out, "%c%c",key[w][z],key[y][x]);
}
fclose(out);
}
int main()
{
int i,j,k=0,l,m=0,n;
char key[MX][MX],keyminus[25],keystr[10],str[25]={0};
char
alpa[26]={'A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z'};
printf("\nEnter key:");
gets(keystr);
printf("\nEnter the plain text:");
gets(str);
n=strlen(keystr);
//convert the characters to uppertext
for (i=0; i<n; i++)
{
if(keystr[i]=='j')keystr[i]='i';
else if(keystr[i]=='J')keystr[i]='I';
keystr[i] = toupper(keystr[i]);
}
//convert all the characters of plaintext to uppertext
for (i=0; i<strlen(str); i++)
{
if(str[i]=='j')str[i]='i';
else if(str[i]=='J')str[i]='I';
str[i] = toupper(str[i]);
}
j=0;
for(i=0;i<26;i++)
{
for(k=0;k<n;k++)
{
if(keystr[k]==alpa[i])
break;
else if(alpa[i]=='J')
break;
}
if(k==n)
{
keyminus[j]=alpa[i];j++;
}
}
//construct key keymatrix
k=0;
for(i=0;i<MX;i++)
{
for(j=0;j<MX;j++)
{
if(k<n)
{
key[i][j]=keystr[k];
k++;}
else
{
key[i][j]=keyminus[m];m++;
}
printf("%c ",key[i][j]);
}
printf("\n");
}
printf("\n\nEntered text :%s\nCipher Text :",str);
for(i=0;i<strlen(str);i++)
{
if(str[i]=='J')str[i]='I';
if(str[i+1]=='\0')
playfair(str[i],'X',key);
else
{
if(str[i+1]=='J')str[i+1]='I';
if(str[i]==str[i+1])
playfair(str[i],'X',key);
else
{
playfair(str[i],str[i+1],key);
i++;
}}
}
return 0;
}
 
```

## OUTPUT:

![Screenshot 2024-09-02 102634](https://github.com/user-attachments/assets/d6aebfcc-cd36-4e0d-a76a-df192cd214c5)

## RESULT:
The program is executed successfully


---------------------------

# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Hill cipher is a substitution cipher invented by Lester S. Hill in 1929. Each letter is represented by a number modulo 26. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, again modulus 26.
To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption. The matrix used for encryption is the cipher key, and it should be chosen randomly from the set of invertible n × n matrices (modulo 26).
The cipher can, be adapted to an alphabet with any number of letters. All arithmetic just needs to be done modulo the number of letters instead of modulo 26.


## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int keymat[3][3] = { { 1, 2, 1 }, { 2, 3, 2 }, { 2, 2, 1 } };
int invkeymat[3][3] = { { -1, 0, 1 }, { 2, -1, 0 }, { -2, 2, -1 } };
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

// Function to encode a triplet of characters
void encode(char a, char b, char c, char ret[]) {
    int x, y, z;
    int posa = (int)a - 65;
    int posb = (int)b - 65;
    int posc = (int)c - 65;

    x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];

    ret[0] = key[x % 26];
    ret[1] = key[y % 26];
    ret[2] = key[z % 26];
    ret[3] = '\0';
}

// Function to decode a triplet of characters
void decode(char a, char b, char c, char ret[]) {
    int x, y, z;
    int posa = (int)a - 65;
    int posb = (int)b - 65;
    int posc = (int)c - 65;

    x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];

    ret[0] = key[(x % 26 < 0) ? (26 + x % 26) : (x % 26)];
    ret[1] = key[(y % 26 < 0) ? (26 + y % 26) : (y % 26)];
    ret[2] = key[(z % 26 < 0) ? (26 + z % 26) : (z % 26)];
    ret[3] = '\0';
}

int main() {
    char msg[1000];
    char enc[1000] = "";
    char dec[1000] = "";
    int n;

    strcpy(msg, "MOHAN");
    printf("Input message : %s\n", msg);

    // Convert the input message to uppercase
    for (int i = 0; i < strlen(msg); i++) {
        msg[i] = toupper(msg[i]);
    }

    // Remove spaces
    n = strlen(msg) % 3;

    // Append padding text 'X' if necessary
    if (n != 0) {
        for (int i = 1; i <= (3 - n); i++) {
            strcat(msg, "X");
        }
    }

    printf("Padded message : %s\n", msg);

    // Encode the message
    for (int i = 0; i < strlen(msg); i += 3) {
        char a = msg[i];
        char b = msg[i + 1];
        char c = msg[i + 2];
        char encoded[4];
        encode(a, b, c, encoded);
        strcat(enc, encoded);
    }

    printf("Encoded message : %s\n", enc);

    // Decode the message
    for (int i = 0; i < strlen(enc); i += 3) {
        char a = enc[i];
        char b = enc[i + 1];
        char c = enc[i + 2];
        char decoded[4];
        decode(a, b, c, decoded);
        strcat(dec, decoded);
    }

    printf("Decoded message : %s\n", dec);
    return 0;
}
```


## OUTPUT:

![Screenshot 2024-09-02 103324](https://github.com/user-attachments/assets/0fce1432-0a08-46d6-8d40-004b6497cc50)


## RESULT:
The program is executed successfully

-------------------------------------------------

# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Vigenere cipher is a method of encrypting alphabetic text by using a series of different Caesar ciphers based on the letters of a keyword. It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. It consists of the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.



## PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>  // For exit() function
#include <ctype.h>   // For toupper() function
#include <string.h>  // For strlen() function

void encipher();
void decipher();

int main() {
    int choice;
    while (1) {
        printf("\n1. Encrypt Text");
        printf("\n2. Decrypt Text");
        printf("\n3. Exit");
        printf("\n\nEnter Your Choice: ");
        scanf("%d", &choice);

        if (choice == 3)
            exit(0);
        else if (choice == 1)
            encipher();
        else if (choice == 2)
            decipher();
        else
            printf("Please Enter a Valid Option.\n");
    }
    return 0;  // Added return statement for the main function
}

void encipher() {
    unsigned int i, j;
    char input[50], key[10];

    printf("\n\nEnter Plain Text: ");
    scanf("%s", input);  // Removed newline for better input handling

    printf("Enter Key Value: ");
    scanf("%s", key);

    printf("Resultant Cipher Text: ");
    for (i = 0, j = 0; i < strlen(input); i++, j++) {
        if (j >= strlen(key)) {
            j = 0;
        }
        printf("%c", 65 + (((toupper(input[i]) - 65) + (toupper(key[j]) - 65)) % 26));
    }
    printf("\n");  // Added newline for output formatting
}

void decipher() {
    unsigned int i, j;
    char input[50], key[10];
    int value;

    printf("\n\nEnter Cipher Text: ");
    scanf("%s", input);  // Removed newline for better input handling

    printf("Enter the Key Value: ");
    scanf("%s", key);

    printf("Resultant Plain Text: ");
    for (i = 0, j = 0; i < strlen(input); i++, j++) {
        if (j >= strlen(key)) {
            j = 0;
        }

        // Calculate the decrypted character value
        value = (toupper(input[i]) - 65) - (toupper(key[j]) - 65);
        if (value < 0) {
            value += 26;  // Correct for negative values in circular shift
        }
        printf("%c", 65 + (value % 26));
    }
    printf("\n");  // Added newline for output formatting
}
```

## OUTPUT:

![Screenshot 2024-09-02 103543](https://github.com/user-attachments/assets/0da7c926-22bd-49c3-b404-2ea57c1a218a)


## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
In the rail fence cipher, the plaintext is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main() {
    int i, j, len, rails, count;
    char str[1000];
    int code[100][1000]; 

    printf("Enter a Secret Message: ");
    fgets(str, sizeof(str), stdin);  
    str[strcspn(str, "\n")] = '\0'; 

    len = strlen(str);

    printf("Enter number of rails: ");
    scanf("%d", &rails);

    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            code[i][j] = 0;
        }
    }

    count = 0;  
    j = 0;      

    while (j < len) {
        if (count % 2 == 0) {
            for (i = 0; i < rails && j < len; i++) {
                code[i][j] = (int)str[j]; 
                j++;
            }
        } else {
            for (i = rails - 2; i > 0 && j < len; i--) {
                code[i][j] = (int)str[j]; 
                j++;
            }
        }
        count++;
    }

 
    printf("\nEncrypted Message: ");
    for (i = 0; i < rails; i++) {
        for (j = 0; j < len; j++) {
            if (code[i][j] != 0) {
                printf("%c", code[i][j]);
            }
        }
    }
    printf("\n");

    return 0;
}
```
## OUTPUT:

![Screenshot 2024-09-02 103748](https://github.com/user-attachments/assets/02930d68-a2a5-4495-93d5-7188a7efa4da)


## RESULT:
The program is executed successfully
