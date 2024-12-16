# Trivial Flag Transfer Protocol
We are given a .PCAPNG file `https://mercury.picoctf.net/static/cc6074838ede2edf9f805fd2b58bdc58/tftp.pcapng`, and we have to recover the flag hidden.

## Hints given
1.) What are some other ways to hide data?
##

Now to open this file we need an application named WireShark, Which can be used to open .PCAPNG files.
When we open the file, we can see that one section shows all the different type of protocols, We have to extract the files
with Trivial Flag Transfer Protocol.
![Screenshot (778)](https://github.com/user-attachments/assets/6672d7c5-b984-49fa-acc3-24d0ed1f9ff1)

These are extracted files: -
![image](https://github.com/user-attachments/assets/62a6ed96-5020-499e-8e00-6aca65ef1465)

Now we need to look them one by one.

When we open the `instructions.txt` file we are given a ROT13 encoding.
`GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA`.

Upon decoding it: - `TFTP DOESNT ENCRYPT OUR TRAFFIC SO WE MUST DISGUISE OUR FLAG TRANSFER.FIGURE OUT A WAY TO HIDE THE FLAG AND I WILL CHECK BACK FOR THE PLAN`.

The decoded message mentions something about the extracted file `plan`.
Opening the `plan` file, again we have some encoded message.
`VHFRQGURCEBTENZNAQUVQVGJVGU-QHRQVYVTRAPR.PURPXBHGGURCUBGBF`.

Upon decoding it: - `I USED THE PROGRAM AND HID IT WITH-DUE DILIGENCE.CHECK OUT THE PHOTOS`.
The decoded meaage tells us about the `program.deb` file and has also mentioned how it hid the flag with `DUEDILIGENCE`.

One of the program that is used to hide data is `steghide`. We can use the help of the manpage of `steghiide` and `steghide --help`
to get more details about it.

```bash
muizz@LAPTOP-VF1FT9IQ:~$ ls
Dockerfile                  convert.py:Zone.Identifier                 key                                   picture3.bmp
Dockerfile:Zone.Identifier  cryptonite_taskphase_Muizz                 key.pub                               program.deb
chall                       flag.txt                                   ld-linux-x86-64.so.2                  qsstv
chall:Zone.Identifier       format-string-1                            ld-linux-x86-64.so.2:Zone.Identifier  signal.sr:Zone.Identifier
chall_1.S                   format-string-1.1                          libc.so.6                             vuln
ciphertext                  freakada_3301_message.png                  libc.so.6:Zone.Identifier
ciphertext:Zone.Identifier  freakada_3301_message.png:Zone.Identifier  picture1.bmp
convert.py                  game-redacted.c                            picture2.bmp
muizz@LAPTOP-VF1FT9IQ:~$ steghide extract -sf picture1.bmp
Enter passphrase:
steghide: could not extract any data with that passphrase!
muizz@LAPTOP-VF1FT9IQ:~$ steghide extract -sf picture1.bmp DUEDILIGENCE
steghide: unknown argument "DUEDILIGENCE".
steghide: type "steghide --help" for help.
muizz@LAPTOP-VF1FT9IQ:~$ steghide extract -sf picture1.bmp -p
steghide: the "-p" argument must be followed by the passphrase.
steghide: type "steghide --help" for help.
muizz@LAPTOP-VF1FT9IQ:~$ steghide extract -sf picture3.bmp
Enter passphrase:
the file "flag.txt" does already exist. overwrite ? (y/n) y
wrote extracted data to "flag.txt".
muizz@LAPTOP-VF1FT9IQ:~$ cat flag.txt
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
muizz@LAPTOP-VF1FT9IQ:~$
```

FLAG: - `picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}`

This is how i solved it.

