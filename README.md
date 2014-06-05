# Production Code Analysis: Tales of deleting 200K+ LOC by Dan Mayer

In a long-lived Ruby application with many contributors, it's common to feel like you have lost control of the codebase. Refactoring is difficult in these situations, but tools are available to help you regain the control you once had. I will cover driving refactoring based on production metrics and analysis as a solution to this problem. 

* Start simple: what you can learn from New Relic and other performance monitors
* Fill in missing pieces with event tracking, email tracking, partial tracking, i18n locale tracking, and one-off trackers 
* Quickly comparing performance between two implementations 
* Introduce Coverband code coverage in production, which detects unused code.

## Running locally

If you want presenter mode make sure the deck.remote.js script is in the file. Then open `index.html`

To control the presentation and view the speaker notes, then run the deck.remote project.

    ~/projects/deck.remote.js/deck-remote-server/main.js &
    open ~/projects/deck.remote.js/deck-remote-client/index.html


## Add Slides (Maybe)

* rearview, do you know when someone breaks an old feature? A post purchase feedback survey pulling in good upsell money. A JS change from another team broke the feature, it took 8 days before it was noticed. A feature isn't live unless you have metrics, and near real time alerting.
  
### Maybe Research and add a slide?
  
* [Ruby 2 systemtap](http://avsej.net/2012/systemtap-and-ruby-20/)
* [dtrace method cache clear tracing](https://github.com/simeonwillbanks/busted/blob/master/dtrace/probes/examples/method-cache-clear.d)
* [method tracer](https://github.com/change/method_profiler)
* covering rearview