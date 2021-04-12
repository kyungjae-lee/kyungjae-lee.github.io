---
layout: notes
title: "[C Programming] gets(), fgets()"
meta: Important facts about the 'gets' and 'fgets' function
reference: 
category: c-programming
---

## Syntax

```c
char* gets(char *s);
char* fgets(char *restrict s, int n, FILE *restrict stream);

/* Examples */
gets(str);                      /* reads a line from stdin */
fgets(str, sizeof(str), fp);    /* reads a line from fp */
```

## Reading Strings Using gets()

Like scanf(), gets() reads input characters into an array, then stores a null
character. In other respects, however, gets() is somewhat different from
scanf():
- gets() doesn't skip white space before starting to read the string (scanf()
  does).
- gets() reads until it finds a new-line character (scanf() stops at any
  white-space character). In addition, gets() discards the new-line character
  instead of storing it in the array; the null character takes its place.

### Example

```c
#include <stdio.h>

#define STR_LEN 20

int main(int argc, char *argv[])
{
    char str1[STR_LEN + 1];
    char str2[STR_LEN + 1];

    printf("Enter a sentence: ");
    scanf("%s", str1);
    gets(str2);

    printf("%s\n", str1);
    printf("%s\n", str2);

    return 0;
}
```

Input
```text
Enter a sentence: This is a sentence.
```

Output
```text
This
 is a sentence.

```

Description
![scanf-gets]({{site.baseurl}}/img/c-programming/scanf-gets.jpg){:.inline-img-w900}


## Reading Strings Using fgets()

fgets() reads characters from the specified stream until whichever below 
happens first:
- fgets() reaches the first new line character (fgets() stores the new-line
  character along with the other characters.)
    - gets() never stores the new-line character, but fgets sometimes does.
- fgets() has read 'sizeof(str) - 1' characters (suppose 'str' is an array
  passed to the first parameter of fgets())


### Example

```c
#include <stdio.h>

#define STR_LEN 15

int main(int argc, char *argv[])
{
    char str1[STR_LEN + 1];
    char str2[STR_LEN + 1];

    printf("Enter a sentence: ");
    fgets(str1, sizeof(str1), stdin);
    fgets(str2, sizeof(str2), stdin);

    printf("%s\n", str1);
    printf("%s\n", str2);

    return 0;
}
```

Input
```text
Enter a sentence: This is a sentence.
```

Output
```text
This is a sente
nce.

```

Description
![fgets]({{site.baseurl}}/img/c-programming/fgets.jpg){:.inline-img-w900}


## fgets() vs. gets(), Which one to Use?

Use fgets() instead of gets() in most situations because it is safer!

fgets() guarantees that the string being read fits into the array. (gets() may
step outside the bounds of the receiving array.)

