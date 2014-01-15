Testing and Continuous Integration
==================================

Automated testing of your web application is a very important thing, do it from day one! Aim for *fast* tests that aren't annoying to wait for.


Unit Testing vs. Behavior Driven Tests?
---------------------------------------

We initially wrote [BDD Tests](https://en.wikipedia.org/wiki/Behavior-driven_development) to test the server, as it sounds to be a very nice way to describe the behavior of the software. But it didn't work out so well for us: we ended up having tests that took over half an hour to run through and tested the whole stack, i.e. the web server, external libraries and multiple times the same parts of our code.


Do Unit Testing!
----------------

Unit Tests are not only fast, since they test only small parts of your code, they also force to better structure your code to make it testable.


Code coverage
-------------

Measuring [code coverage](https://en.wikipedia.org/wiki/Code_coverage) can be useful, it helps you cover cases you haven't thought about. But don't go for that 100% coverage only to have 100% coverage.

Good tools are [coverage.py](http://nedbatchelder.com/code/coverage/) for Python and [Istanbul](https://github.com/yahoo/istanbul) for JavaScript.


Nose
----




Travis
------
