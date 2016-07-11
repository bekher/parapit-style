# Parapit Style Guide

This guide is not meant to be exhaustive. See the [Complete Guides](#complete-guide) section to fill in the gaps.

## Table of Contents
1. [Ground Rules](#ground-rules)
2. [Security](#security)
3. [Version Control](#version-control)
4. [Whitespace](#whitespace)
5. [Naming](#naming)
6. [Comments](#comments)
7. [Testing](#testing)
8. [Printing](#printing)
9. [Control Structures](#control-structures)
10. [Other Practices](#other-practices)
11. [Javascript Specific](#javascript)
12. [Python Specific](#python)

Addendum: [Complete Guides](#complete-guides)

## Core Guide
#### Ground Rules
  1. First rule: Use common sense.
  2. Second rule: Security is the main priority.
  3. Third rule: [KISS](https://en.wikipedia.org/wiki/KISS_principle).
  
#### Security
+ Do not commit secrets and passwords, even to private repositories
+ Do not execute code as root, even in development
+ Backend:
  - Do not EVER execute any shell commands from within the code without talking to Greg first
  - Do not use eval or its cousins
  - Sanitize ALL user input
  - Sanitize ALL data collection when processing 
+ Frontend:
  - Do not insert arbitrary data in the DOM, escape all HTML
  - Sanatize and verify ALL user input

#### Version Control
  + Pre-v1.0.0 stable:
    - Clone a new branch off of master, with a descriptive name: `Greg-dev` for general development/short-term tasks, and `Greg-add-enclave-view` for specific, medium/long-term tasks. (we will work off of a development branch after we launch)
    - After finishing a new feature or fixing a bug, open a merge request and another engineer should review your code.
	
#### Whitespace
+ Line breaks:
    - Unix linebreaks (‘\n’) no Windows linkebreaks (‘\r\n’) (convert with dos2unix if needed, preferably do not code on Windows)
+ Line length:
    - 120 characters or less (recommend under 80)
+ Avoid trailing whitespace

#### Naming
+ Variable names should be descriptive but curt
  - Yes: `var numFeedItems`
  - No: `var nItems`
  - No: `var theNumberOfFeedItems`
+ Use camelCase for variables and functions
+ First letter uppercase CamelCase for classes
+ Constants should be in all caps

#### Comments
+ Insert comments as needed, preferably every at each logical code-block separation or every few lines. 
+ Comment a function/method if you feel the need to explain its purpose. Keep comments curt and to the point, under two sentences long, ideally under ten words. If you feel the need to explain something in detail, put it above the function declaration in a `/* block comment */`
+ Commented dead code should be deleted, unless there is a convincing justification

#### Testing:
+ Write unit tests when possible. We will crack down on testing further into development. 
+ Always write tests for security.

#### Printing:
+ Avoid printing to stdout except for critical errors or for initial startup, before a logger is instantiated.
+ Use a logging facility when an error may be thrown
+ Add debug printing when debugging, but remove before pushing. 

#### Control structures:
+ K&R style brackets and whitespace
  - Yes:

	```javascript
	if(...) {
	  doThings();
	} else if (...) {
	  doOtherThings();
	} else {
	  doSomethingElse();
	}
	```
	
  - No:

	```javascript 
  if (…)
  {doThings(); doMoreThings;}
  else if (…)
	{
	  doSomethingElse();
	}
	```
	
+ Use ternary operators when possible and not error checking
	- Example:

	```javascript
    config.http ? config.http.port : (config.port, config.hostname)
  ```
+ Complex conditional expressions should be assigned to a variable

#### Other practices
+ Avoid “magic” code; definition: spaghettified and/or mysterious code that works but you cannot explain why.
+ Don’t put an else after a return, the else will be executed regardless
+ Do not compare x == true or x == false, use (x) or (!x). However, do compare objects to null and strings to “” if there is chance for confusion
+ Declare local functions close to their use
+ Use single quotes (unless writing JSON)

#### Javascript

ES5 & ES6
+ Indentation
  - Two space soft tabs
+ Use lodash utility functions when possible 
+ async.waterfall if you are on the highway to callback hell
+ Create objects with {member: value} rather than new Object()
+ One variable declaration per statement
+ Functions with optionals should have an `opts` parameter object
   - Example: 

   ```javascript
    var myFunc = function(opts, callback) {
      var app = opts.app || {};
      var hostname = opts.hostname || '127.0.0.1';
      var port = opts.port || '1234';
    }
    ```

ES5 Only
+ Always `‘use strict’`
+ Use semicolons

#### Python
+ Indentation
  - Four space soft tabs
+ Avoid global variables
+ Do not place outer parenthesis around conditionals: if 1 > 2: instead of if (1 > 2):
+ Use string formatters instead of + concatenation, for example: myStr = ‘The %s number is %d’ % (‘magic’, 42)

-----
Check out [Mozilla's style guide](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Coding_Style) that inpsired some parts of this guide.

## Complete guides

Consult these other guides to fill in the gaps (purposefully) left in place by this guide. 

+ NodeJS Backend 
  - JS ES5: https://github.com/airbnb/javascript/tree/master/es5
+ React Full-Stack
  - JS ES6: https://github.com/airbnb/javascript
  - JSX/React: https://github.com/airbnb/javascript/tree/master/react
+ Analysis/ML: 
  - Python: https://www.python.org/dev/peps/pep-0008/
