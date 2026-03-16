# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:
```c
#include <stdio.h>
#include <string.h>

int generateMAC(char message[], char key[])
{
    int i, mac = 0;

    // Concatenate key and message
    char combined[200];
    strcpy(combined, key);
    strcat(combined, message);

    // Simple hash calculation
    for(i = 0; i < strlen(combined); i++)
    {
        mac = mac + combined[i];
    }

    return mac % 256;   // simple MAC value
}

int main()
{
    char message[100], key[100];
    int mac, received_mac;

    printf("Enter the message: ");
    scanf("%s", message);

    printf("Enter the secret key: ");
    scanf("%s", key);

    // Generate MAC
    mac = generateMAC(message, key);
    printf("Generated MAC: %d\n", mac);

    // Verification
    printf("Enter received MAC for verification: ");
    scanf("%d", &received_mac);

    if(mac == received_mac)
        printf("Message is authentic and unchanged\n");
    else
        printf("Message authentication failed\n");

    return 0;
}
```
## Output

![MAC Output](Screenshot%202026-03-16%20084534.png)

## Result
The program is executed successfully.
