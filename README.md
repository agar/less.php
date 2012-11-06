less.php
========

The **dynamic** stylesheet language.

<http://lesscss.org>

about
-----

This is a PHP port of the official JavaScript version of LESS <http://lesscss.org>.

Most of the code structure remains the same, which should allow for fairly easy updates in the future. That does
mean this library requires PHP5.3 as it makes heavy use of namespaces, anonymous functions and the shorthand ternary
operator - `?:` (to replicate the way Javascript will return the value of the first valid operand when using  `||`).

A couple of things have been omitted from this initial version:

- Evaluation of JavaScript expressions within back-ticks (for obvious reasons).
- Definition of custom functions - will be added to the `\Less\Environment` class.
- A tidy up of the API is needed.

_Note: I haven't had time to keep this up to date at all - to be honest a direct port of the less.js code is not 
likely an efficient approach anyway and was more an exercise to see if it was possible. If you're for a PHP version
of less.js you can use in production, check out [https://github.com/leafo/lessphp](https://github.com/leafo/lessphp)._

use
---

### The parser

```php
<?php

$parser = new \Less\Parser();
$parser->getEnvironment()->setCompress(true);

// parse css from a less source file or directly from a string
$css = $parser
            ->parseFile($path)
            ->parse("@color: #4D926F; #header { color: @color; } h2 { color: @color; }")
            ->getCss();
```

### The command line tool

The `bin/lessc` command line tool will accept an input (and optionally an output) file name to process.

```bash
$ ./bin/lessc input.less output.css
```

### In your website

The `bin/less.php` file can be moved to the directory containing your less source files. Including a links as follows
will compile and cache the css.

```html
<link rel="stylesheet" type="text/css" href="/static/less/css.php?bootstrap.less" />
```

NB: You'll need to update this file to point to the `lib` directory, and also make sure the `./cache` directory is
writable by the web server.

license
-------

See `LICENSE` file.
