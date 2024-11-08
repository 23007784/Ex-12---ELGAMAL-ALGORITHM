# Ex-12---ELGAMAL-ALGORITHM
## AIM
To implement ElGamal Cryptography in Python for secure communication,
focusing on key generation, encryption, and decryption processes
## ALGORITHM
Step 1: Choose a large prime number “p” and a primitive root “g” modulo “p”.                         
Step 2: Each party generates a private key x (random integer such that 1<x<p).             
Step 3: Each party computes the public key y=g^x mod p.          
Step 4: The sender chooses a random integer k (where 1<k<p1 < k < p1<k<p).          
Step 5: The sender computes the ciphertext:    
c1=g^k mod p                          
c2=m⋅y^k mod p (where mmm is the plaintext message).                        
Step 6: The ciphertext is sent as the pair (c1, c2).                       
Step 7: The receiver computes the shared secret.                 
Step 8: The receiver recovers the plaintext message.  
## PROGRAM
```
#include <stdio.h>
#include <math.h>
#include <stdlib.h>
int mod_exp(int base, int exp, int mod) {
int result = 1;
base = base % mod;
while (exp > 0) {
if (exp % 2 == 1) {
result = (result * base) % mod;
}
exp = exp >> 1; 
base = (base * base) % mod;
}
return result;
}
int gcd(int a, int b) {
if (b == 0)
return a;
else
return gcd(b, a % b);

}
int main() {
int p, g, x;
int h, y; 
int message, k;
int c1, c2, decrypted_message; 
printf("\n\n****Elgamal encryption and decryption**\n\n");
printf("Enter a large prime number (p): ");
scanf("%d", &p);
printf("Enter a primitive root of p (g): ");
scanf("%d", &g);
printf("Enter the private key (x): ");
scanf("%d", &x);
h = mod_exp(g, x, p);
printf("Public key (h) = %d\n", h);
printf("Enter the message to encrypt (as an integer less than p): ");
scanf("%d", &message);
do {
printf("Enter the ephemeral key (k) such that gcd(k, p-1) = 1: ");
scanf("%d", &k);
} while (gcd(k, p - 1) != 1);
c1 = mod_exp(g, k, p); 
c2 = (message * mod_exp(h, k, p)) % p; 
printf("Ciphertext (c1, c2) = (%d, %d)\n", c1, c2);
int inverse = mod_exp(c1, p - 1 - x, p); 
decrypted_message = (c2 * inverse) % p; 
printf("Decrypted message = %d\n", decrypted_message);
return 0;
}
```
## OUTPUT
![crypt12](https://github.com/user-attachments/assets/c18e2e01-0b35-4514-af88-cd3473913b62)

## RESULT
Thus, the program for ElGamal Cryptography was executed successfully,
demonstrating its eƯectiveness in securely encrypting and decrypting messages
between parties.
