---
title: "Thoughts on Interviewing: II"
date: 2023-04-13 07:30:35 -0900
draft: false
description: Our interview process is broken.  Here's the second in a two-part series on my observations and ideas to fix the process.
thumbnail:
  url: /img/interviewing-2.jpg
  author: Cytonn Photogrphy
  authorURL: https://unsplash.com/@cytonn_photography
  originURL: https://unsplash.com/photos/two-people-shaking-hands-n95VMLxqM2I
  origin: Unsplash

tags:
  - Interviewing
  - Hiring
  - Software as Craft
---

In the [first part]["previous"] of this series, I talked a little about how our industry interviews
currently and some of the issues I have with the current process. In this post, I want to talk a little more about what
we should be doing in interviews, and who we're actually trying to hire.

First, let's talk about what we're trying to get out of our hiring process.

If the answer is: "A software developer" I would pose that we need to think a little deeper about what we really want
out of a candidate. While we often have ideas of what we need in terms of skill set, I don't think that skill set should
be anything more than a passing concern when considering a candidate.

Let's go a little deeper into what I just said. We often look at a candidates skill set and try and match it to what the
team needs right now. Which is fine if we're trying to fill a short term position where the work only consists of a
given skill set. I would put forth the idea that most teams are not looking for this (nor should they be). We should be
looking for a new team member. Someone that will bring experience, ideas, learning, growth, knowledge and learning to
the team (and the company). We want critical thinkers, and candidates that care about the quality of our code. We want
people that will have ideas about process, and how to make software in a more efficient, extensible, and sustainable
way.

Using skill set will not get you this person. Code challenges will not tell you much about a candidates ability. The
only real way to know if we are interviewing and hiring the correct person is to work with the candidate. We need to
learn whether a candidate can work alongside of other members of the team.

Can they communicate effectively?
Can the candidate use our tools (or learn quickly)?
Will they raise the level of the team?
Can they take (and give) instruction?
Will they bring additional culture to the team?
All of these are important and relevant to making sure we hire a great candidate.

Still, a person applying for a job as a software developer needs to know how to develop software. So let's start there:

## The Six Minute Interview

{{< link llewelyn-falco-li >}}Llewellyn Falco{{< /link >}} developed a challenge for gaining knowledge of a candidates
ability in a
fairly quick way. He calls it '[The Six Minute Interview]["six-minute"]'. I have written several versions of this
challenge and added
them to my personal GitHub repository.

This challenge works best online, and usually can be set-up as a fifteen-minute screen. The main idea is that after six
minutes, you can get a general overview of a person's ability, and most importantly, if you want to continue to see them
code more. After six minutes, if they aren't the right candidate, you can say "thank you" and hang up. This gives you a
simple way to finish a screen without crushing the hopes of a candidate. If you want to see more, you can ask them to
continue for another 30-60 minutes with the code that they've started, or just pass them onto the next step of the
process.

## Code Challenges

You'll remember that in the first part of this series, I talked about how I think white-boarding is not the answer.
Along with this, I believe that static 'code challenges' give us the same feedback as white-boarding. The candidate has
seen the problem before, or if not, they've looked it up online. Or, maybe they've actually solved it themselves. How do
we know?

I think the answer is to give them a challenge, but instead of asking them to return the finished product as a single
deliverable, we ask them to provide a link to a repository. The challenge we give should be a longer challenge, with
more than one component (ie: middle tier & UI, tests, etc). Not just a single problem, but an actual project. This
doesn't mean it has to be huge. Just large enough to see how a candidate handle different areas of development.

### Untimed

I heard people say "Timed challenges show us how a candidate works under pressure". Maybe this is true, but does it show
us the real ability of a candidate? I've been on the candidate side of the a timed challenge. We all have. Did you do
your best work? Did you do it correctly and take all the steps necessary to ensure you wrote quality code and the best (
as you know it) implementation? I didn't. I worked feverishly to just get it done. It was crap code and probably had
several bugs. Is this what we're looking for in a candidate? Someone who, when faced with a time deadline will write
crap code to just 'get it done'? I hope not. This is not the kind of company I want to work for, nor the type of
developer I want to work with.

Once I recognized that I was just writing code to get it done, I started practicing quality code practices for code
challenges. I often wouldn't finish, but I would be sure of the quality of the code I did write. Often, not finishing
would cause me to not move forward with the interview process. Fine. In the end I realized, I don't want to work a
company that values getting it done quickly over getting it done correctly.

The crux of this idea is: We should not be giving timed challenges. Candidates should be asked to complete a project
using their best practices to ensure it is maintainable, extensible, bug-free, and finished.

### Use A Repository

Asking them to provide a link to the code repository will enable us to view the process of software development from the
candidates point of view. We can look at commit history, and the evolution of the project. We can see how often they
committed and what changes came when. Did the candidate work on a branch, or master? Did they make a bunch of small
commits, or a few larger ones? Did they add effective commit messages?

We can see how they decided to structure the project. Is all the code in a single project? Are there
multiple projects, and if so, are they effectively laid out in the hierarchy? Are tests in the same project or a
different one? Does the project structure match what would be considered appropriate for the language that they are
using?

Once a candidate is finished, they should provide us 'contributor' access to their repository allowing us to see all
commits and merges.

### Feedback

Once the challenge is submitted to us, we should be able to provide constructive feedback to candidates on their code
challenge. This feedback can ask questions about implementation and practices, as well as include recommendations for
creating a better solution. Not only does this provide the candidate with insight into our company development ideals,
it allows them to learn and grow. A candidate should be able to defend their position on questions such as: "Why did you
implement this library?", "Was this the best structure for the solution?", and "What is the benefit of doing it this
way?". I would rather see a candidate defend their position, even if I think it's incorrect. The candidate should also
be able to take the feedback and learn from it. I'm looking for an ability to incorporate feedback that the candidate
thinks is a positive improvement to their solution.

## In Person Interview

Once a candidate is moved to the "in-person" level of the process, technical skills should known and no longer a focus
of the interviewer. The candidate has demonstrated technical aptitude and now we are looking at them to see if they will
be a positive addition to the team. This in-person time should not be wasted on white boarding or knowledge testing, but
should instead be used to make sure that both the candidate and the team are comfortable working together. The best way
to do this is to put the candidate into a scenario that has them work as they would if they were hired.

### Code Together

Be upfront and straight about expectations. If you expect the candidate to follow certain practices, like
paired-programming, or TDD, have them do it with the team. If possible, have the candidate work on production code and
be on a commit. This is, again, a time to see how well they receive and incorporate feedback. Do they ask the right
questions of the team? Many candidates are reticent to ask "Why" or suggest alternatives to what they're told during an
interview. Do they know how to write in a Test-Driven manor? Can they effectively pair? Do they want to do it all
themselves, or are they willing to work collaboratively?

### Personality Fit

One of the most important things I want to see in a candidate is the ability to learn from mistakes. Take time to ask
the candidate about mistakes they've made (not just in writing software), and what they've learned from it. A candidate
that can't (or won't) tell you about their mistakes during an interview is a red flag for me. Ask about a time when they
stood up for what they believed in, even if the outcome wasn't to their liking. Take time to find out about the
candidate as a person and think about whether you'd want to sit with this person for the next 6 months every day. While
you may not have to, it will give you a good idea of whether you feel comfortable with this person as a co-worker. Try
not to use the phrase "Tell me about a time when..." Most candidates have a ready made example that they've rehearsed
for this question. You may still get the pre-formatted answer if you ask a question in another way, but it may be enough
to nudge the candidate toward a more genuine reply.

### Don't make it a Test of Mental Toughness

Many people I've met talk about an interview as a time to really stress a candidate. This will "show how they work under
pressure". This is a horrible idea. Why do we feel this is necessary? If your team is under so much pressure that you
feel the need to test the candidate on how they react, you need to change the way your team works. As a candidate, I
would wholly reject any job that I felt was at a company that was interviewing me this way. Why would I want to work at
a company where conditions like this were 'normal'?

## Judgement Day

Finally, at some point (usually soon after the in person interview) a judgement has to be made. This is (obviously) the
most important decision in the process.

If you cannot find a good reason to say "Yes", the answer should be "No!"

Let me state that again. If you cannot give a good reason why you should hire a candidate, the answer should be to
pass. "They could work out..." is not a good reason. "They have the skills we want..." is not a good reason. "They seem
really excited about the job" is not a good reason. Too often we attempt to fill a position with a body just so we can
get someone to do they work. This will keep a company from moving forward and teams from growing to their full
potential.

Whether the answer is a "yes" or a "no", give the candidate as much honest and constructive feedback as you can in the
shortest time possible. A person will never get better or change if they don't hear this feedback.

It all comes down to hiring and ensuring we have a good fit for the team and the company. Hiring for software
development shouldn't be a body in seat process, nor should it be a search for "good enough". These are my thoughts on
the process and I would love to hear your feedback. Our industry is still new enough and our processes are
ever-changing, and because of this, we need to continually update and refine our hiring processes, not to find the
person
that fits the position, but the person that better the team and the company.

["previous"]:{{% relref thoughtsoninterviewing-1.md %}}
["six-minute"]:{{% relref sixminuteinterview.md %}}
