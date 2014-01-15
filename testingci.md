# Testing and Continuous Integration #

Automated testing of your web application is a very important thing, do it from day one! Aim for *fast* tests that aren't annoying to wait for.


## Unit Testing vs. Behavior Driven Tests? ##

We initially wrote [BDD Tests](https://en.wikipedia.org/wiki/Behavior-driven_development) to test the server, as it sounded to be a very nice way to describe the behavior of the software. But it didn't work out so well for us: we ended up having tests that took over half an hour to run through and tested the whole stack, i.e. the web server, external libraries and multiple times the same parts of our code.


## Do Unit Testing! ##

Unit Tests are not only fast (they only test isolated parts of your code), they also force to better structure your code to make it testable.

For the server side: always create the models you need in your tests. We ended up writing a model creation mixin for the most common models of our application. Like this you can conveniently setup the required models at the beginning of your test function, without much hassle.


## Code coverage ##

Measuring [code coverage](https://en.wikipedia.org/wiki/Code_coverage) can be useful, it helps you cover cases you haven't thought about. But don't go for that 100% coverage only to have 100% coverage.

Good tools are [coverage.py](http://nedbatchelder.com/code/coverage/) for Python and [Istanbul](https://github.com/yahoo/istanbul) for JavaScript.


## Nose for Python ##

Install [nose](https://nose.readthedocs.org/) and the Django test runner [django-nose](https://github.com/django-nose/django-nose) ([installation instructions](https://github.com/django-nose/django-nose#installation)).

Fasten-up the tests by [reusing the database](https://github.com/django-nose/django-nose#enabling-database-reuse):

    REUSE_DB=1 ./manage.py test


## Karma for JavaScript ##

Setup the [Karma](http://karma-runner.github.io) test runner and run it from the [Grunt](http://gruntjs.com) task `grunt test`. For this, add the NPM package `grunt-karma` to your client's dependencies.

Install [PhantomJS](http://phantomjs.org), the headless WebKit browser, and configure Karma to use it.

    npm install phantomjs

For more details, checkout the [Karma configuration file]() and the [Grunt task]() as used in the Braindump application.


## Travis ##
