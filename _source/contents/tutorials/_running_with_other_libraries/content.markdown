<p>Venus simplifies running unit tests for JavaScript. To minimize overhead, we set out to create a tool that makes it easier to work with an existing test library such as Mocha, Jasmine or QUnit.</p>

<h3>Mocha</h3>
<a href="http://visionmedia.github.com/mocha/" target="_blank">http://visionmedia.github.com/mocha/</a>

<p>Mocha is a feature-rich test framework that provides a wealth of features, not limited to, but including: async support, watching for slow tests, and integration with various assertion libraries. However, it doesn't contain integration with any browsers (ex. WebKit). By simply adding Venus annotations, you can use Venus to run your tests using PhantomJS, while still being able to run them using the mocha CLI.</p>

<p>Let's say you have this test file, <code>tests.js</code>:</p>

```js
describe('Array', function() {
  describe('#indexOf()', function() {
    it('should return -1 when the value is not present', function() {
      expect([1, 2, 3].indexOf(5)).to.be(-1);
      expect([1, 2, 3].indexOf(0)).to.be(-1);
    });
  });
});
```

<p>In order to make <code>tests.js</code> runnable in Venus, modify your file as follows:</p>

```js
/**
 * @venus-library mocha
 * @venus-template sandbox
 */
describe('Array', function() {
  describe('#indexOf()', function() {
    it('should return -1 when the value is not present', function() {
      expect([1, 2, 3].indexOf(5)).to.be(-1);
      expect([1, 2, 3].indexOf(0)).to.be(-1);
    });
  });
});
```

<p>NOTE: This file uses <code>expect.js</code>, but can be modified to use any assertion library supported by Mocha.</p>

<p>Now you can run your tests using Venus:</p>

```bash
$ venus run -t tests.js -n

info:   Serving test: http://localhost:2013/venus-core/1
info:   executor started on localhost:2013
info:   Phantom browser is loading http://localhost:2013/venus-core/1

--------------------------------------------------------


PhantomJS/1.7.0

   Array >> #indexOf()
     ✓ should return -1 when the value is not present


✓ 1 test completed (0.01ms)
```

<h3>Jasmine</h3>
<a href="http://pivotal.github.com/jasmine/" target="_blank">http://pivotal.github.com/jasmine/</a>

<p>Jasmine is a behavior-driven development framework for testing JavaScript code. By default, it includes an HTML file that serves as a test runner.  However, it doesn't provide a command-line interface to run your unit tests. By simply adding Venus annotations, you can use Venus to run your tests both from the command line, while still preserving the ability to use the HTML test runner.</p>

<p>Let's say you have this file, <code>tests.js</code>:</p>

```js
describe('A suite', function() {
  it('contains spec with an expectation', function() {
    expect(true).toBe(true);
  });
});
```

<p>In order to make <code>tests.js</code>: runnable in Venus, modify your file as follows:</p>

```js
/**
 * @venus-library jasmine
 * @venus-template sandbox
 */
describe('A suite', function() {
  it('contains spec with an expectation', function() {
    expect(true).toBe(true);
  });
});
```

<p>Now you can run your tests using Venus:</p>

```bash
$ venus run -t tests.js -n

info:   Serving test: http://localhost:2013/venus-core/1
info:   executor started on localhost:2013
info:   Phantom browser is loading http://localhost:2013/venus-core/1

--------------------------------------------------------


PhantomJS/1.7.0

   A suite
     ✓ contains spec with an expectation


✓ 1 test completed (0ms)
```

<h3>QUnit</h3>
<a href="http://qunitjs.com/" target="_blank">http://qunitjs.com/</a>

<p>QUnit is a JavaScript unit test suite used by jQuery, jQuery UI, and jQuery Mobile.  It provides a web page interface for running your unit tests.  However, it doesn't provide a command-line interface to run your unit tests.  By simply adding Venus annotations, you can use Venus to run your tests both from the command line, while still preserving the ability to use the web page interface.</p>

<p>Let's say you have this test file, <code>tests.js</code>:</p>

```js
test( "hello test", function() {
  ok( 1 == "1", "Passed!" );
});
```

<p>In order to make <code>tests.js</code> runnable in Venus, modify your file as follows:</p>

```js
/**
 * @venus-library qunit
 * @venus-template sandbox
 */

test( "hello test", function() {
  ok( 1 == "1", "Passed!" );
});
```

<p>Now you can run your tests using Venus:</p>

```bash
$ venus run -t tests.js -n

info:   Serving test: http://localhost:2013/venus-core/1
info:   executor started on localhost:2013
info:   Phantom browser is loading http://localhost:2013/venus-core/1

--------------------------------------------------------


PhantomJS/1.7.0

   hello test
     ✓ Passed!


✓ 1 test completed (20ms)
```
