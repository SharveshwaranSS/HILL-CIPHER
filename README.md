# HILL CIPHER
## EX. NO: 3 
## AIM:
 IMPLEMENTATION OF HILL CIPHER
## To write a C program to implement the hill cipher substitution techniques.
## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To decrypt the message, each block is multiplied by the inverse of the m trix used for encryption. The matrix used for encryption is the cipher key, and it shold be chosen randomly from the set of invertible n × n matrices (modulo 26).

## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
~~~
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define MOD 26

int key[3][3], invKey[3][3];

// Function to multiply the matrix for encryption/decryption
void hillCipher(char message[], int matrix[3][3]) {
    char result[100];
    int len = strlen(message);

    // Padding if needed
    while (len % 3 != 0) {
        message[len++] = 'X';
        message[len] = '\0';
    }

    for (int i = 0; i < len; i += 3) {
        int x = (matrix[0][0] * (message[i] - 'A') + matrix[0][1] * (message[i + 1] - 'A') + matrix[0][2] * (message[i + 2] - 'A')) % MOD;
        int y = (matrix[1][0] * (message[i] - 'A') + matrix[1][1] * (message[i + 1] - 'A') + matrix[1][2] * (message[i + 2] - 'A')) % MOD;
        int z = (matrix[2][0] * (message[i] - 'A') + matrix[2][1] * (message[i + 1] - 'A') + matrix[2][2] * (message[i + 2] - 'A')) % MOD;

        result[i] = (x + 'A');
        result[i + 1] = (y + 'A');
        result[i + 2] = (z + 'A');
    }
    result[len] = '\0';
    printf("%s\n", result);
}

int main() {
    char message[100];

    // Get key matrix
    printf("Enter 3x3 key matrix:\n");
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            scanf("%d", &key[i][j]);

    // Get inverse key matrix
    printf("Enter 3x3 inverse key matrix:\n");
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            scanf("%d", &invKey[i][j]);

    // Get message input
    printf("Enter message (uppercase only, no spaces): ");
    scanf("%s", message);

    printf("Encrypted message: ");
    hillCipher(message, key);

    printf("Decrypted message: ");
    hillCipher(message, invKey);

    return 0;
}

~~~
## OUTPUT
![image](https://github.com/user-attachments/assets/3db9bb29-76a8-4a2c-89bc-ee70fb63a3b7)
## Result:
The program is executed successfully

