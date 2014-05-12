# Production Code Analysis: Tales of deleting 200K+ LOC by Dan Mayer


In a long-lived Ruby application with many contributors, it's common to feel like you have lost control of the codebase. Refactoring is difficult in these situations, but tools are available to help you regain the control you once had. I will cover driving refactoring based on production metrics and analysis as a solution to this problem. * Start simple: what you can learn from New Relic and other performance monitors * Fill in missing pieces with event tracking, email tracking, partial tracking, i18n locale tracking, and one-off trackers * Quickly comparing performance between two implementations * Introduce Coverband code coverage in production, which detects unused code.

## Add slides

* garbage collection:
  * oobgc
  * [gc tracer](https://github.com/ko1/gc_tracer)
  * gc profiling (link to mountain west memory talk)
* "they left the suspension cables because they're still sort of holding up parts of the bridge. Nobody knows which parts, but everybody's pretty sure they're important parts."
-- http://mashable.com/2014/04/30/programming-sucks/?utm_cid=mash-com-fb-main-link
* rearview, do you know when someone breaks an old feature? A post purchase feedback survey pulling in good upsell money. A JS change from another team broke the feature, it took 8 days before it was noticed. A feature isn't live unless you have metrics, and near real time alerting.
* Sam Rawlins [@srawlins](https://twitter.com/srawlins)
	* [AllocationStats](https://github.com/srawlins/allocation_stats)
	* [rack-allocation_stats](https://github.com/srawlins/rack-allocation_stats)
	* [Ruby 2.1 Awesomeness: Pro Object Allocation Tracing](http://www.confreaks.com/videos/3272-mwrc-new-ruby-2-1-awesomeness-pro-object-allocation-tracing)
* Thanks Aman Gupta [@tmm1](https://twitter.com/tmm1)
  * [rack#warmup preloading](https://github.com/rack/rack/commit/f791197f501776480a67211afbca0b32c628b2c9)
      * "With complex frameworks like Rails, many dependencies are auto-loaded
and data like mime-type and i18n is not loaded into memory by default. This
often means the first few requests handled by an application are quite
slow."
  * [ruby 2.1 method cache](http://tmm1.net/ruby21-method-cache/)
  * https://github.com/tmm1/stackprof
  * [history of Ruby's GC](http://tmm1.net/ruby21-rgengc/)
  
### Maybe Research
  
* [Ruby 2 systemtap](http://avsej.net/2012/systemtap-and-ruby-20/)
* [dtrace method cache clear tracing](https://github.com/simeonwillbanks/busted/blob/master/dtrace/probes/examples/method-cache-clear.d)
  

#deck.js

A JavaScript library for building modern HTML presentations. deck.js is flexible enough to let advanced CSS and JavaScript authors craft highly customized decks, but also provides templates and themes for the HTML novice to build a standard slideshow.

## Quick Start

This repository includes a `boilerplate.html` as a starting point, with all the extensions included. Just [download it](https://github.com/imakewebthings/deck.js/archive/latest.zip), open `boilerplate.html`, and start editing your slides.

## Documentation

Check out the [documentation page](http://imakewebthings.github.com/deck.js/docs) for more information on the methods, events, and options available in core and all the included extensions.  A sample standard slide deck is included in the package under the `introduction` folder.  You can also [view that sample deck](http://imakewebthings.github.com/deck.js/introduction) online to play with the available style and transition themes.

## Extensions, Themes, and Related Projects

Take a look at [the wiki](https://github.com/imakewebthings/deck.js/wiki) for lists of extensions, themes, and other related goodies.  If you have a publicly available project of your own, feel free to add to the list.

## Dependencies (included in this repository)

- [jQuery](http://jquery.com)
- [Modernizr](http://modernizr.com)

## Tests & Support

Unit tests are written with [Jasmine](http://pivotal.github.com/jasmine/) and [jasmine-jquery](https://github.com/velesin/jasmine-jquery). You can [run them here](http://imakewebthings.github.com/deck.js/test).

deck.js has been tested with jQuery 1.6+ and works in IE7+, Chrome, FF, Safari, and Opera. The more capable browsers receive greater enhancements, but a basic cutaway slideshow will work for all browsers listed above. Please don't give your presentations in IE6.

For any questions or general discussion about deck.js please direct your attention to the [mailing list](http://groups.google.com/group/deckjs) (uses Google groups.)  If you would like to report a bug, please see the [issues page](https://github.com/imakewebthings/deck.js/issues).

## Printing

Core includes stripped down black and white print styles for the standard slide template that is suitable for handouts.

## Awesome Contributors

- [jbuck](https://github.com/jbuck)
- [cykod](https://github.com/cykod)
- [dougireton](https://github.com/dougireton)
- [awirick](https://github.com/awirick)
- Daniel Knittl-Frank
- [alexch](https://github.com/alexch)
- [twitwi](https://github.com/twitwi)

If you would like to contribute a patch to deck.js please do as much as you can of the following:

- Add or amend Jasmine tests.
- Add inline documentation.
- If the standard snippet of an extension changes, please change it in both the introduction deck and the snippet html in the extension folder.
- If the API changes, it would be awesome to receive a parallel pull request to the gh-pages branch which updates the public-facing documentation.

## License

Copyright (c) 2011-2014 Caleb Troughton

Licensed under the [MIT license](https://github.com/imakewebthings/deck.js/blob/master/MIT-license.txt)

## Donations

[![Gittip donate
button](http://img.shields.io/gittip/imakewebthings.png)](https://www.gittip.com/imakewebthings/ "Donate weekly to this project using Gittip")
