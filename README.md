# mock-function

The original intention of this module is to simplify mock functions in unit
tests.

Instead of writing:

    function mockFunction(val) {
      if (val === 'foo')
        return '1';
      }
      if (val === 'bar')
        return '2';
      }
    }

Which easily becomes too voluminous and cluttered, one should be able to write:

    const mockFunction = require('mock-function');
    const fn = mockFunction().with('foo').returns('1').with('bar').returns('2');

I created this for this rather simple purpose, so this module hasn't been
thoroughly tested etc. But the behavior I needed has been covered in the tests.

### Usage/Examples

`require('mock-function');` returns a function, which is supposed to be called
as a function, not a constructor. It returns another function, which allows its
return values to be set up thru `.with()` and `returns()`/`throws()` calls.

For behavior details see the tests in the test directory, though the behavior
should be rather intuitive.

Here, just a couple of examples:

    const mockFunction = require('mock-function');
    const mf = mockFunction()
      .with(1, 2, 3).returns('foo')
      .with([2, 1]).throws(new Error('Foo'));

    mf([2, 1]);             // will throw new Error('Foo')
    mf(1, 2, 3);            // will return 'foo'
    mf(anyOtherOrUndef);    // will return undefined
