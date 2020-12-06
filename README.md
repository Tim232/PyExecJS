PyExecJS (EOL)
==============
[![Build Status](https://travis-ci.org/Tim232/PyExecJS.svg?branch=travis-ci)](https://travis-ci.org/Tim232/PyExecJS)

[EOL](https://gist.github.com/doloopwhile/8c6ec7dd4703e8a44e559411cb2ea221)
---

Run JavaScript code from Python.

PyExecJS is a porting of ExecJS from Ruby.
PyExecJS **automatically** picks the best runtime available to evaluate your JavaScript program.

A short example:

```python
import execjs
execjs.eval("'red yellow blue'.split(' ')")
>>> ['red', 'yellow', 'blue']
ctx = execjs.compile("""
     function add(x, y) {
         return x + y;
     }
 """)
 ctx.call("add", 1, 2)
 >>> 3
 ```

# Supported runtimes

## First-class support (runtime class is provided and tested)

* [PyV8](http://code.google.com/p/pyv8/) - A python wrapper for Google V8 engine,
* [Node.js](http://nodejs.org/)
* [PhantomJS](http://phantomjs.org/)
* [Nashorn](http://docs.oracle.com/javase/8/docs/technotes/guides/scripting/nashorn/intro.html#sthref16) - Included with Oracle Java 8

## Second-class support (runtime class is privided but not tested)

* Apple JavaScriptCore - Included with Mac OS X
* [Microsoft Windows Script Host](http://msdn.microsoft.com/en-us/library/9bbdkx3k.aspx) (JScript)
* [SlimerJS](http://slimerjs.org/)
* [Mozilla SpiderMonkey](http://www.mozilla.org/js/spidermonkey/)

# Installation

    $ pip install PyExecJS

# Details

If `EXECJS_RUNTIME` environment variable is specified, PyExecJS pick the JavaScript runtime as a default:

    >>> execjs.get().name # this value is depends on your environment.
    >>> os.environ["EXECJS_RUNTIME"] = "Node"
    >>> execjs.get().name
    'Node.js (V8)'

You can choose JavaScript runtime by `execjs.get()`:

    >>> default = execjs.get() # the automatically picked runtime
    >>> default.eval("1 + 2")
    3
    >>> import execjs.runtime_names
    >>> jscript = execjs.get(execjs.runtime_names.JScript)
    >>> jscript.eval("1 + 2")
    3
    >>> import execjs.runtime_names
    >>> node = execjs.get(execjs.runtime_names.Node)
    >>> node.eval("1 + 2")
    3

The pros of PyExecJS is that you do not need take care of JavaScript environment.
Especially, it works in Windows environment without installing extra libraries.

One of cons of PyExecJS is performance. PyExecJS communicate JavaScript runtime by text and it is slow.
The other cons is that it does not fully support runtime specific features.

[PyV8](https://code.google.com/p/pyv8/) might be better choice for some use case.

# Changelog

## 1.0.0
- First release.
