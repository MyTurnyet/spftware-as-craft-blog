---
title: Collaborative Programming... Remotely!
date: 2023-04-02 14:56:39 -0900
draft: false
toc: true
thumbnail:
    url: /img/remote-work.jpg
    author: Kristing Wilson
    authorURL: https://unsplash.com/@kristinwilson
    origin: https://unsplash.com/photos/person-in-blue-jacket-sitting-on-brown-wooden-chair-near-brown-wooden-table-during-daytime-z3htkdHUh5w
    originName: Unsplash

author: Paige Watson
tags:
- Collaboration
- Mobbing
- Tools
- Software as Craft
---

One of the most active topics at meet-ups and in online discussion groups in the last few months centers
around "what works" and "what doesn't work" when collaborative programming in our new era of all remote work. Over time,
the one list of "do's" and "don'ts" that has made it's way to the forefront of discussions is the list at
[remotemobprogramming.org][remotemobprogramming.org], compiled by Simon Harrer, Jochen Christ, and Martin Huber.

I'm going to go through their list and give a little commentary of my own. Not all of their ideas translate to the way
we work at all companies, but most can be applied even in a modified fashion to help us work better remotely.

So, let's jump in:

## Everyone Remote
While this doesn't directly apply to us all (yet), teams need to be 100% in the office, or 100% remote. Anything else
and no matter how you try to maintain open communication, there will be information asymmetry. One part of the team (
_usually the part that is in the office_) will have access to information that is not fully disseminated to the remote
members. This is why it's easy to feel disconnected or 'alone' when working remotely. When everyone's remote, all
information should be accessible (and optimally, shared face-to-face) to all team members.

## Camera on!
If you want the team to work collaboratively, you need to provide a collaborative environment. This means that we can
see and hear each other member of the team at all times. It takes a little getting used to at first but works best if
you have multiple monitors set up, so you can keep the video window small and off to the side, but still on the main
screen. The main idea is that you can see the other teammates as you are working collaboratively. Microphones should be
muted if you have background noise that would be distracting, but should generally be kept on. On my last team, this was
immensely helpful. Not only did it allow the developers to continue to collaborate in real-time, it also allowed
managers and PO's to "drop-in" with questions and issues, instead of waiting for email or MSTeams replies. This makes
communication faster and more effective.

## Small Team
I don't have to say much about this, as we already have small teams where I work. I believe they can be too small. The
smallest team size for teams that wish to work collaboratively should be four people. In a collaborative environment,
the smallest size of a working unit is a pair. There are times when more than one task needs to be completed at once and
three people do not split into pairs very easily. We are not able to maintain a collaborative practice if we can't
maintain a minimum collaborative working unit size for all of our tasks.

## Same Work Hours
This is **really important** to working collaboratively. Teams or specifically working groups (pairs or mobs), should
maintain the same working hours. This doesn't mean that you have to set a time frame in stone. It means that all the
people doing the work need to be online together for the time the work is being done. If you and I are pairing, and I
have a dentist appointment tomorrow, there's no reason we can't set working hours around that appointment.

Working groups should also agree on breaks and lunchtimes. You don't have to stay with your group, just have an
agreed-upon return time and be ready to resume working at that time.

## Typist and Guides
For a long time, I've called this "Driver/Navigator". The book "Code with the Wisdom of the Crowd by Mark Pearl" calls
the role at the keyboard "Typist". I like this better and am going to use this nomenclature going forward. [Llewelyn
Falco]( https://www.linkedin.com/in/llewellynfalco ) describes what he calls "Strong-style Pairing" by saying:

> "For an idea to go from your head into the computer it MUST go through someone else's hands".

The typist is just that: The person that enters the code into the computer. Everyone else guides the typist. I have
written a blog post about the Driver/Navigator process.

## Screen Sharing
Having tried several ways of pairing remotely, I agree with the idea that screen sharing is the best way that we
currently can collaborate. I've said it before: MSTeams is a presentation tool, not a collaboration tool. This helps to
enforce the Strong-type pairing as it is hard to share control of an IDE in MSTeams. It also allows us all to use to
customize our IDE to be more productive.

## 10 Minute Intervals
The [remotemobprogramming.org][remotemobprogramming.org] team uses 10-minute intervals for their rotations. The rotate the typist role every 10
minutes to "keep everyone concentrated and every opinion in the mix". I have tried different times, from 15 minutes to
as much as 30 minutes a rotation. I think this is something that the working group needs to discover for themselves.
Usually, a pairing rotation can be a little longer than a mobbing rotation.

The best way to decide this is to actually experiment with different times. Try 10 minutes, then after a couple of
rotations, take a few minutes to discuss whether lengthen (or shorten!) the time frame. Use a timer that everyone can
see. I like the Focus app (for a Mac), but I have also used several others like Micheal Vilar's Timer-app, and even the
[mob.sh][mob.sh] app has a built-in timer.

On previous teams, we would start with a longer time (25-30 minutes) and notice when one of the work group members
started to lose focus. This was often something as simple as glancing at their phone or looking around the room. We
would write the elapsed time on the window, and after several rotations, we would average the times and start again.
This would create a custom working rotation that was effective and productive.

## Git Handover
One of the most process-intensive aspects of remote collaborative work is the hand-over of work. When the rotation
happens, getting the code onto another person's computer can be confusing and frustrating. The easiest solution to this
is to share a screen and give control to the current typist. This poses several issues that could slow down the
work-group. Things like lag time, differences in IDE, and computer setup can make the team less productive. The tool
that the [remotemobprogramming.org][remotemobprogramming.org] group recommends (which was created by them) is the "[mob.sh][mob.sh]" app written in GO. I would
really recommend that you give this a try as it works quite well and allows each person to work on their machine when
it's their turn to be the typist.

## Group Decisions
One of the most important and positive things to come from collaborative work is Collaborative Decision-Making. Group
decisions are superior to individual decisions. Everyone on the team has the ability to contribute, discuss, learn, and
contribute. If we do not make Group Decision Making part of our collaboration work, it's not really a collaboration. We
shouldn't have one team member responsible for architecture and process decisions.

I'd love to hear your thoughts on this and am always open to discussion about how to continually make our processes more
effective.

[remotemobprogramming.org]:https://remotemobprogramming.org
[mob.sh]:https://mob.sh
