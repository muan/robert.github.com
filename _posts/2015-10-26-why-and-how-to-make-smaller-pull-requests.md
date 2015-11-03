---
title: Why and how to make smaller pull requests
layout: post
---
There are only two things in the world scarier than making a 2,000 line pull request. One of them is giant murderous space robots, and the other is having to review a 2,000 line pull request. Your reviewer will inevitably make themselves a strong cup of coffee, sit themselves down in their favorite chair and read the first 100 lines very carefully. They will then realize that there are 1,900 more lines of this lunacy to go, randomly suggest you rename a few variables and give a caveated “Lgtm, although I don’t have much context on this code”.

On the other hand, there are only two things in the world more calming than making a 50 line pull request. One of them is far too obscene to go into here, and the other is reviewing a 50 line pull request. Your reviewer can actually understand the change you are proposing and suggest meaningful design alternatives. You can respond to them, ship, and start on the next chunk.

Once merged, deploying your small change will be equally pleasant. There are few interactions that you need to worry about and few execution paths that you need to test. When your code does break, its small surface area will make rolling back relatively straightforward, and you will have fewer bugs interacting in fewer weird ways to worry about simultaneously. Small steps make it less likely that any of them will break anything too badly.

Small pull requests can allow you to move much, much faster. You have fewer interactions to juggle in your head, and fewer test failures to play whackamole with at the same time. Your code will be better; these small chunks will be reviewed, improved and battle-tested in production at a regular cadence. You won’t emerge from your code cave after 3 weeks smelling like feet with an enormous diff that is pivotally reliant on some profoundly erroneous assumptions. You can course correct faster and see if what you are trying to build is actually useful Lean Startup 5 Whys Lorem Ipsum Toyota Previa.

Raw line count is a simple and easy to measure metric for the “size” of your pull requests, but in many ways it is just an accessible proxy for “complexity”. Changing every single hyphen in your entire site to an em-dash might touch a lot of lines and a lot of files, but couldn’t be described as a “complex” change. On the other hand, updating multiple different config files can produce a 5 line diff with the complexity and scariness of a billion em-dash-updates. If your codebase is a molecule, then you should be looking to break your changes down to their simplest, atomic form, where breaking them down any further doesn’t make any sense and might even cause a strong-nuclear-force catastrophe.

Signs that you may need to split your diff include a high line count, many files touched, and any work that is taking more than a day or two. But perhaps the best indication is when a description of your changeset is impossible without the use of multiple “and also”s. Sometimes pull requests need to be on the conceptually chubby side, and sometimes your fundamental unit of functionality will just be large. But most of the time it won’t be. If something could reasonably be in its own pull request, it probably should. Think about what the smallest, incrementally useful thing you can possibly deploy is; often it won’t be the entire task that you are currently thinking about.

I was recently writing a new feature to allow my team to re-munge Widgets that have already been splunked. It turned out that I needed to refactor some of the Widget data model first, so I started doing this. It then turned out that in order to test this refactoring I in turn needed to refactor our Widget testing framework. My diff was expanding faster than the Ottoman Empire in the late 15th and early 16th centuries. Inspired, I split out the test framework refactoring, made a PR, got some feedback, argued that 30 characters is a perfectly reasonable length for a method name, and merged the PR. Next I split out the Widget data model refactoring and made another PR. Then I fixed a small oversight in the previous change that was causing some minor data inconsistencies. Finally I was in a position to add the 100 lines that actually allowed us to re-munge Widgets that have already been splunked. It felt good.

This is not even close to being science, but [I joined Stripe in March 2014](http://robertheaton.com/2014/03/07/lessons-from-a-silicon-valley-job-search/), and it took me 15 months to make my first 300 pull requests. It took me 4 months to make my next 300. I’ve written much better code, felt a lot calmer and several of my co-workers have commented on how I’ve even started smelling a little less like feet.