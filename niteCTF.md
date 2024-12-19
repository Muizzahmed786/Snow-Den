# Disclaimer: - I was not able to solve any challenge in niteCTF.

## Miscellaneous:- Beyond a plane
In this challenge we were given a photo of a metro station and we had to find out a billboard which was about a concert held on 26 October 2024.
upon looking at the metro station, it was a station in Gurgaon. Station name is Vodafone Belvedere Towers metro station. Here is the image of it.
![WhatsApp Image 2024-12-15 at 15 30 43_9286ab88](https://github.com/user-attachments/assets/6a9e9289-4d79-4340-aad6-6ad0a71907ea)

Searching for concerts on 26 October 2024, I found many concerts organised, but one seemed to be like less known by the people, which was the concert organised by Hyundai India.
This event was called Hyundai Spotlight and multiple artists performed there.
The flag to the challenge was `nite{Hyundai,Shankar_Ehsaan_Loy,KTPO}`.
##

## Binary Exploitation:- Print the gifts
source code:-
```bash
#include<stdio.h>
#include<string.h>

int main()
{
	setvbuf(stdin,NULL,2,0);
	setvbuf(stdout,NULL,2,0);
	char buf[100];

	while(1)
	{
		char c = ' ';
		printf("What gift do you want from santa\n>");
		fgets(buf,sizeof(buf),stdin);
		printf("Santa brought you a ");
		printf(buf);
		puts("do you want another gift?\nEnter y or n:");
		scanf("%c",&c);
		if('n'==c)
			break;	
		getchar();
	}
}
```
In the source code we can see that in `printf(buf)` there is a format string vulnerability, What we had to do was to write a payload to the buffer and see how it reacts to it.
What we had to do here was to include `%n` fromat specifier as part of the payload, what is does is it writes a vlaue to the memory address i.e. memory manipulation.

flag: - `nite{0nLy_n4ugHty_k1d5_Use_%n}`
