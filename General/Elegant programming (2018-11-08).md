Elegance is not limited to people, cloths or objects. It can be applied to any creative process.  
In programming, elegance is a way to design software with both simplicity, efficiency, expressivity and power.

## What is the contrary of elegant programming ? Ugly programming !

We can learn a lot from bad things/examples. So let’s face them.

We all have seen ugly programs one day. Many of us even have had to work with ugly source code, and know that can be a nightmare.

Ugly coding can easily be detected:

-   **Functions are veeeeeery long**.  
    Why would the original author split its code in clearer small parts when he can aggregate every functionality to the same huge function ?
-   **Source files are very long too**.  
    They usually contain a dozen classes or more. Not even related, of course.
-   **There are no commentaries in the code**.
-   **There is no documentation files either**.  
    Who needs that ? It’s more productive to write code only, isn’t it ?
-   **Cryptic coding style**.  
    The author doesn’t mind if you spend an hour trying to “decode” every function, or every line. Anyway he thinks nobody will be good enough to understand his marvelous code, and nobody deserves that (I agree the latter point, we don’t deserve _that_ !).
-   **Names are somewhat cryptic too**.  
    Such as a, or getdecabsvalofthat. Or even TIWIM (for This Is What I Meant).
-   **Many portions of code are duplicated**. Usually with errors on updates.  
    The author wrote a piece of code, duplicated it somewhere else (rather than making a function) then updated the first portion and forgot to update the second portion accordingly.
-   **Some constructions/instructions are very unusual and strange**.  
    Maybe the author tried to optimize his code, or used some tricks he likes much. Unfortunately, it is not maintainable, or even understandable.
-   **The author writes 1000 lines of code** when 50 would have been enough.  
    An ugly code should always be a lot more complex, inefficient and mysterious than necessary.
-   **Errors/exceptions occur at any moment**, without clear explanation or justification. Typically, the program just crashes silently.
-   **The author included external libraries** that nobody knows and that are not maintained for many years by their respective authors.  
    Guess who will have to write a replacement ?
-   **The programming language is esoteric**.  
    You will have to learn it, whether you like it or not. Even if you rewrite the software, you need to understand the original source code anyway.
-   **The whole structure of the software is a mess**.  
    You don’t understand how it works, how the different parts work together, or even what every part does/represents.  
    In fact, 6 months after having written it, the author himself already forgot how this mess works.

In general, an ugly source code is written fast, without taking into account the future (next programmers, next company, evolution), and is not focused on quality.  
Then you can directly throw it into the dustbin.

## The principles of elegant programming

### The right language(s)

A software is expressed in various kinds of languages:  
programming languages (C#, Java), data languages (XML),  
graphical languages (UML representation, trees, graphs),  
tactile languages ([braille](https://en.wikipedia.org/wiki/Braille) that you read using your hands),  
and even audio languages (vocal synthesis, alarms and any sound that has a specific meaning).

About the programming language, you have to choose one that satisfies several rules:

-   **Modern**.  
    If you choose a language that has been created 30 years ago, please don’t complain it does not allow modern programming techniques (without ugly tricks or external libraries).
-   **Well-known**.  
    If the language you choose is known by only 1% of the developers, who will be able to work on it (now and later) ? It may even disappear after a few years, whatever it’s a good language or not.
-   **Well-designed**.  
    Too many languages are designed by half-amateurs, and mainly gained popularity due to useful libraries or good advertising/propaganda. A badly designed language leads to a badly designed program.  
    You need good tools, and good languages, in order to build great software.
-   **Adapted**.  
    Most languages, although relatively generalist, are in fact focused on one programming field: operating systems, desktop applications, mathematical libraries, web, mobile applications, real-time, embedded platforms..

Some rules can be contradictory. A good modern language may be not well-known, and a well-known language can be too old or badly designed.

An important point: every programmer has a favorite language, and tends to choose or even impose it for any project. Although that’s a common human behavior, it can be in opposition with these rules.

### Simplicity

Some people confuse simplicity and simplism.  
Simplicity does not imply power reduction.  
It implies direct ways to do things.

For example, **duplication** is something we learned to fight, in the programming field.  
Experience showed us that duplication leads to defects, confusions and difficulties of maintenance.

We need to make things as simple and clear as possible. The principle has to do with **simplification in mathematics**: expressing something in a shorter and clearer way, preserving the exact meaning.

### Efficiency

-   **Confusion** reduces efficiency.
-   **Ambiguity** makes the reader waste time trying to figure out what something really is/expresses.
-   **Synonym**:  
    When something specific is made/expressed/declared in several ways, this always leads to problems.  
    It is confusing: which one should we choose ? Why ? Is there different ways ?

Let me give you an analogy: in a natural language, sometimes several words can express the same meaning. In short, they are synonyms.  
When I propose to remove some of these words, some people are shocked and claim that would reduce the richness of the language. They confuse the number of words of this language and the number of meanings this language can express.  
Would it be useful to be able to express the idea of a house using 1000 different words ? Obviously no, if all these words express the very same meaning.

In natural languages though, words are rarely real synonyms: their meaning is close but their context is somewhat different.  
Nevertheless, in an artificial language, we should tie every meaning to one word and only one word. That is how programming languages work, and that avoids confusions.

The same comes with code structures: one meaning should be tied to one class or one library.  
And only one, so we avoid ambiguities at the same time (a class must not express two meanings).

### Expressivity

Elegance is clearly incompatible with unreadable languages or declarations/expressions.

Someone made a good example by inventing the [brain fuck](https://en.wikipedia.org/wiki/Brainfuck) programming language: even if it has not been specifically designed to be unreadable, the concept leads to something mostly incomprehensible.

**Concept 1**:  
A good expressivity is when someone that ignores the language can guess the meaning of the code.

**Concept 2**:  
A good expressivity is when someone who knows the language understands the code in seconds.

The expressivity also depends on the reader’s culture.  
For example, a mathematician will understand functional programming faster than imperative (procedural) programming.  
So the language, either textual or graphical, should be close to what the reader knows and practices every day.

### Prototypes and old programs must be rewritten

Programming is creating. It is halfway between research and realization.  
So the very first version of a program should be seen as a prototype. Its structure has been in constant evolution during its development, so it needs revision.  
While a product is designed, a stack of decisions and researches slowly grows. The final result is no more elegant because these decisions are usually contradictory.  
The lessons that have been learned need to be synthesized. The best way to do that is to build a new elegant product that applies this new knowledge.

Some computer theories explain how we should plan the software creation. The first theories even tried to convince us it would be possible to calculate everything and set time limits. Unfortunately these models failed completely. Later theories included evolution during the “programming cycle”, and didn’t succeed much more. Some recent theories propose more adaptable management, in place of rigid planning. That seems more realistic.  
Until now, programming is still a creative process. That makes it slightly unpredictable.

The same comes with old programs: successive versions cause ambiguities, unbalanced structures, and heterogeneous programming styles (due to different authors and to the evolution of the programming language).

For all these reasons, it is better to replace the whole program by a new one.

Benefits:  
Writing a new program, you can

-   employ a modern programming language,
-   apply modern programming techniques,
-   use a better design,
-   include new functionalities that were inapplicable to the old program,
-   add new platforms (ex: mobile),
-   build a new team, focused on new aims or working differently.

## Why don’t we always apply elegance rules ?

There are reasons that may explain why so many source codes are more or less ugly, inefficient, badly structured, confuse or undocumented.

-   The **natural tendency of the programmer to write code fast** in order to obtain a visual or concrete result as soon as possible.  
    Documenting, or taking time to build a better structure is more boring than creating something new. Prototypes are more seducing than polished work, because we like creating, not working hard on boring things.
-   **Companies need to comply with unrealistic planning**.  
    Maybe the client is impatient and threats canceling the project at any moment if it takes too long. Maybe other companies are in competition, and the first one that completes a software gets the market. Maybe there is a high pressure from the company’s board.
-   **It’s easier aggregating than restructuring**.  
    In real life, project’s aim can change, features can be added or removed at any moment. Software creation still is barely predictable because the needs evolve along with the development (and the versions).  
    But after a while, restructuring is needed. And nobody likes that.
-   **It’s easier copying than inventing**.  
    Invention requires time, imagination, tests, and prototypes. And nothing guarantees a usable result.
-   **Good structure and elegant programming require experienced developers**.  
    It takes years to learn why programs have deep structural problems and how to write better code.  
    Unfortunately, companies tend to employ young developers only, because they basically think development is just a repetitive task that will be done equally by any programmer. So why would they pay more for an experienced developer ?  
    Would they employ an inexperienced architect to build the highest sky scrapper worldwide ? I don’t think.

Short-term and money considerations, intellectual tendencies, lack of imagination, and ignorance can lead to a project crash. Or to a poor product at least.  
Both developers, managers and investors can be part of these bad decisions. And the whole company may pay for the resulting bad results.

## Conclusion

Elegant programming has great benefits but needs well organized work .. and minds.

How to write elegant code, and get great products ?

-   **One meaning → one expression**.  
    No more, no less.  
    No synonyms, no ambiguities, no duplication.
-   **Define and classify** the concepts, meanings and usages that form your code.  
    They must be clear not only to you, but to any developer who discovers your code as well.
-   **Restructure when needed**.  
    The structure should be revised regularly. Do not hesitate to move things, rename, split or group them in order to keep the code well organized.
-   **Internal documentation**.  
    Both in the source code _and_ in separate documents. Explain not only what things are but what methods you apply too.
-   **Choose the right language**.  
    The one that both allows modern programming, is well-known, is well-designed and fits the project well.
-   **When a product/technique is mature, it’s probably time to replace it**.  
    It will be modern again and adapted to the current or future context/customers.
-   **Project planning** should include time for prototypes, experimentation, code restructurings, and internal documentation.
-   Teams should include **experienced developers** along with younger programmers.

Elegance costs at the beginning, and pays later.  
It’s an investment, and a choice that should be made deliberately and applied continuously.

Elegance is obviously in complete contradiction with the current tendency to rationalize programming, a concept that has always produced poor products and failing projects.

It is up to you to choose the elegance now. I’m sure you will like that. And your customers will, too.