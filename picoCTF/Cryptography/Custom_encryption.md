# Custom_encryption

in this challenge we are given a python encoding script and from that we have to create a decryption script.
the encrypted file information is provided to us:- `https://artifacts.picoctf.net/c_titan/18/enc_flag`.
The encryption script is given below:-
```bash
from random import randint
import sys


def generator(g, x, p):
    return pow(g, x) % p


def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(((ord(char) * key*311)))
    return cipher


def is_prime(p):
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    if v > 1:
        return False
    else:
        return True


def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text


def test(plain_text, text_key):
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers")
        return
    a = randint(p-10, p)
    b = randint(g-10, g)
    print(f"a = {a}")
    print(f"b = {b}")
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        return
    semi_cipher = dynamic_xor_encrypt(plain_text, text_key)
    cipher = encrypt(semi_cipher, shared_key)
    print(f'cipher is: {cipher}')


if __name__ == "__main__":
    message = sys.argv[1]
    test(message, "trudeau")
```

in the `test` function we can see that `message` and `"trudeau"` are passed as arguments;
two variables `p=97` and `g=31` are initialized. In this function only another function `generator` is called and the variables `u`,`v` and `key` are assigned when it
returns a value. After that it looks like `key`, `b_key` and `shared_key` will have the some value.
Then `semi_cipher` is assigned to the result of `dynamic_xor_encrypt(plain_text, text_key)`.

In `dynamic_xor_encrypt` function string `cipher_text` is initialized. Here `text_key` is `"trudeau"` and `plaintet` is our `message`.
After that a block of code is present which calculates `cipher_text` and then returns it.
After that `cipher` is assigned to the result of `encrypt(semi_cipher, share_key)`.
In the `encrypt` function an array `cipher` is initialized and then `cipher.append(((ord(char) * key*311)))` gives us the individual array elemnts as the loop is goinf on.
And then this array is returned. The `cipher` which we have in the flag information comes from here and we have to decrypt it.

the decryption script is given below :-
```bash
def generator(g, x, p):
    return pow(g, x) % p

def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text

a = 94
b = 29
cipher = [260307, 491691, 491691, 2487378, 2516301, 0, 1966764, 1879995, 1995687, 1214766, 0, 2400609, 607383, 144615, 1966764, 0, 636306, 2487378, 28923, 1793226, 694152, 780921, 173538, 173538, 491691, 173538, 751998, 1475073, 925536, 1417227, 751998, 202461, 347076, 491691]
p = 97
g = 31

u = generator(g, a, p)
v = generator(g, b, p)
key = generator(v, a, p)

dec = ""
for i in cipher:
    dec = dec + chr(i // 311 // key)

print(dynamic_xor_encrypt(dec,"aedurtu"))
```
The terminal output is given below :-
```bash
PS C:\Users\Muizz Ahmed\Desktop\PYTHON> python -u "c:\Users\Muizz Ahmed\Desktop\PYTHON\dec_custom_enc.py"
Traceback (most recent call last):
  File "c:\Users\Muizz Ahmed\Desktop\PYTHON\dec_custom_enc.py", line 22, in <module>
    key = generator(v, a, p)
                    ^
NameError: name 'v' is not defined
PS C:\Users\Muizz Ahmed\Desktop\PYTHON> python -u "c:\Users\Muizz Ahmed\Desktop\PYTHON\dec_custom_enc.py"
picoCTF{custom_d2cr0pt6d_751a22dc}
PS C:\Users\Muizz Ahmed\Desktop\PYTHON>
```

in the decryption script I have decalred a string `dec`. the `for` loop iterates through every element of the `cipher` array and converts each element into their
character representation, the `chr()` function does this and `ord()` gives us the numerical representation.
after that, in `print(dynamic_xor_encrypt(dec,"aedurtu"))` the `"aedurtu"` comes when instead of it I entered `"picoCTF"`. When I tried with `"trudeau"` I was not
getting the correct result.

FLAG:- `picoCTF{custom_d2cr0pt6d_751a22dc}`.
