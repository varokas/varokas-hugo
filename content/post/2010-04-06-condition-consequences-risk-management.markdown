---
author: varokas
comments: true
date: 2010-04-06 03:59:30+00:00
layout: post
slug: condition-consequences-risk-management
title: Condition-Consequence Risk Statements
wordpress_id: 127
categories:
- Software Engineering
---

I remembered somebody told me that good software managers are good risk managers. I tend to agree with that specific statement. The dramatic amount of delays we faced usually results from us overlooking some tasks (checklists and estimation techniques help in this one) or us unable to understand our project risks and deal with them accordingly (such as your vendor going out of business..).


### Risk Statements


Okay, great! Lets get some risks on the table, then.



	
  1. What if my company decides that they are not going to fund this project any more?

	
  2. What if Microsoft drop all supports for .NET platform?

	
  3. What if the PC I have got a virus and I have to send them to repair for 3 days?

	
  4. What if my project manager is hit by a train?

	
  5. What if the planet is hit by an asteroid, wiping out all major continents, humanity ceases to exist and all that we know as a civilization is gone?


I could go on and on (I am very good at these things) but I can imagine people eyebrows raised more and more from (1) to (5). What is it that makes (1) more likely to be happening than (5)? Can you point out which ones are actually useful?

In matter of fact, none of them has any value for risk management at all. They are not based on a factual context of imminent threats. In risk management, we do not seek to understand and mitigate every possibility of the universe. We just need to know what events are likely to happen, justified by some knowledge of current status, and plan to deal with them accordingly.


### Condition-Consequence Risk Statements


Let me try this again.



	
  1. The company memo indicates a transformation into an IT consultant, this project might not be funded anymore.

	
  2. Microsoft begins to phase out their platform supports prior to 2007, we might have to rework the UI module as it relies solely on .NET.

	
  3. The company firewalls is currently disabled, We might have to face with outage from a virus.

	
  4. My project managers has got to cross this unguarded and poorly lit train tracks every night, he might get hit by a train.

	
  5. (okay... probably let this one go)


Now it seems to hold more water, doesn't it. What actually happens here is that you put factual elements (the underlined part) into risk statements. Essentially what you said is: "Based on this fact, I believe this is going to happen". The underlined part should be hard, cold, non-controversial fact. The part that follows are your predictions based on the stated facts. Assessing their impacts and probability is another day's story.

And remember to keep it short. Less than 30 words (just like the example) is more than enough to capture your concerns. It always looks redicoulous to me when people tried to elicit their risks using huge pile of forms, resulting in one phone book of risks that nobody cares about. This is bad. This is actually even worse than no risks management, because at that point you already wasted time on collecting them.

While this kind of risk statements seems overly simple by traditional standards, the method is actually in used and published by [NASA ](https://docs.google.com/viewer?url=http://process.nasa.gov/documents/riskmgmt.pdf)(Page 6) and its [Goddard Space Flight Center ](https://docs.google.com/viewer?url=http://standards.gsfc.nasa.gov/gsfc-std/gsfc-std-0002.pdf)(Page 8, signed May 2009). Yes, you are looking at the agency that had sent people to the moon, landed rovers on mars and shot satellites into deep space. I am sure that they have got a lot of stuff that could go very very wrong. Yet they seems to live in peace with their risks that is managed based on facts rather than series of pessimistic opinions. Unless your projects goal is to explore the Pegasus galaxy, this should be sufficient for your needs.


### A Question to Agile Evangelist


The reason why I bring this up is I have not seen Agile projects manage risks before (at least not explicitly), and the topic is not so popular among Agile community. They might discard this idea quickly probably because of the bulkiness of traditional risk documentation methods.  Given this lighter-weight risk statements, it might begins to make sense for Agile teams to put 2-3 of these statements up with their iteration plan. This should helps the whole team understands what are the things to watch out for, not just managements. Then we could revise it every iteration to be up-to-date. Any thoughts? See you in the comments.
