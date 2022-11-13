# Lab Report 4 - Vim (Week 7)

## Part 1

_Task_: Changing the name of the "start" parameter and its uses to "base"

Step to do: Assume we are in the "week6-skill-demo1" directory

`vim DocSearchServer.java<Enter>/start<Enter>cebase<Esc>n.n.n.:wq<Enter>`

_Description_:

* `vim DocSearchServer.java<Enter>`: this is the command line that we need to go into the DocSearchServer.java file by vim. Here is the output:

<img src="1.1.JPG" alt="1.1" width="700"/>

* `/start<Enter>`: this will help us search the term we want. Here, we are looking for a word "start" and click Enter to start a cursor at that position. 

<img src="1.2.JPG" alt="1.2" width="700"/>

* `ce`: this will remove a whole word and start an Insert mode.

<img src="1.3.JPG" alt="1.3" width="700"/>

* `base<Esc>`: this will add a word "base" and click Esc button to log out of the insert mode.

<img src="1.4.JPG" alt="1.4" width="700"/>

* `n.n.n.`: this will go to the next word that we search before, which is "start", and click "." to redo the step `cebase<Esc>` 3 times. 

<img src="1.5.JPG" alt="1.5" width="700"/>

<img src="1.6.JPG" alt="1.6" width="700"/>

<img src="1.7.JPG" alt="1.7" width="700"/>

* `:wq<Enter>`: this will help us save the file, then quit vim and return to the terminal.
