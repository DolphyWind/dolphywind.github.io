---
title: 'Electra: A 2D Language'
date: 2024-03-06T23:19:47+03:00
draft: false
toc: false
images:
tags:
  - programming
  - esoteric
author: "DolphyWind"
---

The first appearance of Electra dates back to 2021. While watching the Truttle1's AsciiDots video, the idea of developing Electra formed in my head. It wasn't anything special, so
I implemented it using simple switch case statements. It was a stack based 2D language with an additional register named "current value". It only had four directions, and a limited
set of instructions. You can still find the legacy Electra on [here](https://github.com/DolphyWind/Small-Codes/tree/master/C%20and%20C%2B%2B/Electra-Legacy). It was very amateurishly
coded, had bad design choices and was very limited, so I moved on to other projects.

Now before going further, let me explain how current Electra works. Electra operates on a two-dimensional grid, it has components, generators and currents. Generators generate
currents at the beginning of the program. On each iteration of the program, the currents move one unit forward, depending on their direction. There are 8 directions: East, NorthEast,
North, NorthWest, West, SouthWest, South, SouthEast. If a current moves onto a component, and that component accepts a current coming from that direction the component works, and
then it clones the current, or it kills it. So it is a challenging language, as you also have to think which component accepts currents from which direction and structure your code according
to that.

<div class="img-with-text">
    <img width="650" src="/content/electra_truth_machine.png" alt="Truth machine in Electra" />
    <p style="font-size: 0.85em; transform: translateY(-7px);" >Truth machine in Electra</p>
</div>


But in late 2022, the idea sparkled again. Mainly because of the components named "portals", I'll talk more about them later on. This time I was more organized, I wanted Electra
to be hard, but not extremely hard. So there were some barriers that I needed to overcome.

The first barrier was the memory, since it is a two-dimensional language, I decided
to use stacks again as opposed to declaring variables or using registers. And since single stack languages are hard to deal with, I decided to make it multi-stacked, so I gave it 64 stacks. "Why 64?"
you might ask, it is completely arbitrary: I wanted a number that wouldn't feel limiting when writing code, and 64 seemed okay. I also used an OOP based approach which
made adding new features and extending the language much easier. 

There was also another big issue: writing similar code over and over again. Although not recommended, in traditional languages this task can usually be accomplished by simply copy-pasting the code.
But it leads to messy code, so they overcome this challenge by having functions.

But my language was two-dimensional, how could I ever implement something like a function? Now, let's think about what
a function does. If you think of an imaginary instruction pointer executing your traditional code line by line -or rather, statement by statement- a function is just something that "teleports" that instruction pointer
to somewhere else. The actual implementation is more complicated than that, as it has to remember where it came from in a FIFO manner. But for intuition, that is a great enough example.

The portals in Electra are analogous to the functions of traditional languages, as in; they teleport currents, the currents remember where they come from in a FIFO manner and thus portals can be called recursively.
The first instance of a portal is marked as the "original portal", every other current that has flown to an unoriginal portal is teleported to the original portal, and when it's reflown to the original portal they teleport back
where they last came from. If a symbol does not have an assigned role in the Electra spec, it is considered a portal. I'm aware that this is somewhat of a bad design choice because if you add new components,
you may break existing code, but I decided to go with it anyway, since I don't expect people writing corporate code with Electra.

After implementing the language, I made two Reddit posts ([P1](https://www.reddit.com/r/programming/comments/12ok7r4/electra_the_esolang_where_you_code_like_an/), [P2](https://www.reddit.com/r/ProgrammingLanguages/comments/12omegv/electra_the_esolang_where_you_code_like_an/)).
I made these posts somewhat late at night, so I went to sleep, expecting them to get at most 10 to 20 upvotes and maybe a couple of stars on GitHub. I couldn't be more wrong, both of them got a good amount of attraction
and now the repo has 97 stars. I got a lot of positive reactions, with a fair amount of criticism. The criticism was because of the phrase I've used for the language,
"The language where you code like an Electrician", is somewhat misleading, because the paradigm has nothing to do with electrical engineering, it is just that your code looks like an electrical circuit. But,
again I wasn't expecting it to get a lot of attention, so it was a phrase I arbitrarily and quickly came up with, without putting many thoughts. Nonetheless, the overall reaction I got was pretty positive, and it made my day.

After a couple of months, I randomly decided to write a Brainfuck interpreter in Electra. It took me a weekend and the funny part is I am not sure if it has a bug or not. It is painfully slow, so
the "bug" could be a case of not waiting long enough to finish its execution. To give an idea of how slow it is, the Brainfuck code that prints first 100 squares executes in about an hour on my machine.
I am planning to implement the visual mode, a mode that allows you to see your code, memory layout, logs etc. to better debug an Electra code. I might implement it using ncurses, or I could use a TUI
library as well. After implementing it, I might add some GIFs to this post. [Here's](https://github.com/DolphyWind/Electra-Lang/blob/master/examples/brainfuck_interpreter/brainfuck.ec) a link to the code.

<div class="img-with-text">
    <img width="650" src="/content/electra_bf.png" alt="BF" />
    <p style="font-size: 0.85em; transform: translateY(-7px);" >A random part of the brainfuck interpreter</p>
</div>


Update: I identified the "bug". It was not a bug but rather the stdin buffer limit... Well, at least I'm not going to lose my sanity by debugging it again. As for the visual mode, it is still unimplemented.
I am planing to write a curses wrapper first, since none of the TUI libraries I've found give me the full control and abstraction I desire. Unfortunately for now both tasks are really time-consuming for me.
