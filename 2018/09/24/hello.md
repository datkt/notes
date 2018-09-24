# Feeds, Trees, & Kotlin

> 2018-09-24 13:22

## Hello World !

This is my first post and the beginning of my journey to learning
[Kotlin/Native [1] [2]][kotlin/native] and the porting/implementation of various modules used in
the [Dat Project [3]][datproject.org]. [I come from the world of
JavaScript and C][github.com/jwerle] and will try to dissect the
internals of things like [Hypercore][github.com/mafintosh/hypercore] and
create a working and stable implementation in Kotlin. I will often show
JavaScript and Kotlin _side-by-side_ to emphasis what I'm trying to
demonstrate or explain something when porting or implementing code from
JavaScript, in Kotlin.

## `let/const`, `var/val`, & mutability

Lets consider how mutable and immutable values are declared. In JavaScript,
we use `let` and `const` to denote mutability and immutability,
respectively.  However, `const` doesn't actually prevent the value it
points to from changing. It only prevents the variable identifier from
changing what it points to. This actually maps directly to Kotlin with
the `var` and `val` keywords respectively. The `var` keyword [4] in Kotlin is
a little nostalgic coming from JavaScript **:]**

Below, we define an `Address` class that has a bunch of defaults for
things like `street`, `city`, `state`, `zip`, and `country`. The example
shows how mutability works in both JavaScript and Kotlin.

```js
class Address {
  constructor() {
    this.street = '1234 4th Ave'
    this.city = 'New York'
    this.state = 'New York'
    this.zip = 10001
    this.country = 'US'
  }
}

// `address` cannot point to anything else
const address = new Address()

// this will throw an Error (Assignment to constant variable)
address = new Address()

// the values of the instance can change.
address.street = '5678 5th Ave'

// `street` can be changed to anything
let street = address.street

street = '5678 5th Ave'
```

```kotlin
class Address {
  var street: String = '1234 4th Ave'
  var city: String = 'New York'
  var state: String = 'New York'
  var zip: Int = 10001
  var country: String = 'US'
}

// `address` cannot point to anything else
val address = Address()

// this will throw an Error (val cannot be reassigned)
address = Address()

// the values of the instance can change.
address.street = '5678 5th Ave'

// `street` can be changed to anything
var street = address.street

street = '5678 5th Ave'
```

You may have noticed that we can specify that mutability of _properties_
on the class level in Kotlin. This is not possible in JavaScript without
melding together things like [Symbols][mdn.org/symbol] and
[property accessors][mdn.org/accessor].

This is quite _powerful !_

Throughout all the posts I write, I'll try to show the JavaScript
counterpart of the Kotlin code in question.

I hope this helps...

## Initial Commit

I'm working up to an initial commit, for _anything_. However, I haven't decided
where and what to tackle first. [Yoshua Wuyts][github.com/yoshuawuyts]
([@yoshuawuyts][@yoshuawuyts]) has done an incredible job working on the
[Rust implementation][github.com/datrs] so I'll likely take direction
from that project.

### Ideas

Below are a few starting places I've been thinking about

* `cinterop` of `libsodium` and a `hypercore-crypto` wrapper
* Top down from class to internals, stubbing structures out and working
  inwards?
* Start with tests and public API and working backwards
* Write a SLEEP parser (thanks [yosh][@yoshuawuyts])
* Still thinking....

## References

[1] - [Kotlin][kotlinlang.org] - Statically typed programming language for modern multiplatform applications.
[2] - [Kotlin/Native][kotlinlang.org/native] - A technology for compiling Kotlin to native binaries that run without any VM.
[3] - [Dat Project][datproject.org] - A Distributed Data Community

[kotlinlang.org]: https://kotlinlang.org
[kotlinlang.org/native]: https://kotlinlang.org/docs/reference/native-overview.html

[datproject.org]: https://datproject.org/
[datprotocol.com]: https://www.datprotocol.com

[mdn.org/symbol]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol
[mdn.org/accessor]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_accessors

[github.com/datrs]: https://github.com/datrs
[github.com/jwerle]: https://github.com/jwerle
[github.com/mafintosh]: https://github.com/mafintosh
[github.com/yoshuawuyts]: https://github.com/yoshuawuyts
[github.com/mafintosh/hypercore]: https://github.com/mafintosh/hypercore

[@yoshuawuyts]: https://twitter.com/yoshuawuyts
