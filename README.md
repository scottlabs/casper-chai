# Casper.JS Assertions for Chai [![Build Status](https://secure.travis-ci.org/brianmhunt/casper-chai.png?branch=master)](https://travis-ci.org/brianmhunt/casper-chai)

**Casper–Chai** provides a set of custom assertions for use with [CasperJS][].
You get all the benefits of [Chai][] to test with CasperJS.

It is an alternative to Casper's built-in [Tester][] assertions.  Instead of using
Casper's Tester you can use (in this case with [mocha-casperjs][] and Chai):

    describe("my page", function () {
      it("can be opened by Casper", function () {
        casper.open("http://www.google.com")

        casper.then(function () {
          expect(casper.currentHTTPStatus).to.equal(200);
        });

        casper.then(function () {
          expect("Google").to.matchTitle
        });
      });
    });

### Examples

````html
<html>
  <head>
    <title>Casper-Chai Example</title>
    <link rel="stylesheet" href="site.css" type="text/css">
  </head>
  <body>
    <header>
      <a href="javascript:void(0)" class="signin">Sign In</a>
    </header>
    <article>
      <ul class="breadcrumbs">
        <li>Home</li>
        <li>Blog</li>
        <li aria-selected="true">Using Chai in your casper tests</li>
      </ul>
      <div class="greeting">Hello</div>
      <span class="greeting help">Need help?</span>
    </article>
    <footer>
      <a href="/help" id="help-link" class="help">Help</a>
    </footer>
  </body>
</html>
````

Assertions that pass

````javascript
expect(/Casper/).to.matchTitle
'Casper-Chai Example'.to.matchTitle
'site.css'.should.be.loaded
'body > header'.should.be.inDOM
(function() { document.querySelectorAll('li').count === 3 }).to.be.trueOnRemote
'#help-link'.should.have.attribute('href')
'ul.breadcrumbs li'.should.contain.an.element.with.attr('aria-selected')
'.greeting'.to.have.tagNames(['div', 'span'])
'li[aria-selected]'.should.contain.text('Using Chai')
'header a'.should.have.text(/Sign/)
'.greeting'.should.not.have.text(/Bye/)
````

Assertions that fail

````javascript
'li'.should.have.attr('aria-selected')
'li'.should.not.have.an.element.with.attr('aria-selected')
'.greeting'.should.not.have.tagName('span')
'.help'.should.have.text('Help')
````

[Full documentation and more examples](https://github.com/brianmhunt/casper-chai/blob/master/docs/casper-chai.md).

For even more examples, if you are cool with
[CoffeeScript](http://coffeescript.org/), check out the [unit
tests](https://github.com/brianmhunt/casper-chai/blob/master/test/common.coffee).


### Installation

Casper-Chai can be installed with [npm][] using `npm install casper-chai`, or
including
[`casper-chai.coffee`](https://raw.github.com/brianmhunt/casper-chai/master/lib/casper-chai.coffee)
in a directory `require` will find it.

Add extensions to Chai with:

    casper_chai = require('casper-chai');
    chai.use(casper_chai);

To develop and test casper-chai locally, clone the project and run `npm install` to get dependencies
(which, obviously, requires [npm][] to be installed). You will need `cake` to generate documentation - which should be possible by running `npm install -g coffee-script`. Also make sure you have the latest version of [casperjs][] installed.

[CasperJS]: http://casperjs.org/
[Chai]: http://chaijs.com/
[Mocha]: http://visionmedia.github.com/mocha/
[mocha-casperjs]: http://github.com/nathanboktae/mocha-casperjs
[npm]: https://npmjs.org/
[Tester]: http://casperjs.org/api.html#tester

