# littleDB
Little database written in C.  
Part of the code is taken from https://cstack.github.io/db_tutorial .  
What I did was:
- implementing few features
- understand the b-tree algorithm
- make some fixes and solve some warnings
- trying to organize the code in a COBOL way, given my recent experience with it.
For more info read my article about it: https://medium.com/@alessandrotambellini03/my-experience-migrating-legacy-code-985b63841363

Another thing that I tried to implement was the management of kill signals. 
But it failed :(

## B-tree
B-tree is the ds used to represent tables and indexes.
For indexes it is used a variant called **B+ tree**   
Explanatory videos:
- https://www.youtube.com/watch?v=K1a2Bk8NrYQ
- https://www.youtube.com/watch?v=NI9wYuVIYcA

Correlated:  
`const uint32_t PAGE_SIZE = 4096;`
It is the same size of a page used in the virtual memory of most computer architectures. 
This means one page used in littleDB corresponds to one page used by the OS. 
So, given this correspondence, the OS will move pages in and out of memory as whole units instead of breaking them up.

## Management of Kill Signals
My initial idea was to close elegantly the db file and then exit the program 
if the user types ^C or ^\\. But I was not able to structure safe code or code that I fully understand.  
More info at:
- https://www.reddit.com/r/C_Programming/comments/y0k9lp/how_to_use_a_signal_handler_to_run_cleanup/
- https://stackoverflow.com/questions/6970224/providing-passing-argument-to-signal-handler

So, the program can be nicely stopped just with the `.exit` command. 
Otherwise the changes of the current session are lost.

## Single file
I wrote all the code into a single `main.c` file for 2 reasons:
- I recently downloaded **MS-DOS** v1.25 where the entirity of the code is written in few files: https://github.com/microsoft/MS-DOS/tree/main/v1.25
- During [my last internship](https://medium.com/p/985b63841363/edit) I worked with Java and **COBOL** that are the opposite in terms of code structure paradigm: OOP vs Procedural. 
In Java, I was maybe thinking too much on how to structure the different classes, while in COBOL a program was written in a single huge file. So, I wanted to try this second approach.

### Run
To run the program, you can:
- Go to the **Run and Debug** section of VSCode 
and use `.vscode > tasks.json` and `.vscode > launch.json`
- Do it manually. So, first compile it with
    `gcc -std=c11 -Wall -Wextra main.c -o main.out`  
    and then run it with `./main.out db`
