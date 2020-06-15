# Golang in London - Music Player

Hello and welcome to the first, live-coding session with Golang in London!

Today we'll build a simple music player in the terminal, using amazing [beep](github.com/faiface/beep) library. And, of course, all using Go!

If you will ever get lost or will want to redo the whole workshop alone - follow the tutorial below. Also, use [CHEAT.md] if you need a reference to basics of Go. Let's roll!

## Table of Contents

<a name="top">

* [Intro](#intro)
* [Local setup](#local-setup)
* [App setup](#app-setup)
* [The App itself](#app-itself)
* [How to improve](#improve)
* [About the author](#about)

[^Top](#top)

<a name="intro"/>

## Intro

If you're here, you most probably know what Go is and why we use it. In case you need a refresher:

**Go** (or known also as **golang** - because of it's web domain) is a statically typed, compiled programming language designed at Google by Robert Griesemer, Rob Pike and Ken Thompson. Released in late 2009, it took the programming scene by a storm.

Why **Go** you might ask?

* Language spec for Go is 50 pages - where Java's is around 770 pages;
* Genius standard library that allows to create production-ready apps out-of-the-box
* Extremely well designed concurrency using *goroutines*
* Garbage collection optimized for low latency
* Great documentation
* Excellent tooling, again, out-of-the-box
* Fast compile times
* Very stable library, with a strict compatibility promise that all Go 1 programs will run unchanged on later versions of Go 1.x
* Heavily used in cloud tools - from Docker to Dropbox
* Very desired - according to StackOverflow's 2019 survey, it's the third most wanted programming language

[^Top](#top)

<a name="local-setup"/>

## Local Setup

Installing Go is really fun, quick and straightforward. First, check [Getting Started](https://golang.org/doc/install) and get the distribution from [Downloads](https://golang.org/dl/). 

Once that's done, open your terminal and check if Go is installed properly:

```
go version
```

That should return:

```
go version go1.14 darvin/amd64
```

> Bear in mind - the last part depicts the system and processor architecture - I'm on Mac, so if you're using anything else - it'll be different for you.

Ok, we got Go running, let's setup the directory for our app. Create a folder in your work directory called `Music-Player` and let's roll with this!

> I'm an avid fan of terminal and Vim - so everything from this point now on will refer to terminal actions. If you don't want to go so deep, feel free to use any IDE you want! (Actually, VSCode have amazing support for Go!)

[^Top](#top)

<a name="app-setup"/>

## App Setup

Navigate to your work directory and enable Go modules. Type in your terminal:

```
export GO111MODULE=on
```

What are **Go modules**? Go Modules is the way how Go manages it's dependencies. Once we have that, let's initialize the modules. In your terminal type:

```
go modules init music-player
```

That will create a new file called `go.mod` which will take care of any dependencies we will need!
That takes care of the whole setup part - let's roll with the code!

[^Top](#top)

<a name="app-itself"/>

## The App Itself

There's a few reasons why I've decided to write a small CLI for playing music:

* We will use a great [beep](github.com/faiface/beep) library for handling the streaming
* We will learn how to handle the errors and how to use `defer` keyword
* We will learn how to use `goroutines` and `channels`

That said, let's crack the code down! First thing we need to create is the file itself. In the terminal type:

```
touch main.go
```

`main.go` is the file in which we'll write the whole logic for the app. We can divide the application into five steps:

* Set up imports
* Open the file
* Prepare the streamer
* Set up speaker
* Play the file

### Set up imports

Open the file and type below:

**main.go**
```go
package main

import (
  "log"
  "os"
  "time"

  "github.com/faiface/beep"
  "github.com/faiface/beep/mp3"
  "github.com/faiface/beep/speaker"
)
```

From the top:

* `package #####` tells the compiler if the file should be compiled as an application or should it be treated as a shared library. In our case `package main` will tell the compiler to treat the app as a executable program.
* `import` statement imports all necessary packages to our codebase. First three packages are from the standard library, then we get three packages from `github.com/faiface`. Most of the IDEs nowadays will do the imports automatically for you!

### Open the file

If we want to play something, we need to somehow import the file to our code. In `main.go` add:

**main.go**
```go
func main() {
  f, err := os.Open("./test.mp3")
```

Before we move anywhere further, let's see what's going on here:

```go
func main()
```

This bit shows the code which function should be invoked first. In Go we define function by using keyword `func` and then name of the function. `main()` should not get any parameters!

```go
f, err := os.Open("./test.mp3")
```

`os.Open` means that we will call a function `Open` from `os` package, which will return two values. As we haven't defined the types of these, we can use a shorthand assignment operator - `:=`.

This way, we don't have to worry about the types from our return!

Let's add more code:

**main.go**
```go
if err != nil {
  log.Fatal(err)
}
```

If you'll write Go in any production capacity, then you'll see `if err != nil` **A LOT**. At first it might look weird and feel weird but after a while it'll be your second nature!

Go doesn't have a concept of `null` values - we deal with `nil`/zero values for each type. In case of `error`, it's `nil`.

So what we're doing here, we literally check, if the error is `nil`. If not, then we print the error to `stdout` and call `os.Exit(1)` - all by using neato `log.Fatal`! In other words - we print the error and then crash the app.

### Prepare the streamer

[^Top](#top)

<a name="improve"/>

## How To Improve

[^Top](#top)

<a name="about"/>

## About The Author


