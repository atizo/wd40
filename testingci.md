# Testing and Continuous Integration #

Automated testing of your web application is a very important thing, do it from day one! Aim for *fast* tests that aren't annoying to wait for -- this encourages continous integration.


## Unit Testing vs. Behavior Driven Tests? ##

We initially wrote [BDD Tests](https://en.wikipedia.org/wiki/Behavior-driven_development) to test the server, as it sounded to be a very nice way to describe the behavior of the software. But it didn't work out so well for us: we ended up having tests that took over half an hour to run through and tested the whole stack, i.e. the web server, external libraries and multiple times the same parts of our code.


## Do Unit Testing! ##

Not only are Unit Tests super fast (by testing isolated parts of your code), they also force you to better structure the code to make it testable.


## Server: Nose for Python ##

Install [nose](https://nose.readthedocs.org/) and the Django test runner [django-nose](https://github.com/django-nose/django-nose) ([installation instructions](https://github.com/django-nose/django-nose#installation)).

Fasten-up the tests by [reusing the database](https://github.com/django-nose/django-nose#enabling-database-reuse):

    REUSE_DB=1 ./manage.py test

### Use models in tests ###

Very often, a test requires data to deal with (some users with profiles, entries etc.). A test function must be self-sufficient (they may be runned in any order), so always create the required objects at the beginning of the function. You can create objects used by multiple test functions in the test case's `setUp()` function.

To create test objects conveniently, we ended up writing a model creation mixin for the most common models of our application. This mixin provides helper functions that, if no arguments are given, create a model that has meaningful default values and randomized unique data (like the username). Here is an example usage of the creation mixin:

    class SomeTestCase(TestCase, ModelCreationMixin):
        def testSomething():
            # create a user with profile using
            # default values and a random username
            user1 = self.new_user()

            # create a user with profile using a specific username
            user2 = self.new_user(username='joe')

            # test something with user1 and user2


## Client: Karma for JavaScript ##

We run JavaScript tests with the [Karma](http://karma-runner.github.io) test runner from the [Grunt](http://gruntjs.com) task `grunt test`. Setup Karma by adding the NPM package `grunt-karma` to your client's dependencies.

The automated client tests should run without a browser UI, so install [PhantomJS](http://phantomjs.org), the headless WebKit browser, by adding the dependency `phantomjs`. Then configure Karma to use it:

    browsers = ['PhantomJS'];

To load and use templates in tests, precompile them by adding the dependency `karma-ng-html2js-preprocessor` and define `html2js` as preprocessor:

    preprocessors = {
        'app/**/templates/*.html': 'html2js'
    };

In tests, templates can then be loaded like this:

    beforeEach(module('app/mymodule/templates/mytemplate.html'));

For all the details, checkout the [Karma configuration file]() and the [Grunt task]() from the Braindump application.


## Code coverage ##

Measuring [code coverage](https://en.wikipedia.org/wiki/Code_coverage) can be useful, it helps you cover cases you haven't thought about. But don't go for that 100% coverage only to have 100% coverage.

We use [coverage.py](http://nedbatchelder.com/code/coverage/) for Python and [Istanbul](https://github.com/yahoo/istanbul) for JavaScript.

tbd. (configuration details, run)

## Travis ##
