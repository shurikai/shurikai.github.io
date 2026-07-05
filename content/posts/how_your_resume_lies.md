+++
date = '2026-07-04T20:15:59-04:00'
draft = true
title = 'How Your Resume Lies While Telling the Truth'
+++

The most dangerous thing that can happen with your resume when working with an LLM to optimize for job applications isn't an
outright lie. It's a completely believable exaggeration.

`Led the decomposition of monolithic Java applications into modular Spring Boot services, defining service boundaries
and communication patterns to support independent feature development.` Sounds good, right? It does, except what really
happened was more like `Part of a six-person consulting team decomposing a legacy monolith for a large financial services
client. I worked on service boundary decisions and some of the Spring Boot implementation. One of several engineers on the
project.` That bullet made it into exactly one application before I caught it. One. And I could have missed it even then.

It's not true fabrication by the LLM, but rather something harder to catch and individually defensible. It's *plausible exaggeration* of
the actual truth. I did all of the things in that sentence, but the first word, `Led`, brings with it a connotation that just isn't true.
The danger of this type of error is not a gross level of exaggeration, but rather the fact that it usually takes at least two or three
resume generations to go from 'Contributed to' to 'Led'. It's the proverbial frog in the boiling water - the change is gradual enough
that even a careful person *just misses it*.

It would be easy to look at that sort of pattern and throw out a blanket 'LLMs lie', but if you really dig into the mechanics of what
is going on, you'll see that there is a structural reason that this sort of drift occurs. The LLM chooses to optimize for the wrong
signal in this case. The model is trained to produce compelling output, and in this case 'Led a cross-functional initiative' is way
more compelling than 'Was one of six people working on one'. Here, the *accuracy* is more important than the *fluency*, but the model
doesn't realize that its modification is getting slightly further from actual fact.

So, how do you defend against this sort of drift? How do you reduce the tendency to keep adding slightly to inaccuracies when generating
a resume? The best defense is simple: start from one human-authored source of truth describing your work history in
precise terms, always generating new versions directly from that source. If you *do* end up with an exaggerated claim, it won't be large,
and it won't be compounded in the next pass through the process. It will be terminated before it ever really begins.

If you've run your own resume through an LLM recently, take some time and review it for your own version of 'Led'. It's probably in
there. Especially if you've done it more than one time.
