# m00nwalk
we have been given an audio file and we have to decode it.
audio file: - `message.wav`

## hints given: -
1.) How did pictures from the moon landing get sent back to Earth?
2.) What is the CMU mascot?, that might help select a RX option
##

When we look for the hints, we get to know that `qsstv` is a software which is used to sent pictures from space to earth and the name of the
CMU mascot is named `scotty`.

Here given below is the working of this challenge: -

on tab 1 :- Here i have installed qsstv and other required packages for it. After that launching `qsstv`.
```bash
muizz@LAPTOP-VF1FT9IQ:~$ sudo apt-get install qt5-default libopenjp2-7-dev libpulse-dev libv4l-dev libasound2-dev libgtk-3-dev libfftw3-dev
[sudo] password for muizz:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package qt5-default is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source

E: Package 'qt5-default' has no installation candidate
muizz@LAPTOP-VF1FT9IQ:~$ sudo apt-get install hamlib-dev
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
E: Unable to locate package hamlib-dev
muizz@LAPTOP-VF1FT9IQ:~$ sudo apt-get install qsstv
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
qsstv is already the newest version (9.5.8-2).
0 upgraded, 0 newly installed, 0 to remove and 56 not upgraded.
muizz@LAPTOP-VF1FT9IQ:~$ qsstv
QStandardPaths: wrong permissions on runtime directory /run/user/1000/, 0755 instead of 0700
muizz@LAPTOP-VF1FT9IQ:~$
```

on tab 2:- Here i have open the sound control tab where we have to alter some settings
```bash
muizz@LAPTOP-VF1FT9IQ:~$ pactl load-module module-null-sink sink_name=virtual-cable
23
muizz@LAPTOP-VF1FT9IQ:~$ pavucontrol
```
We have to select `Monitor of Null Output` in the from section.
![Screenshot 2024-12-18 164837](https://github.com/user-attachments/assets/18c6c451-87d7-4ec2-b44b-e6a78c4e8f66)



In the image given below, I have selected PulseAudio set input audio voice and output audio voice to `pulse -- PulseAudio Sound Server`.
This can be done by selecting the configurations tab.

![Screenshot 2024-12-18 164825](https://github.com/user-attachments/assets/91d8a0f7-35c9-4f33-894a-ce096622e312)

on tab 3: - here to use the input `paplay -d virtual-cable` following by the name of the audio file. After this the qsstv software will start
recieving the audio and will generate the image.
```bash
muizz@LAPTOP-VF1FT9IQ:~$ ls
Dockerfile                  convert.py:Zone.Identifier                 key                                   picture1.bmp
Dockerfile:Zone.Identifier  cryptonite_taskphase_Muizz                 key.pub                               picture2.bmp
chall                       flag.txt                                   ld-linux-x86-64.so.2                  picture3.bmp
chall:Zone.Identifier       format-string-1                            ld-linux-x86-64.so.2:Zone.Identifier  program.deb
chall_1.S                   format-string-1.1                          libc.so.6                             qsstv
ciphertext                  freakada_3301_message.png                  libc.so.6:Zone.Identifier             signal.sr:Zone.Identifier
ciphertext:Zone.Identifier  freakada_3301_message.png:Zone.Identifier  message.wav                           vuln
convert.py                  game-redacted.c                            message.wav:Zone.Identifier
muizz@LAPTOP-VF1FT9IQ:~$ paplay -d virtual-cable message.wav
```

The final image after fully recieving the message: -
![Screenshot 2024-12-18 165243](https://github.com/user-attachments/assets/cf8b9ae0-c8c4-44ab-9875-ebfeeb08e8f6)

Therefore, flag: - `picoCTF{beep_boom_im_in_space}`.

This is how i solved it.

## references
1.) https://ourcodeworld.com/articles/read/956/how-to-convert-decode-a-slow-scan-television-transmissions-sstv-audio-file-to-images-using-qsstv-in-ubuntu-18-04
2.) https://www.m0plt.me.uk/qsstv.php
##
#





