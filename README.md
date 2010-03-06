`clj-unit` is a simple unit testing library for Clojure. The goal of `clj-unit` is to provide a non-magical, developer-friendly unit testing API along with a wide variety of assertion helpers.

Features
--------

 * Extremely small core implementation with a simple interface.
 * Pluggable reporters, with a built-in console reporter that uses [clj-stacktrace](http://github.com/mmcgrana/clj-stacktrace) to provide trimmed, cleaned, and colorized backtraces on unit test errors.
 * Stateless facade for reporters, eliminating the need for them to maintain their own global state.
 * Many built in assertions.
 * New assertions can be implemented as stand-alone functions; they don't need to be methods or macros.

Available Assertions
--------------------

 * `assert=`
 * `assert-not=`
 * `assert-in-delta`
 * `assert-that`
 * `assert-not`
 * `assert-nil`
 * `assert-fn`
 * `assert-not-fn`
 * `assert-instance`
 * `assert-isa`
 * `assert-match`
 * `assert-throws`
 * `flunk` (always fails)
 * `success`, `failure`, `assert-truth` (for defining custom assertions)

Example
-------

    (ns myapp.utils-test
      (:use clj-unit.core))
    
    (deftest "re-match?"
      (assert-that (re-match? #"o"   "foo"))
      (assert-not  (re-match? #"bar" "foo")))
    
    (deftest "url-escape, url-unescape: round-trip as expected"
      (let [given "foo123!@#$%^(){}[]?/"]
        (assert= given (url-unescape (url-escape given)))))
    
    (deftest "check-keys: throws on unrecognized keys"
      (assert-throws #"unrecognized keys"
        (check-keys {:foo "bar" :fiz "bat"} [:foo :bar])))
    
    (run-tests 'myapp.utils-test)

License
-------

Copyright 2009-2010 Mark McGranaghan and released under an MIT license.
