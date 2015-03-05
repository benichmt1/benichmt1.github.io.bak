---
layout: post
title: "sCTF 2015 Q1 - Overflow Tutorial"
description: ""
category: Tutorial
tags: [CTF, Beginner,Buffer Overflow]
---
{% include JB/setup %}
This problem made for a great introduction to beginner-level buffer overflows in C through an improper `fgets()`.

###Overflow

{% highlight text %}
Connect to the server with:

nc 104.236.255.49 12341
{% endhighlight %}

Upon connection to the server, a prompt appeared for a username. After entering a username, a simple menu appeared which allowed users to view the source code of a program, attempt to access the flag, or exit. Naturally, I decided to peek at the source code first:
{% highlight c %}

  #include <stdio.h>

typedef struct
{
const char *fname;
const unsigned int authlevel;
}FENTRY;

#define NUM_FENTRY 2

const FENTRY flist[]={
{"main.c",3},
{"words.txt",126}
};


void printfile(const char* fname)
{
FILE *file=fopen(fname,"rt");
char c;
while( !feof(file) && (c=fgetc(file))!=EOF ) putchar(c);
fclose(file);
}

int main(void)
{
unsigned int authlevel=5;
char name[32];
int i;
int choice;

printf("Welcome to remote file viewing, guest access mode.\n");
printf("What is your name? ");
fgets(name,34,stdin);
printf("Your authorization level is %03d.\n",authlevel);

for(;;)
{
printf("0: exit\n");
for(i=0;i<NUM_FENTRY;++i)
printf("%d: Level %03d: view \"%s\"\n",i+1,
flist[i].authlevel,flist[i].fname);

if(scanf("%d",&choice)!=1)
{
scanf("%*[^\n]%1*[\n]");
continue;
}

if(choice==0) return 0;

if(choice>NUM_FENTRY)
{
printf("Invalid choice\n");
continue;
}

if(authlevel>=flist[choice-1].authlevel)
printfile(flist[choice-1].fname);
else printf("Error: Authorization level of %03d+ required. "
"Your level is %03d.\n",flist[choice-1].authlevel,
authlevel);

}

return 0;
}

{% endhighlight %}


Immediately I noticed two important features of this code - the choice did not check for negative responses, and fgets() reading in 34 characters to a character array (name) of only 32 characters. Conveniently for this exercise, fname and authlevel were defined consecutively in the struct. This meant that their locations in memory were adjacent, and overwriting the memory would be fairly simple!

In order to overflow the buffer, I tested a long string of 34 'A' characters. This successfully overwrote 'authlevel' with the ASCII character code for 'A', 065. Since the flag needed an authorization level of 126, I used the same ASCII table to lookup the character for 126 which happens to be the tilde character. By filling the buffer with 34 '~' characters, I overwrote the memory location of authlevel and was able to read the flag.


<strong>Difficulty:</strong> 3

<strong>Fun:</strong> 4
