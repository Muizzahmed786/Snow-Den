# tunn3l v1s10n

In this challenge we are provided with a file with .BMP extension. This tells us that it is a bit-map file.
A bit-map file is an image file format which is used to store bitmap digital images. It is capable of storing 2-D images in various color depths.

to access this file we require a hex editor, through which we can make some changes required to open the file.

The image given below shows the initial file specifications.
![Screenshot (722)](https://github.com/user-attachments/assets/04887078-716a-4b09-b35e-2dde34062a43)

As we can see in OA offset BA is present, which is incorrect because OA offset is the starting address of the byte where the bitmap image data can be found.
Similar case is for OE offset. OE offset gives the size of the header.
0B offset is the binary literal of the byte.

If we make some changes in the values of the offset in hexadecimal form, we can acccess the file.

![Screenshot (723)](https://github.com/user-attachments/assets/5d05d175-3f1b-4f3b-b201-aa2dad29bcd6)

Now if we try opening it we can see the image given below

![Screenshot (720)](https://github.com/user-attachments/assets/b82ed2b9-f59d-4df7-baa8-b655a24f7c5f)

flag :- picoCTF{qu1t3_a_v13w_2020}

This is how i solved it.

## references
1.) https://en.wikipedia.org/wiki/BMP_file_format




