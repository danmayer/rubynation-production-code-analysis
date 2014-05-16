# Production Code Analysis: Tales of deleting 200K+ LOC by Dan Mayer


In a long-lived Ruby application with many contributors, it's common to feel like you have lost control of the codebase. Refactoring is difficult in these situations, but tools are available to help you regain the control you once had. I will cover driving refactoring based on production metrics and analysis as a solution to this problem. * Start simple: what you can learn from New Relic and other performance monitors * Fill in missing pieces with event tracking, email tracking, partial tracking, i18n locale tracking, and one-off trackers * Quickly comparing performance between two implementations * Introduce Coverband code coverage in production, which detects unused code.

## Outline

* Code Can be a mess (something funny line the programming sucks quote)
* A bit of history cloned projects
* Show some 'proof' my git lines deleted
* It isn't just me, we celebrated it as a team. We encouraged it. Improving code, deleting code, sharing our best commits in campfire.
  * show team code deletion
* There is no magic bullet. It can be slow and hard. 
  * but code can help!
* outline of tools / topics to discuss  
  * existing outline slide
* The basics: where to start


## Add Slides

* garbage collection (simple how to measure requests/GC cycles):
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
  
    [~/projects/deals] git log --numstat --pretty="%H" --author="dan.mayer" --since="2 years ago" app | awk 'NF==3 {plus+=$1; minus+=$2} END {printf("+%d, -%d\n", plus, minus)}'
+20973, -47034
[master][~/projects/deals] git log --numstat --pretty="%H" --since="2 years ago" app | awk 'NF==3 {plus+=$1; minus+=$2} END {printf("+%d, -%d\n", plus, minus)}'
+197326, -215514

    [~/projects/admin] git log --numstat --pretty="%H" --author="dan.mayer" --since="2 years ago" app | awk 'NF==3 {plus+=$1; minus+=$2} END {printf("+%d, -%d\n", plus, minus)}'
+13555, -52091
    git log --numstat --pretty="%H" --since="1 year ago" app | awk 'NF==3 {plus+=$1; minus+=$2} END {printf("+%d, -%d\n", plus, minus)}'
+8226, -79265
    git log --numstat --pretty="%H" --since="2 years ago" app | awk 'NF==3 {plus+=$1; minus+=$2} END {printf("+%d, -%d\n", plus, minus)}'
+110020, -204037
  
### Maybe Research
  
* [Ruby 2 systemtap](http://avsej.net/2012/systemtap-and-ruby-20/)
* [dtrace method cache clear tracing](https://github.com/simeonwillbanks/busted/blob/master/dtrace/probes/examples/method-cache-clear.d)
* PL deprecation: http://code.livingsocial.net/ia/pipeline/blob/master/lib/pipeline/deprecation.rb  this could be interesting to talk about.
* [method tracer](https://github.com/change/method_profiler)
* [ruby-prof](https://github.com/ruby-prof/ruby-prof)
* covering rearview