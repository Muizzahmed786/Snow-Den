# Day 1
In day 1, we are introduced to OPSEC, which is operational security. It is a term which was used in the military to refer to the process of protecting sensitive information
and operations form adversaries.

In this task we are given a website which is a youtube to .mp3 converter.
These websites are prone to have significant risks, such as : -

1.) Malvertising: Many sites contain malicious ads that can exploit vulnerabilities in a user's system, which could lead to infection.
2.) Phishing scams: Users can be tricked into providing personal or sensitive information via fake surveys or offers.
3.) Bundled malware: Some converters may come with malware, tricking users into unknowingly running it.

we are given a youtube link `https://www.youtube.com/watch?v=dQw4w9WgXcQ` which we have to convet to .mp3 file.
Upon doing that we recieve two .mp3 files namely song.mp3 and somg.mp3. The second one seems to be suspicious.

![Screenshot (731)](https://github.com/user-attachments/assets/c1fdc017-84f2-484e-851d-01ee5cb24f42)

As we can see in the above image that using the `file` command on files `song.mp3` and `somg.mp3` gives us the file type of the respective file.
On using this command on `somg.mp3` file we see that it is not an audio file, but it's a MS Windows shortcut.

`exiftool` is a command is used to reveal the embedded commands and attributes of a file.
![Screenshot (732)](https://github.com/user-attachments/assets/109ab3fe-aa6b-4c97-8518-4a2b586d8d48)

## Learnings
1.) Learnt about OPSEC and what are the common mistakes which lead to different vulnerabilities.

