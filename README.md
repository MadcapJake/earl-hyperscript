# Earl Hyperscript

[![npm package][npm-ver-link]][releases]
[![][dl-badge]][npm-pkg-link]
[![][mit-badge]][mit]

Converts [Earl Grey](https://breuleux.github.io/earl-grey/)'s document building syntax to vtree that works with [Cycle.js](http://cycle.js.org/).

## Example

Here's a rewrite in Earl Grey of the increment/decrement counter from Cycle.js's [basic examples](http://cycle.js.org/basic-examples.html).

```earl-grey
require:
   "@cycle/core" as cycle
   "@cycle/dom"  -> makeDOMDriver
   earl-hyperscript -> h

main = {=> DOM} ->
   chain cycle.Rx.observable:
      @merge with
         chain DOM:
            @get(".decrement") with .click
            @map: ev -> -1
         chain DOM:
            @get(".increment") with .click
            @map: ev -> +1
      @start-with: 0
      @scan: (x, y) -> x + y
      @map: count ->
         h: div %
            button.decrement % .Decrement
            button.increment % .Increment
            p % 'Counter: {count}'

cycle.run(main) with {
   DOM = makeDOMDriver("#app")
}
```

# License

[MIT][mit] © [Jake Russo][author] et [al][contributors]


[mit]:          http://opensource.org/licenses/MIT
[author]:       http://github.com/MadcapJake
[contributors]: https://github.com/MadcapJake/earl-hyperscript/graphs/contributors
[releases]:     https://github.com/MadcapJake/earl-hyperscript/releases
[mit-badge]: https://img.shields.io/badge/license-MIT-444444.svg?style=flat-square
[npm-pkg-link]: https://www.npmjs.org/package/earl-hyperscript
[npm-ver-link]: https://img.shields.io/npm/v/earl-hyperscript.svg?style=flat-square
[dl-badge]: http://img.shields.io/npm/dm/earl-hyperscript.svg?style=flat-square
