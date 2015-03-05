---
layout: post
title: "sCTF 2015 Q1 - Overflow Tutorial"
description: ""
category: Tutorial
tags: [CTF, Beginner,Buffer Overflow]
---
{% include JB/setup %}
This problem made for a great introduction to beginner-level buffer overflows in C through an improper fgets(). 
###Overflow

{% highlight text %}
Connect to the server with:

nc 104.236.255.49 12341
{% endhighlight %}

Upon connection to the server, a prompt appeared for a username. After entering a username, a simple menu appeared which allowed users to view the source code of a program, attempt to access the flag, or exit.
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
