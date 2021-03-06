* <h3>Why?</h3>

`@venus-fixture` imports HTML markup into your test page, it gives you quick access to DOM nodes for testing your client side interactions.  Importing HTML fixtures saves you the time otherwise spent stubbing or mocking the DOM or elements.

* <h3>How?</h3>

Include the `@venus-fixture` directive in your venus annotation block.  The argument passed to `@venus-fixture` is a file path, it's relative to test file you're annotating.  An example of this directive is below:
```code
@venus-fixture ../fixtures/exampleFixture.fixture.html
```

The full annotation block to may look like the following:
```code
/**
 * @venus-library mocha
 * @venus-include ../lib/zepto.1.0.min.js
 * @venus-include ../src/Silence.js
 * @venus-fixture ../fixtures/exampleFixture.fixture.html
 */
```

When you run your test, the markup from `exampleFixture.fixture.html` will be available on your test page.  The ability to test your DOM manipulations and callbacks to user interactions is now at your fingertips.

* <h3>Examples</h3>

Example test directory structure:
```bash
// Example Test Folder Structure

|-simpleFixtureExample
  |-lib
    |-zepto.1.0.min.js
  |-specs
    |-exampleFixture.spec.js
  |-fixtures
    |-exampleFixture.fixture.html

```


The contents of our HTML fixture file `exampleFixture.fixture.html`:
```code
<div id="example-fixture-container"></div>
```

<strong>Example test</strong> uses zepto to verify that our HTML fixture has been loaded on the page:
```code
describe('Testing @venus-fixture', function() {
  it('Loads our html', function() {
    var length = $('#example-fixture-container').length;
    expect(length).to.be(1);
  });
});
```

<strong>Example test</strong> verifies that a callback was fired by a click event, and that the arguments passed contained a specific DOM id:
```code
describe('Test event delegation target', function() {
  it('Click target should equal "example-fixture-container"', function() {
    var spy = sinon.spy();

    document.addEventListener('click', spy, true);
    $('#example-fixture-container').trigger('click');

    // Callback gets called once
    expect(spy.calledOnce).to.equal(true);
    // The expected element id was passed
    expect(spy.args[0][0].target.id).to.equal('example-fixture-container');
  });
});
```
