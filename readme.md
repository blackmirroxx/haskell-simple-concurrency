# Haskell concurrency by example

This tutorial will introduce you to simple mechanisms for concurrency in Haskell.
It was inspired by the concurrency-related chapters of [Go by Example](http://gobyexample.com), which I found to be a great reference to Go's concurrency primitives.
You can follow along with [the tutorial](./src/tutorial.md), clone this repository and run the code locally, or open it up [in FP Complete's online Haskell IDE](https://www.fpcomplete.com/user/eightyeight/concurrency-by-example) to edit and run the code yourself.

I wrote this to:

 1. Learn more about Go's concurrency primitives by translating them.
    Go is frequently praised for its built-in channels and goroutines, so I was naturally interested.
    But at the same time, I'd like to see how we can achieve similar results in Haskell.
 2. Learn more about Haskell's concurrency capabilities, and hopefully teach you about them, too.
    I haven't had much cause to use them, so I'm keen to get my hands dirty and solidify my knowledge.
 3. Hopefully reach out to interested non-Haskellers who may not know about some of these features.
    Ah yes, my secret motives are revealed.

## Running the code

If you've cloned this repository to run locally, once you have Stack, or plain GHC/Haskell platform installed, you can run any of the example files by entering, for example,

    $ stack runhaskell Threads.hs

at the command-line.
You can also open modules in GHCI to play around with them in a REPL:

    $ stack ghci
    > :load src/Threads.hs
    > main

Note that you cannot compile the example files directly, but I have provided a `Main.hs` file which runs all the examples, and which can be compiled into an executable if you wish. The program stack is part of "The Haskell tool stack" and can be installed seperately. Stack is a hidden dependacy, but get involved indirectly. 

    $ ghc --make -threaded Main.hs
    $ ./Main

## A brief word on syntax

As a Haskeller learning Go, I found myself regularly forgetting that `<-` and `->` have different meanings in the two languages.
In Haskell, `<-` is a generic operator called _bind_ which runs some sort of action and stores the result in a variable (_binds_ it).
`->` is used in anonymous functions, e.g. `\x -> x + 1`, and in type signatures, like `Int -> Int`.
In Go, both of these operations refer specifically to channels, as far as I'm aware.

## Further reading

This tutorial has covered some of the basic concurrency primitives available in Haskell/GHC, but I've stayed away from mentioning any of the other resources out there, or libraries you could use to simplify your code and amplify its power.
So, I'll do that now.

For a far more in-depth look at a variety of techniques and libraries for doing concurrency and parallelism in Haskell, [Parallel and Concurrent Programming in Haskell](http://community.haskell.org/~simonmar/pcph/) is the authority, and is available for free online!
The book is written by the author of both the [async](https://hackage.haskell.org/package/async) package and GHC's parallel runtime itself.

If you're keen to use channels in your application, then you might want to take a look at the [unagi-chan](https://hackage.haskell.org/package/unagi-chan) library, which provides super-performant channels, and even has directed channels built-in.

And if you want a higher level of composable concurrency, then [stm](https://wiki.haskell.org/Software_transactional_memory) is for you.
It stands for software transactional memory, and it's all the rage these days.
This wouldn't be a Haskell tutorial if I didn't link you to a research paper, so [here's](http://research.microsoft.com/pubs/67418/2005-ppopp-composable.pdf) the classic paper introducing Haskell's implementation of STM.
Trust me, it's a pretty easy read!

The [pipes-concurrency](https://hackage.haskell.org/package/pipes-concurrency) library allows you to build up dynamic networks of concurrent activities.
