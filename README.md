# squery
A pure-Scala toolkit for working in the browser

The sQuery library has a straightforward but deep mission: to replace jQuery.

As the Scala.js ecosystem evolves, we are seeing more and more folks building complex tools in it, even native-Scala UI frameworks. But deep under the hood, we are still often using jQuery. Even many frameworks use jQuery internally, because jQuery is specifically *not* a framework. Instead, it's a toolkit for making it more bearable to work with the DOM.

I'm the maintainer of the jquery-facade library, and use jQuery heavily myself. But it's always a bit frustrating, because it *thinks* like JavaScript, not like Scala -- it is weakly-typed and ad-hoc in many areas where we generally expect better nowadays. But I keep using it, because raw DOM programming is horribly unpleasant.

Hence, sQuery. This is specifically *not* a simple rewrite of jQuery in Scala. It makes no claims of being even remotely API-compatible with jQuery, since the APIs are much of the problem. Instead, its goal is to fill the same ecological niche as jQuery -- providing a decent interface for working with the DOM -- with an idiomatic Scala API.

### Using sQuery

sQuery gets installed in your libraryDependencies as usual:
```
libraryDependencies += "org.querki" %%% "squery" % "0.1"
```

It has no JavaScript dependencies. (That's kind of the point.) It uses Scala.js' DOM facade to do most of its work.

### The sQuery Philosophy

First and foremost: sQuery is *not* a framework. You should instead think of it as a toolkit for *building* frameworks -- whether formal libraries, or ad-hoc mini-frameworks for a small Scala.js application. (That said, sQuery's philosophy is likely to be more powerful for some kinds of frameworks than others.)

Its sole task is to provide more usable, often higher-level, constructs for working in the DOM. There are parallels between sQuery and jQuery in terms of functionality, but that is intentionally inexact: much of what jQuery does is irrelevant or actively in the way when writing a Scala program.

sQuery is not trying to be a single overarching gadget, nor to monkey-patch into DOM objects, the way jQuery does. Instead, it is following a more typical Scala approach, with some basic guidelines:

* Typeclasses should be favored whenever appropriate. These not only promote decoupled code, they allow higher-level constructs to share the same abstractions as the native DOM. For example, consider the `Disableable` typeclass, which represents something that can be disabled. By viewing this as a typeclass, we can use the same paradigm for built-in DOM objects like buttons, and high-level framework objects like panes.

* These typeclasses should be kept relatively decoupled, insofar as possible. Among other things, this should allow the Scala.js compiler to efficiently trim things down to just the code you are actually using.

* Things should work naturally with Scala collections. jQuery implicitly invents its own concept of collections -- when you say `$(something)`, you often get back an opaque object that contains a collection. We should instead have our typeclasses work naturally with Scala collections where appropriate, and avoid inventing unnecessary data structures.

### State of the Project

sQuery is still basically nascent at this point. What is there works decently well, but there isn't much there yet. I am adding bits gradually as I refactor jQuery out of my own code, but I'm not trying to create the whole thing at a shot.

Collaborators would be highly welcomed. If this is just my baby, it'll evolve gradually, becoming slowly more useful, but will probably never be "complete" in any meaningful sense. If you're interested in working on this and adding pieces, drop me a note -- I'm `jducoeur` pretty much everywhere (particularly on Gitter and Gmail).

Notes on the project can be found in Querki, in the [sQuery Documentation Space](https://www.querki.net/u/jducoeur/squery-documentation/#!squery-documentation). (This isn't really documentation yet, but should eventually grow up to be.)

### Releases

* **0.1** -- initial release, with Focusable, Findable, Disableable and Cookies.
