---
title: 'Taking A Joke To An Extreme'
date: 2025-08-14T20:28:45+03:00
draft: false
toc: false
images:
tags:
  - programming
author: "DolphyWind"
---

[Code Guessing](https://codeguessing.gay/index) is an online social deduction game. On each round there are two phases: the writing phase and the guessing phase. At the beginning of the
writing phase, players are given a specification and expected to write code, that in some shape or form adheres to it. The writing phase, if no extension happens, lasts for a week and after that, all entries are shuffled
and made public. The guessing phase comes after the writing phase, in it each player guesses which entry is written by which player. At the end of a round, players earn 1 point for
each player they guessed correctly and lose 1 point for each player that guessed them correctly. The winner of a round determines the next challenge.

There are all kinds of players: Some get too competitive and impersonate others, pay attention to every single detail of other submissions. Some don't care about the guessing phase and the point system and just focus on solving
the challenge. Some try to write code that is aesthetically pleasing. Players are very well encouraged to show their creativity during the writing phase otherwise it would be a very boring ripoff of leetcode.

My code guessing submissions usually are impersonations (though I stopped doing that once I became less competitive), implementations of algorithms I wanted to try but previously had no reason to, silly jokes or occasional
boring entries. Code guessing offers challenges of every kind. So there is always something different to try.

There are many interesting stories to tell about code guessing. From the time there was a malicious JavaScript entry (the kind that steals your guesses and sends them to a remote server) to the time it turned out the owners
of each code were present in the HTML code of the page and no one noticed it for 58 rounds. On this blogpost I am going to talk about me taking an in-joke to an extreme.

## CG 53: Box Drawing
It was an average round. The challenge was, given a string of unicode characters, named "drawing", figuring out whether it follows the given criterias or not. I submitted a buggy python code, as the
challenge was not that interesting for me. But during the guessing phase, an entry piqued my interest. It was a PICO-8 game cartridge, submitted by olus2000.
[PICO-8](https://www.lexaloffle.com/pico-8.php) is a fantasy console by Lexaloffle. Here's the said entry:
![olus2000's cg53 entry](/content/cg53_olus2000.png)

Yes that png file **is** the cartridge. Anyway, at the moment I thought I found the perfect person to impersonate next round... 

## CG 54: 3D Rendering
CG 54's challenge is still one of my favorites to this day, not just because it started it all but because I genuinely had so much fun coding it. The challenge was to implement 3D rendering. To impersonate olus2000,
I decided to get a copy of PICO-8 and solve the challenge in it.

I decided to have a simple 3D cube on the screen and have 3D camera controls. To implement it, I used the MVP matrix method. How it works is, to find the on-screen coordinate of a given vertex, we multiply it with three special
$4\times 4$ matrices, namely, Model ($M$), View ($V$) and Projection ($P$). "Well, aren't we in 3D? Why are those matrices $4\times 4$?" you might ask, while it is technically possible, turns out each can be represented as a
single $4\times 4$ matrix with the help of [Homogeneous Coordinates](https://en.wikipedia.org/wiki/Homogeneous_coordinates) and easily processed with GPU hardware.

To put it simply, a point in euclidian 3D space with coordinates $(\frac{x}{w}, \frac{y}{w}, \frac{z}{w})$ can be represented as the homogeneous coordinate $(x, y, z, w)$. Usually we care about the case when $w=1$, when it is
"normalized". In short, **model matrix** takes an object from its local coordinate space to world (global) space, the **view matrix** then transforms the scene such that the camera is in the origin, looking along the $z$-axis
(or sometimes $-z$-axis). Finally the **projection matrix** transforms the camera's view frustum into a normalized rectangular prism (in the case of perspective projection).

It turned out to be a bit heavy for the PICO-8 due to rasterization being compute-heavy, but it works well and looks cool in general.
![3d renderer gif](/content/3drenderer.gif)

To my surprise, another player, **kimapr**, has also thought of impersonating olus2000 and submitted a spinning cube in PICO-8.
![Kimapr CG54 gif](/content/kimapr_cg54.gif)

What makes it funnier is that olus2000 did not participate in this round, so we had two impersonators without the impersonatee being present. Impersonating her became an in-joke for a short while.

## CG 56: Reverse Engineer a Regex
The challenge was, given an expression that recognizes a regular language, find a string that is recognized by it. I made a simple recursive descent parser in C but I did not submit that directly.

You see, I *really* liked that in-joke, so I wanted to continue it. In C, there is a feature called "macros". It is essentially a piece of code that gets substituted in the preprocessor pass, before the actual compilation happens.
They are commonly used to get rid of magic numbers but they are much powerful than that. Macros are defined using the `#define` directive and since it is a simple text substitution, they can make your code appear like something
else. You may have seen cursed examples of them usually in the form of memes, something similar to this example
```c
#include <stdio.h>

#define BEGIN int main(){
#define END }
#define SAY puts
#define AND &&
#define OR ||
#define NOT !
#define IF if(
#define THEN ){
#define ELSE }else{
#define FI }
#define REPEAT(n) for(int i=0;i<(n);i++)
#define $ ;

BEGIN
    IF NOT 0 THEN
        REPEAT(3) SAY("Hello, macros!")$ 
    ELSE
        SAY("This shouldn't happen")$
    FI
END
```

After dabbling with C macros for 8+ hours and countless errors later, I turned that beautiful parser C code to this monstrosity:
```c
#include "olus2000.h"

HELLO I AM OLUS2000 AND I WROTE THIS ENTRY. SO MAKE YOUR GUESSES WITH THAT IN MIND.
YOU DON/*'*/T BELIEVE ME? BUT WHY? HAVE I LIED TO YOU BEFORE? PLEASE,
JUST DRAG MY NICK TO THE APPROPRIATE PLACE. YOU WOULDN/*'*/T WANT TO SEE ME SAD WOULD YOU?
YOU STILL DONT BELIEVE ME? FINE... MY FULL NAME IS #### ####. I STUDIED
COMPUTER SCIENCE IN #### #### #### ####. I LOVE PICO8, ESOLANGS, AND
CONCATANATIVE PROGRAMMING. UMM... OH YEAH AND ALSO TOKI PONA. UHH...
IM FROM ####. YOU PROBABLY KNOW IT ALREADY, I JUST WANTED TO POINT IT OUT...
YOU NOW BELIEVE ME, RIGHT? :PLEADING_FACE: I SWEAR, THIS CODE REALLY DOES BELONG TO ME,
I AM NOT IMPERSONATING HIM. AND BY HIM, I MEAN ME OF COURSE. IVE GIVEN A LOT OF PERSONAL
DETAILS SO YOU ARE CONVINCED, R-RIGHT? HAVE A NICE CODE GUESSING
```
<sup><sub>Some parts are censored for privacy reasons</sub></sup>

Yes, that is a C code, a valid C code that reverse engineers a regex. To give you some understanding of it, I'll also provide the first few lines of the `olus2000.h` file.
```c
#define I
#define ESOLANGS UV Hs){YM l=UP(Hs);YM qq
#define STILL 0:0;TC(!(e->s-124)){TC(T)ep(ME[0],to);QH;}
#define IM ){}THAT pt(P*p){TC(pe(p))QH 0;TC(!ph(p,
#define TJ while
#define IT
#define SM break
#define GN(i,s,m)UQ(i,s,m,1)
#define PLACE ME=a;e->sa*=2;}ME[T]=s;++T;}EA th(){B b;b
#define WANT )QH;ek(ME[j]);GN(i,j,T-1){
#define OO free
#define HAVE 0:0;
#define PICO8 QH 0;QH(!(c-pu(p)));}YM ph(P*p
// ...
```

Having a paragraph of text as code is actually pretty trivial by getting the entire code on one line and making the first word to expand to it, but I wanted it to be as much cryptic and scary as possible. So instead the
text and the code evolved together.

When I started making it, my initial plan was to ignore the punctuation alltogether but then I realized I can keep almost all of the punctuation and have my code still compile. For example in C, you can use triple dots to represent
variadic arguments for a function. So each time you see them the previous word ends with an unfinished function definition and the next word completes it. The colon and question mark is possible thanks to ternary expressions and
so on. I even have a `:PLEADING_FACE:` there.

After finishing my craft, I submitted it and took a deep breath. I performed really good on the guessing phase. After getting April Fools'd before the round started (thank you LyricLy) I made it up for it by getting the first
place and having my challenge be the next one.

## More..?
The C code above is already on another level. But I had an idea, what if **everything** was olus2000. So I did what any reasonable person would do, began creating a programming language named olus2000. 

Because she loves concatenative languages, and especially [Forth](https://en.wikipedia.org/wiki/Forth_(programming_language)), I wanted my language to be Forth-like. This decision freed me from focusing on the general structure
of the syntax and wasting my time on stupid decisions.

For a Forth-like language, I needed instructions, better known as "words". Since the characters `0`, `o` and `O` look similar (up to an arbitrary measure of similarity), I wanted each posible
alteration of last three characters of "olus2000" to correspond to a different word. This gives us a total of 27 words, which is enough. 

Numbers are represented in a special ternary-based encoding. First, to begin entering a number you need to switch to either "Number Mode" or "Negative Number Mode" by putting "0lus2000!" or "0lus2ooo!", respectively.
(Looking back at it, the use of the exclamation mark at the end could've been avoided by employing other encoding schemes). When you are in either mode, each term of the form "olus2xyz" represents a group of trits `xyz`, where
`0` means 0, `O` means 1 and `o` means 2. After switching to another mode, these groups are concatenated in the order they appear to form a ternary numeral, which is then interpreted as an integer. Negative number mode makes
this integer negative. To switch to normal mode, use the word "olus2000!". To switch to comment mode use the word "Olus2000!". Strings are put into the quotation marks, and get printed as soon as they are encountered. It is
completely possible to encode them similar to how numbers are encoded but I didn't wanna go that far, mostly because of my own laziness.

The specification of the language seemed good, and it is not that hard to implement. But unfortunately, there is one, rather big issue with the language: it is **very** unintuitive. That's the price we pay for having almost
everything be a variation of the word "olus2000". This issue also makes it near impossible to write a program that is only slightly complex. I have to use it in a code guessing round, mind you. In its current state, 
it seems like we're not gonna be able to use the language. Seems like I have only two options: pour hours to write a simple program and probably lose your mind over a single mistake or abandon the idea. What else there could
be to do?

## Meet Torth
Torth is a Forth-like esoteric programming language. It stands for "Ternary Forth". It exclusively allows ternary numbers in its syntax. Wait a second, what does this have to do with the language above again? 

When I ended the paragraph with "It seems like I have only two options" I wasn't being honest. Because in the past, people have already solved a similar problem. When machine code was too hard to program by hand, people created
assembly languages and assemblers. When that was too hard to deal with, they created modern programming languages. I'm sure you start to see where this is heading to. To remedy the core issue of olus2000, I created another language,
Torth, that is purposefully kept as similar to olus2000 as possible, but at the same time, it makes sense and transpiles to olus2000. Here's a simple 99 bottles of beer on the wall program in Torth:
```
: WRITE_9 IF DROP "ERROR" ELSE DROP "9" THEN ;
: WRITE_8 IF 1 - WRITE_9 ELSE DROP "8" THEN ;
: WRITE_7 IF 1 - WRITE_8 ELSE DROP "7" THEN ;
: WRITE_6 IF 1 - WRITE_7 ELSE DROP "6" THEN ;
: WRITE_5 IF 1 - WRITE_6 ELSE DROP "5" THEN ;
: WRITE_4 IF 1 - WRITE_5 ELSE DROP "4" THEN ;
: WRITE_3 IF 1 - WRITE_4 ELSE DROP "3" THEN ;
: WRITE_2 IF 1 - WRITE_3 ELSE DROP "2" THEN ;
: WRITE_1 IF 1 - WRITE_2 ELSE DROP "1" THEN ;
: WRITE_0 IF 1 - WRITE_1 ELSE DROP "0" THEN ;
: WRITE_HELPER DEPTH IF DROP 1 + IF 1 - ELSE DROP WRITE_0 WRITE_HELPER THEN ELSE DROP THEN ;
: WRITE_NUM IF DUP 101 % SWAP -1 SWAP 101 / WRITE_NUM ELSE DROP WRITE_HELPER THEN ;

: BOTTLES DUP 1 - IF DROP "bottles" ELSE DROP "bottle" THEN ;

: LAST_LINE DUP IF WRITE_NUM ELSE DROP "No more" THEN " " BOTTLES " of beer on the wall.\n\n" ;
: BEER_REGULAR DUP WRITE_NUM " " BOTTLES " of beer on the wall,\n" DUP WRITE_NUM " " BOTTLES " of beer.\nTake one down, pass it around\n" 1 - LAST_LINE ;

: BEER DUP IF BEER_REGULAR BEER THEN ;

10200 BEER
```

The first few lines are for printing ternary numbers in decimal. The rest of the code looks like an average Forth-like language. Here's the same code compiled to olus2000:
```
olus2oOo WRITE_9 olus2o0O olus2OoO "ERROR" olus2o0o olus2OoO "9" olus2oO0 olus2oo0 olus2oOo WRITE_8 olus2o0O 0lus2000! olus200O olus2000! olus20O0 WRITE_9 olus2o0o olus2OoO "8"
olus2oO0 olus2oo0 olus2oOo WRITE_7 olus2o0O 0lus2000! olus200O olus2000! olus20O0 WRITE_8 olus2o0o olus2OoO "7" olus2oO0 olus2oo0 olus2oOo WRITE_6 olus2o0O 0lus2000! olus200O
olus2000! olus20O0 WRITE_7 olus2o0o olus2OoO "6" olus2oO0 olus2oo0 olus2oOo WRITE_5 olus2o0O 0lus2000! olus200O olus2000! olus20O0 WRITE_6 olus2o0o olus2OoO "5" olus2oO0
olus2oo0 olus2oOo WRITE_4 olus2o0O 0lus2000! olus200O olus2000! olus20O0 WRITE_5 olus2o0o olus2OoO "4" olus2oO0 olus2oo0 olus2oOo WRITE_3 olus2o0O 0lus2000! olus200O olus2000!
olus20O0 WRITE_4 olus2o0o olus2OoO "3" olus2oO0 olus2oo0 olus2oOo WRITE_2 olus2o0O 0lus2000! olus200O olus2000! olus20O0 WRITE_3 olus2o0o olus2OoO "2" olus2oO0 olus2oo0 olus2oOo
WRITE_1 olus2o0O 0lus2000! olus200O olus2000! olus20O0 WRITE_2 olus2o0o olus2OoO "1" olus2oO0 olus2oo0 olus2oOo WRITE_0 olus2o0O 0lus2000! olus200O olus2000! olus20O0 WRITE_1
olus2o0o olus2OoO "0" olus2oO0 olus2oo0 olus2oOo WRITE_HELPER olus2o00 olus2o0O olus2OoO 0lus2000! olus200O olus2000! olus200o olus2o0O 0lus2000! olus200O olus2000! olus20O0
olus2o0o olus2OoO WRITE_0 WRITE_HELPER olus2oO0 olus2o0o olus2OoO olus2oO0 olus2oo0 olus2oOo WRITE_NUM olus2o0O olus2OOo 0lus2000! olus2O0O olus2000! olus20o0 olus2Oo0 0lus2ooo!
olus200O olus2000! olus2Oo0 0lus2000! olus2O0O olus2000! olus20Oo WRITE_NUM olus2o0o olus2OoO WRITE_HELPER olus2oO0 olus2oo0 olus2oOo BOTTLES olus2OOo 0lus2000! olus200O
olus2000! olus20O0 olus2o0O olus2OoO "bottles" olus2o0o olus2OoO "bottle" olus2oO0 olus2oo0 olus2oOo LAST_LINE olus2OOo olus2o0O WRITE_NUM olus2o0o olus2OoO "No more" olus2oO0
" " BOTTLES " of beer on the wall.\n\n" olus2oo0 olus2oOo BEER_REGULAR olus2OOo WRITE_NUM " " BOTTLES " of beer on the wall,\n" olus2OOo WRITE_NUM " " BOTTLES
" of beer.\nTake one down, pass it around\n" 0lus2000! olus200O olus2000! olus20O0 LAST_LINE olus2oo0 olus2oOo BEER olus2OOo olus2o0O BEER_REGULAR BEER olus2oO0 olus2oo0
0lus2000! olus20O0 olus2o00 olus2000! BEER 
```

## CG 64: Look And Say Sequence
Finally, the opportunity to use olus2000 has struck! The [look and say sequence](https://oeis.org/A005150) is an integer sequence where the next number is obtained by "describing" the digits of the current number. It starts
with $1$, and continues with $11, 21, 1211, \dots$. The challenge for CG 64 was to generate this sequence.

I started off by implementing the challenge in Torth.
```
: PRINT_3 IF DROP "ERROR" ELSE DROP "3" THEN ;
: PRINT_2 IF 1 - PRINT_3 ELSE DROP "2" THEN ;
: PRINT_1 IF 1 - PRINT_2 ELSE DROP "1" THEN ;
: PRINT_NUM 1 - PRINT_1 ;

: PRINT_STACK (For debug purposes) DEPTH IF DROP "[ " . " ]\n" PRINT_STACK THEN ;

: OPERATE_BODY
    DUP ROT SWAP DUP ROT == 
    IF
        DROP 0 GET 1 + 0 SWAP SET DROP
    ELSE
        DROP DUP 0 SWAP SET 0 1 SET SWAP DROP
    THEN
;

: OPERATE
    SWAP DUP -1 !=
    WHILE
        DROP SWAP OPERATE_BODY SWAP DUP -1 !=
    THEN
    DROP SWAP DROP DROP
;

: STEP
    OPERATE REVERSE DEPTH
    WHILE
        SWAP DUP PRINT_NUM 0 SWAP SET 1 -
    THEN "\n" DROP -1 REVERSE 0
;


(Initial state of the stack) -1 1 0
(Print 1) 1 PRINT_NUM "\n"
(Print the look and say sequence indefinitely) 1 WHILE DROP STEP 1 THEN
```

Then transpiled it to olus2000, gave it a nice shape and ended up with this:
```
                      "" olus2oOo OLUS2OOO "" ""                            olus2o0O olus2OoO                                     "ERROR" olus2o0o                  olus2OoO "3" olus2oO0          olus2oo0 olus2oOo OLUS2ooo olus2o0O 0lus2000!                    olus200O olus2000! olus20O0 OLUS2OOO olus2o0o olus2OoO "2"          olus2oO0 olus2oo0 olus2oOo OLUS2000 olus2o0O ""          0lus2000! olus200O olus2000! olus20O0 OLUS2ooo           olus2o0o olus2OoO "1" olus2oO0 olus2oo0 olus2oOo
                 OLUS200O 0lus2000! olus200O olus2000!                      olus20O0 OLUS2000                                     olus2oo0 olus2oOo                 OLUS20O0  "" olus2OOo          olus2Ooo olus2Oo0 olus2OOo olus2Ooo olus2O00                     olus2o0O olus2OoO 0lus2000! olus2000 olus2000! "" olus2ooO          0lus2000! olus200O olus2000! olus200o 0lus2000!          olus2000 olus2000! olus2Oo0  olus2ooo olus2OoO           "" olus2o0o olus2OoO olus2OOo 0lus2000! olus2000
            olus2000! olus2Oo0 olus2ooo 0lus2000! olus2000                  olus2000! 0lus2000!                                   olus200O olus2000!                olus2ooo olus2Oo0  ""          olus2OoO olus2oO0 olus2oo0 olus2oOo OLUS20OO                     olus2Oo0 olus2OOo 0lus2ooo! olus200O olus2000! olus2O0O ""          olus2oOO olus2OoO olus2Oo0 OLUS20O0 olus2Oo0 ""          olus2OOo 0lus2ooo! olus200O  olus2000! olus2O0O          olus2oO0 olus2OoO olus2Oo0 olus2OoO olus2OoO  ""
         olus2oo0 olus2oOo OLUS20Oo OLUS20OO olus2OOO olus2o00              olus2oOO olus2Oo0                                     olus2OOo OLUS200O                 "" 0lus2000! olus2000          olus2000! olus2Oo0 olus2ooo 0lus2000! olus200O                   olus2000! olus20O0 olus2oO0 "\n" olus2OoO "" "" 0lus2ooo!           olus200O olus2000! olus2OOO 0lus2000! olus2000           olus2000! olus2oo0 0lus2ooo! olus200O olus2000!          0lus2000! olus200O olus2000! 0lus2000! olus2000
       olus2000! "" 0lus2000!             olus200O olus2000! ""             OLUS200O " \n" ""                                     0lus2000! olus200O                olus2000! olus2oOO ""          olus2OoO OLUS20Oo                                                                                        0lus2000! olus200O          olus2000! olus2oO0          olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 " " olus2000                  olus2000 "" olus2000            olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "          olus2000 olus2000                                                                                        olus2000 olus2000           olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "          olus2000 olus2000                                                                                        olus2000 olus2000           olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "          olus2000 olus2000                                                                                        olus2000 olus2000           olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "          olus2000 olus2000                                                                                        olus2000 olus2000           olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "          olus2000 olus2000                                                                                        olus2000 olus2000           olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "          olus2000 olus2000                                                                                        olus2000 olus2000           olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "          olus2000 olus2000 olus2000 olus2000 olus2000                     olus2000 olus2000 olus2000 olus2000 olus2000 olus2000 " "           olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "          olus2000 olus2000 olus2000 olus2000 olus2000                     olus2000 olus2000 olus2000 olus2000 olus2000 olus2000 " "           olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "          olus2000 olus2000 olus2000 olus2000 olus2000                     olus2000 olus2000 olus2000 olus2000 olus2000 olus2000 " "           olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "          olus2000 olus2000 olus2000 olus2000 olus2000                     olus2000 olus2000 olus2000 olus2000 olus2000 olus2000 " "           olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "          olus2000 olus2000 olus2000 olus2000 olus2000                     olus2000 olus2000 olus2000 olus2000 olus2000 olus2000 " "           olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "                                     olus2000 olus2000                     olus2000 olus2000                                                   olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "                                     olus2000 olus2000                     olus2000 olus2000                                                   olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "                                     olus2000 olus2000                     olus2000 olus2000                                                   olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "                                     olus2000 olus2000                     olus2000 olus2000                                                   olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 olus2000 ""                    olus2000 olus2000 ""           olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "                                     olus2000 olus2000                     olus2000 olus2000                                                   olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
     olus2000 " " olus2000                  olus2000 "" olus2000            olus2000 olus2000                                     olus2000 olus2000                 olus2000 olus2000 " "          olus2000 olus2000 olus2000 olus2000 olus2000                     olus2000 olus2000 olus2000 olus2000 olus2000 olus2000 " "           olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
       Olus2000! "" 0lus2000!             olus200O Olus2000! ""             olus2000 olus2000 olus2000 olus2000 olus2000          olus2000 olus2000                 olus2000 olus2000 " "          olus2000 olus2000 olus2000 olus2000 olus2000                     olus2000 olus2000 olus2000 olus2000 olus2000 olus2000 " "           olus2000 olus2000           olus2000 Olus2000!           olus2000 olus2000            olus2000 olus2000           olus2000 olus2000            olus2000 Olus2000!!
         olus2oo0 olus2oOo OLUS20Oo OLUS20OO olus2OOO olus2o00              olus2000 olus2000 olus2000 olus2000 olus2000           olus2000 olus2000               olus2000 olus2000 " "           olus2000 olus2000 olus2000 olus2000 olus2000                     olus2000 olus2000 olus2000 olus2000 olus2000 olus2000 " "           olus2000 olus2000 Olus2000! olus2000 Olus2000!           olus2000 Olus2000! Olus2000! olus2000 olus2000           olus2000 Olus2000! Olus2000! olus2000 Olus2000!!
            Olus2000! olus2Oo0 olus2ooo 0lus2000  olus2000                  olus2000 olus2000 olus2000 olus2000 olus2000             olus2000 olus2000 "" "" ""  olus2000 olus2000 " "             olus2000 olus2000 olus2000 olus2000 olus2000                     olus2000 olus2000 olus2000 olus2000 olus2000 olus2000 " "           olus2000 olus2000 Olus2000! olus2000 Olus2000!           olus2000 Olus2000! Olus2000! olus2000 olus2000           olus2000 Olus2000! Olus2000! olus2000 Olus2000!!
                 OLUS200O 0lus2000! olus200O Olus2000!                      olus2000 olus2000 olus2000 olus2000 olus2000                 olus2000 olus2000 "" olus2000 olus2000 " "                olus2000 olus2000 olus2000 olus2000 olus2000                     olus2000 olus2000 olus2000 olus2000 olus2000 olus2000 " "           olus2000 olus2000 Olus2000! olus2000 Olus2000!           olus2000 Olus2000! Olus2000! olus2000 olus2000           olus2000 Olus2000! Olus2000! olus2000 Olus2000!!
                      "" olus2oOo OLUS2OOO "" ""                            olus2000 olus2000 olus2000 olus2000 olus2000                     olus2000 olus2000 olus2000                            olus2000 olus2000 olus2000 olus2000 olus2000                     olus2000 olus2000 olus2000 olus2000 olus2000 olus2000 " "           olus2000 olus2000 Olus2000! olus2000 Olus2000!           olus2000 Olus2000! Olus2000! olus2000 olus2000           olus2000 Olus2000! Olus2000! olus2000  olus2000!
```

The name of the file is, of course, `olus2000.olus2000`. Actual code occupies the first few lines, the rest is a one giant comment. You can view the specification of [olus2000](https://esolangs.org/wiki/Olus2000) and [Torth](https://esolangs.org/wiki/Torth)
by clicking the respective links. And for the implementation of Torth, click [here](https://github.com/DolphyWind/esoteric/tree/master/torth).

I tried to make it look like someone is impersonating me by creating a new [esolangs.org](https://esolangs.org/) account and naming it "Dolphy" (my main account is named "DolphyWind"). It didn't work at all, even though I guessed
six people correctly that round, four other people have guessed me and I ended the round with a total of $2$ points. I don't really care about it, what I did satisfied me enough.
