---
layout: second
author: Yan
---

The Best Programming Language for Tech Interviews
-------------

What’s the best programming language for interviews if you are pursuing a software engineer position?

**Python3** (Or generically Python) And I will explain below.

```python
print('Hello World')
```

As a software engineer, I have learned several programming languages at different job positions, I have been interviewed at many companies of different sizes, and I have interviewed many candidates at different levels and backgrounds. The choice of the correct interview language is not a life-or-death matter, per se, but it does make your life much easier before and during tech interviews. So what makes Python3 the best interview language?

## It is easy to learn.

Python is a high level language, and it is closer to English compared to other languages. It is so friendly that a person with no previous programming experience may just pick it up and start coding on day one.

Python is a dynamic language, yet strongly typed. It does not need you to declare a variable before using it, and you do not need to explicitly note the type either. This is a great advantage during time-limited interviews. For example, `d={}` defines a dictionary/hash-table and the key/value can be any types. In addition, it can be expanded into a nested dictionary if needed.
```python
d = {}
d['name'] = 'James'
d['age'] = 23
print(d)
```
## It is easy to read.
Indentation.
Python requires strict indentations to form proper code blocks, instead of curly braces `{}` in some other languages. This mandatory convention reduces a lot of unnecessary symbol clutter and enforces the code to be self-organized into visual blocks, thus makes the code easy to the eyes of both the interviewers and interviewees.
```python
def open_windows(windows):
    for w in windows:
        w.open()
def close_windows(windows):
    for w in windows:
        w.close()
```
## It is well-known
It is important to use a popular programming language the interviewer knows. A tech interview is all about you explaining your coding logic to the interviewer, thus it is most effective when both of you know the same programming language well. Python is ([one of](https://www.tiobe.com/tiobe-index/)?) the [most popular programming language](https://pypl.github.io/PYPL.html), so it is highly likely the person on the other side of the table knows it. Personally I feel every software engineer uses Python at some level, to do some scripting during work or merely for fun.

![Ranks](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*_wSvYKsS4rlJekVx2DBr-w.png)
http://pypl.github.io/PYPL.html

## It is versatile.
Python has rich libraries.
Interviews are performed at certain abstraction level, ignoring uninteresting details. With Python, you can skip a lot of low level details with the utilities in the standard library, and focus your attention onto the core problem itself.

Python is also the major programming language used in [Machine Learning](http://ivyproschool.com/blog/2017/08/21/why-python-is-the-preferred-language-for-machine-learning/) and [Data Science](https://www.cbtnuggets.com/blog/technology/data/why-data-scientists-love-python), thanks to the great library support. Software engineer is a versatile career that people often change their interests and positions during the course. Python can easily fill the bridge because of its own versatility.

## Summary
When you are preparing for interviews, using Python for coding practice helps with fast prototyping and high level understanding of the algorithms.

During an interview, your Python code will be concise and clean, saving you a lot of finger typings and more importantly, saving you a lot of precious brain power.

Hopefully you are now convinced to use **Python3** for your interviews! Good luck!

---

Or not yet? Please read on.

So what are the reasons not using other languages for a tech/code interview?

Under the setting of a tech interview, other languages may have a niche for specialized positions. However, for a _general_ interview, Python3 always wins.

I happen to know some of the most popular programming languages and used a few for my tech interviews before. Maybe I can share some of my opinions and experience.

## C
Great language for system and hardware programming. C built everything, C can do everything. But C is lower level and closer to the metal, which makes it too verbose. For example, parsing a string `"apple, orange"` into two words takes a loop and several variables. Python is one line, plus you do not need to worry about edge cases. C is used only when you interview for hardware or embedded systems positions.

## Java
Great language for big enterprise projects, with thousands of engineers and millions of lines of code. For interviews, it is too verbose with static types and boilerplate code. For example, a Java `Hello World` takes five lines, while Python takes only one line. It would be even messier if you started to define `getter` and `setter` in Java.
Most interviews are language agnostic, but I did get asked specifically to code in Java during some interviews, notably Apple and LinkedIn. Also Dropbox favors Java too, because their interview questions are more towards multithreading, which is unnatural to do in Python because of [Global Interpreter Lock (GIL)](https://wiki.python.org/moin/GlobalInterpreterLock).

## Python2
The world is moving to Python3. There is no benefit to get stuck at Python2.

## C++
It is C on steroids, with much richer libraries and object-oriented programming (OOP) support. However, coding during an interview does not need OOP support at the language level. The verbosity and static typing also suffer. Don’t even think about using template during an interview. A simple nested `unordered_map` would take three whole lines to declare.

## Ruby
Ruby is as cool as python, and was super popular ten years ago with [Ruby on Rails](https://www.netguru.com/blog/is-ruby-on-rails-dead). The only problem is that, as a programming language, Ruby is trending down.

## Groovy
It is Java on steroids, and feels a lot like Ruby. Unfortunately not many companies use it.

## Scala
Scala is the most popular functional language. However, keep in mind that all coding challenges are expected to be solved in imperative paradigm. I did use Scala to interview once, and failed miserably. I found out that I could not edit anything in place, consequently made quick-sort impossible. Of course there are excellent engineers can do it, but not me.

## Swift
Well, of course for iOS engineers.

##JavaScript
For frontend engineers.

## Kotlin
For Android engineers.

My two cents, and good luck.

Q.E.D.

Thank you [Eventbrite](https://www.linkedin.com/company/eventbrite/), for Python and everything!

----
Originally posted at https://medium.com/swlh/the-best-programming-language-for-tech-interviews-e5c77d3946ad
