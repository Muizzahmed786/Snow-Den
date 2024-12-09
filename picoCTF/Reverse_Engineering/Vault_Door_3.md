# Vault Door 3

In this challenge we are given a source code `https://jupiter.challenges.picoctf.org/static/a4018cec1446761cb2e8cce05db925fa/VaultDoor3.java`
in which a program is written for the password of a vault.

Source code: -
```bash
import java.util.*;

class VaultDoor3 {
    public static void main(String args[]) {
        VaultDoor3 vaultDoor = new VaultDoor3();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
        String input = userInput.substring("picoCTF{".length(), userInput.length() - 1);
        if (vaultDoor.checkPassword(input)) {
            System.out.println("Access granted.");
        } else {
            System.out.println("Access denied!");
        }
    }

    // Our security monitoring team has noticed some intrusions on some of the
    // less secure doors. Dr. Evil has asked me specifically to build a stronger
    // vault door to protect his Doomsday plans. I just *know* this door will
    // keep all of those nosy agents out of our business. Mwa ha!
    //
    // -Minion #2671

    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i = 0; i < 8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i < 16; i++) {
            buffer[i] = password.charAt(23 - i); 
        }
        for (; i < 32; i += 2) {
            buffer[i] = password.charAt(46 - i); 
        }
        for (i = 31; i >= 17; i -= 2) {
            buffer[i] = password.charAt(i); 
        }
        System.out.print(buffer);
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm12g94c_u_4_m7ra41");
    }
}
```

in the VaultDoor3 class we can see that a sub-string input is given where the format of the string is `picoCTF{   }`. 

![Screenshot (743)](https://github.com/user-attachments/assets/81e56b7b-db55-4f4b-81e9-ffc72b25be41)


Now we go to the checkPassword function where the string password is passed as a parameter.
The password length should be equal to 32 otherwise it will return false.

initially i tried entering some random password to check if it's working.
After that i entered `jU5t_a_sna_3lpm12g94c_u_4_m7ra41` because it looks similar to a flag, but it is scrambled.

![Screenshot (739)](https://github.com/user-attachments/assets/33a7a09d-cf3b-44ad-a725-51e41283c2d1)

Then i entered picoCTF{jU5t_a_sna_3lpm12g94c_u_4_m7ra41} as password. This is because it will go through all the instructions and compare with the buffer
and it may give us the unscrambled string.
To get the unscrambled string we printed the buffer on the console.

![Screenshot (742)](https://github.com/user-attachments/assets/ebcc2354-6b5d-45de-938b-c4c5b6814f39)

the output is mentioned below.
```bash
PS C:\Users\Muizz Ahmed\Desktop\JAVA> cd "c:\Users\Muizz Ahmed\Desktop\JAVA\" ; if ($?) { javac VaultDoor3.java } ; if ($?) { java VaultDoor3 }
Enter vault password: picoCTF{jU5t_a_sna_3lpm12g94c_u_4_m7ra41}
jU5t_a_s1mpl3_an4gr4m_4_u_c79a21Access denied!
PS C:\Users\Muizz Ahmed\Desktop\JAVA>
```
we got the unscramble string as `jU5t_a_s1mpl3_an4gr4m_4_u_c79a21`.

Therefore, the final flag is `picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_c79a21}`.

This is how I solved it.
