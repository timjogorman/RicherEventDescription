Part I. Introduction
====================

Where AMR captures "who is doing what to whom" within a particular sentence, multi-sentence AMR simply extends that to capturing "who is doing what to whom" within larger spans of text.   In practice, this means that we are taking a document or utterance where each sentence has already been given an AMR, and linking them up to a bigger unified structure.

Core Task
---------

We are doing three things in multisentence AMR:

- Linking coreferent variables across sentences 
- Putting implicit numbered arguments into those coreference chains
- Linking set/member and part/whole relations between variables

These are the same distinctions we make in normal AMR
-----------------------------------------------------

Remember that AMR does all within-sentence coreference, regardless of why you know that information.  This means that sometimes in AMR, we are merging two explicit mentions into the same AMR variable.  Remember that "He boy wants the girl to believe him" is AMRed as follows, with the "boy" and "him" merged together:

```
(w / want-01
   :ARG0 (b / boy)
   :ARG1 (b2 / believe-01
             :ARG0 (g / girl)
             :ARG1 b))
```

As another example, consider the three different instances of "b" in the following sentence:

"The boy ran off to California and arrived on Tuesday" 
```
(a / and
      :op1 (r / run-off-24
            :ARG0 (b / boy)
            :ARG2 (s / state :wiki "California" :name (n / name :op1 "California")))
      :op2 (a2 / arrive-01
            :ARG1 b
            :ARG4 s
            :time (d3 / date-entity :weekday "Tuesday")))
```

If this sentence were to be split into two sentence, our within-sentences would lose some of the information:

"The boy ran off to California. He arrived on Tuesday" 

```
(r2 / run-off-24
      :ARG0 (b3 / boy)
      :ARG2 (s / state :wiki "California" :name (n / name :op1 "California")))
      
(a3 / arrive-01
      :ARG1 (h / he)
      :time (d3 / date-entity :weekday "Tuesday"))      
```

In that shift, you lose the knowledge that the :ARG0 of ```run-off-24``` and the :ARG1 of ```arrive-01``` are identical, getting only a "he". You also lose the knowledge of the destination that was arrived at.  Re-capturing this kind of information leads to a guiding principle of this annotation: **we are making links across sentences that AMR would make within the same sentence**.  This means that we need to recover specific information:
 - We need to recover that "boy" and "he" are the same; more generally, we need to link together variables that refer to the same thing.
 - We need to recover that the ```:ARG4``` (end point, destination) of arrive-01 is California; more generally, we need to link unfilled numbered arguments to their referents in other sentences.

The third task -- marking set/member and part/whole relations -- will also be similar to within-sentence AMR intuitions. Imagine we had a single-sentence AMR that said:
```
"John had three cats, one of which was named Mittens"
(h / have-03
      :ARG0 (p / person :name (n / name :op1 "John"))
      :ARG1 (c / cat :quant 3
            :ARG2-of (i2 / include-91
                  :ARG1 (c2 / cat :name (n2 / name :op1 "Mittens")))))
```

If we split this up into "John had three cats.  One cat was named Mittens", then suddenly we are missing that "include-91" relation, and the underlying relationship between "three cats" and "one":

```
"John had three cats.  One cat named Mittens"
(h / have-03
      :ARG0 (p / person :name (n / name :op1 "John"))
      :ARG1 (c / cat :quant 3))

(c2 / cat :name (n2 / name :op1 "Mittens"))
```
So we'll need this set/member ("include-91") relationship between the two as well, so that we can know that Mittens is a member of the set of three cats.  This gives us our third task:

 3) We need to link arguments with Set/Member and Part/Whole relations when appropriate (include-91 and have-part-91, in ARM lingo)


Walking through some examples
-----------------------------

< placeholder for more introductory examples >


General Guidelines -- What Should I Put in Identity Clusters?
=============================================================

::bangbang:: *Remember the above guiding principles: we are trying to re-enact AMR coreference distinctions whenever possible.  Because there are many additional complexities, we will be including many additional guidelines and special cases, but remember to speak up if you feel that your annotations are deviating from within-sentence AMR behavior.*


Making Identical Relations
--------------------------

**One "Identical" chain should contain all variables and implicit relations that refer to that thing**

Re-entrancies within a sentence don't need to be linked (that's why we didn't give them markable boxes).  


**You are co-referring all kinds of concepts, as long as what they refer to is identical**

Namely, this means that you are linking not just people, places, things, etc, but also events and states.  Everything that's coreferential gets linked up!  (With a few exceptions described below). 


**An "Identical" chain can't only have implicit mentions -- you need at least one non-implicit concept**

You will run into instances where multiple implicit arguments clearly co-refer, but where there is no clear mention of who they refer to.  Do not go through and annotate these unless you have at least one non-implicit variable that is part of that chain.  


**Be strict about coreference: check whether "Set/Member" is a better label**

If what you are handling is actually and instance or a subset of a larger thing being referred to, don't conflate them into the same identity chain!  This will be particularly tricky with subsets, when you are talking about a group and get referents like "some of them...". Use Set/Member (which includes "set-subset" in its meaning) for such things.


**Be strict about coreference: don't corefer subevents with larger events**

If you are talking about one battle within a war, or one incision within an operation, or a particular discussion during a larger meeting, those are related by being what we call "Subevents".  It can sometimes be tempting to conflate these sometimes.  However, AMR instances do not, actually, merge these in AMR, and you should just leave them separate whenever possible.  Other, related annotation projects will actually annotate this "Subevent" data, so it will be cleaner for those projects if you don't consider such phenomena identical.


**DO link together dramatically different framings of the same underlying thing**

Let's say you see the AMRs for "*Bill went to Trader Joes. The fool forgot to buy cookie butter.*"  There will be a "(f / fool)" and a "(p / person :name (n / name :op1 "Bill")).  While it's true that "(f / fool)" is going more than *merely* referring to Bill, it is nevertheless still referring to Bill, and thus should still be in the reference chain.  

Do this for events when they are clearly referring to the same event, even if they are reframing that event.  If one sentence mentions "Bill's giving Sam a cookie" and another mentions "Bill's surrender to the forces of tyranny", if they refer to the actual same event, then they are the same. 

**Wikified mentions are assumed to be linked to each other**

Every entity with a ":wiki" link is going to be assumed to be linked up with every other mention.  That means that if you have an identity chain for "Bill Clinton", you don't need to link every instance of ```(p / person :name (n / name :op1 "Clinton"))``` together.  However, you still need to make links from at least one :wiki entry to the pronouns, implicit arguments, and other non-wikified mentions of that term that might exist.  

Naturally, if something has ":wiki -", it does not count as wikified for these purposes. 

Making Set/member relations
---------------------------

**Don't mark Set/member between Identity Chains already linked by "Include-91"**

Set/Member is the same as include-91, and shouldn't be marked redundantly. 

**Set/Member should follow the same rules as "include-91", and is used for both "set/member" and "set/subset" phenomena**

As mentioned above, you can link to *subsets* of a larger set, where it is not a single instance of the larger set, but many.

**Set and Member should be roughly the same kind of thing**

This is part of the definition -- you should be able say "<MemberOrSubset> is one of <Set>" or "<MemberOrSubset> are just some of <Set>".  A particular exception to this are collective reference to groups -- juries, populaces, etc. -- that have individual members.  Even though a given person is not an individual instance of 'populace', you can naturally treat 'populace' as a set.

Naturally, "same type of concept" should be based on your own general understandin of what is being talked about.  The literal "concept" that a variable refers to naturally can be different. 

**Do not mark Set/Member with "extremely generic" mentions such as "one", "everybody", "everything", etc.**

You will run into things that, on some technical understanding of meaning, might be sets that contain some large percentage of things mentioned in the document.  This does not mean they should be linked together.  

**You don't need to show that (a / and) is Set/Member with its :opX instances**

There are many times in AMR where one mentions things like "John and Mary to the store" or "China and Japan are competing".  You can assume that "and" loosely encodes a set/member relationship; you don't need to add "set/member" to all of our coordination instances, nor to add it between "they" and "John" in "John and Mary went to the store.  They bought a cat."

**Do not mark "predicative" assertions about a mention**

It may be obvious that the AMRs for sentence such as "John is foolish", only mention "John" once; foolish is merely a property of "John". 

But if one were to run into examples like "John is a fool", or "I consider John a fool", there might be more of a temptation to link "fool" into the "John" identity chain.  You should resist that temptation.  Because we are already capturing the predicative relationship -- through predicates like "consider-01" or with :mod or :domain relations -- we don't need to also add a coreference link.  

This will be hardest in instances like "John is the tallest man in the world". Even for these, we do not want these to be linked up.  For more details about this kind of particular edge case, see "assertions of identicality" in the Special Cases section

Marking Part/Whole relations
----------------------------

**Don't mark Part/Whole if any mentions are already linked with a :part-of relation**

Like Set/member and "include-91", this is the same as "have-part-91", so don't be redundant. 

**Part/Whole is about physical compositionality -- don't confuse it with "subevent" phenomena**

We are treating this entirely as being "X is a component part of Y".  Even though you might be able to say things like "this dance is part of the wedding" or "that incision was part of the surgery", you should **not** consider them part/whole for our purposes.  

**Part/Whole should not be used for organizational membership**

If someone is part of an organization, then the way to encode that is to link them together with implicit arguments on an instance of "have-org-role-91".  Part/Whole should only be used in the organizational senses when discussing company-company relations, like "Google is part of Alphabet". 

**Part/Whole is not for mere spatial inclusion**

The particular building your are sitting in might be, in some technical level, a part of your city, of your state, your nation, and the world. There's an extent to which 'being part of something', in that sense, is a hard-to-define concept.  But there are some prototypical entailments that should be largely present:
- Compositionality: If one were to make up a list of component parts of the whole, 


"Redundant" relationships
=========================

Redundant implicit arguments can be left out
--------------------------------------------

We will have a very specific idea of redundant: 

An implicit argument is *redundant* if 
- (A) Its predicate is in a coreference chain
- (B) There is a prior mention of that predicate using the exact same roleset
- (C) That identical predicate has the same numbered argument as the implicit argument itself. 
- (D) There is only one referent (identity chain) that has shown up in that particular role, for that particular roleset, for that predicate's identity chain.

In other words, if we have one part of a document in which one mentions:
```
"the cat was bitten by the dog"
(b / bite-01 
      :ARG0 (d / dog)
      :ARG1 (c / cat))
```
Consider a mention that later says:
```
"They were worried about the bite"
(w / worry-01
      :ARG0 (b / bite-01)
      :ARG1 (t / they))
```
This will show in our multi-sentence AMR Anafora annotations as:
```
"They were worried about the bite"
(w / worry-01
      :ARG0 (b / bite-01 
           :ARG0 (i / implicit-biter_agent)
           :ARG1 (i2 / implicit-entity_bitten))
      :ARG1 (t / they))
```      
If you have linked the two bite-01 instances together, then both ```:ARG0 (i / implicit-biter_agent)``` and ```:ARG1 (i2 / implicit-entity_bitten)``` pass this test, and don't need to be annotated. 

If you are at all uncertain about the identity of the referent, it is best to add this reference in.  We also need to emphasize that this **only** works if you have prior coreferent mentions of the **exact same predicate**.  


Special Cases and Additional Guidelines
=======================================

Assertions of Identicality
--------------------------

Hopefully it is clear from the prior guidelines that most "predicative" or "equational" constructions don't actually mean that you should link both mentions into the chain.  However, there is a tiny subset of cases where one really is getting links between two coreference chains, and claiming that those two chains are identical.  This is seen most clearly with things like:

- Clark Kent is Superman!
- I suspect Ted is the Zodiac killer.

This can occur for cases where one is not named, when there is an ongoing discussion of whoever did a particular thing

- I think mary is my secret santa.
- People think that OJ is the killer.

**DISCUSSION POINT / PROPOSAL**: We will treat these with this "marginal-identity-91" operator. 


True generics (synonymous with "one","everyone") should not be linked to implicits
----------------------------------------------------------------------------------

AMR annotations are full of concepts such as "recommend-01" (used for modal verbs like "should"), where the recommender isn't really clear, but might construed as being "people in  general recommend that...".  "John is funny" can be constued as "People find John funny".    It might be tempting, therefore, if you find a nice generic like "people" or "one" or "everyone", to link up all these implicit arguments to such as generic.  **Resist that urge!**.  Since that is a can of worms, consider it to be explicitly forbidden to link to such terms.

Don't link up generics (that you wouldn't link in AMR)
------------------------------------------------------

As a clear-cut example, look at the AMR for the following sentence, and note that we have two different monetary amounts, each in a unit of "dollar". Indeed, both mentions of dollar are referring to teh same thing -- the general idea of US dollars.  But we nevertheless don't corefer them -- it would be wrong to replace "d2 / dollar" with a mere re-entrant variable "d3":

```
The government 's borrowing authority dropped at midnight Tuesday to $ 2.80 trillion from $ 2.87 trillion .

 (d4 / drop-01 
	:ARG1  (t / thing 
		:ARG1-of  (b / borrow-01 
			:ARG0 g 
			:ARG1-of  (a / authorize-01 
				:ARG2  (g / government-organization 
					:ARG0-of  (g2 / govern-01))))) 
	:ARG3  (m2 / monetary-quantity 
		:quant 2870000000000 
		:unit  (d3 / dollar)) 
	:ARG4  (m / monetary-quantity 
		:quant 2800000000000 
		:unit  (d2 / dollar)) 
	:time  (d / date-entity 
		:time "0 
		:weekday  (w / wednesday))) 
```

We do not link these "dollar" elements.  While technically you might say that they are talking about the same generalized idea of dollars, nothing is added by linking them together. Another way to say this is that, since "dollar" is a generic word without need of context, coreference of "d3" and "d2" adds no information to our AMRs. 

As a general rule, you can avoid coreferring things that are "generic", but you shouldn't be too strict about any exact definition of genericity; start with that definition and then try to calibrate to how this has been annotated in within-sentence AMR.  A good example of things that we are keeping slip are the two mentions of "economy" in the following AMR, used in "economic block" and "economic war":


```
I would suggest an economic block and the sharing of nuclear technology within this block to ensure their sovereignty from both military and economic war.
 (s / suggest-01 
	:ARG0  (i / i) 
	:ARG1  (a / and 
		:op1  (b / block 
			:mod  (e2 / economy)) 
		:op2  (s2 / share-01 
			:ARG0 b 
			:ARG1  (t / technology 
				:mod  (n / nucleus)))) 
	:purpose  (e / ensure-01 
		:ARG0 b 
		:ARG1  (s3 / sovereignty 
			:topic  (a2 / and 
				:op1  (w / war-01 
					:mod  (m / military) 
					:mod  (e3 / economy)) 
				:op2  (w2 / war-01) 
				:mod  (b2 / both)) 
			:poss b))) 
```

Or the two mentions of "politics" in the following:


```
There are far more important political and economical reasons for military intervention or political sanctions.
 (r / reason 
	:mod  (p / politics) 
	:mod  (e / economy) 
	:mod  (i / important 
		:degree  (m / more 
			:degree  (f / far))) 
	:ARG0-of  (c / cause-01 
		:ARG1  (o / or 
			:op1  (i2 / intervene-01 
				:ARG0  (m2 / military)) 
			:op2  (s / sanction-02 
				:ARG2  (p2 / politics))))) 
```











Handling Errors in the AMRs
===========================

There are a bunch of issues that you might encounter that are essentially caused by issues in the original AMR annotation.  

AMR missed a within-sentence reentrancy
---------------------------------------
You **are** allowed to link within the same sentence, but only in the case of errors, where you believe the original AMR should have merged those into a single variable. Simply treat them like normal mentions, and link them to your identity chain normally. 

AMR annotation has conflicting :wiki values for the same identity chain
-----------------------------------------------------------------------
If you run into this situation, annotate an identity chain as normal, but make sure that every instance of this term is brought into the same identity chain. During quality control we will check for whether a given chain has multiple :wiki links; all you need to do is catch the error. 

Removable components in equational clauses
------------------------------------------

Remember that in the AMR guidelines, "the boy is a hard worker" is AMRed as:

```
(w / work-01
      :ARG0 (b / boy)
      :manner (h / hard-02))
```

You may run into cases where this kind of thing is instead annotated as 

```
"the boy is a hard worker"
(p / person
      :ARG0-of (w / work-01
            :manner (h / hard-02))
      :domain (b / boy))
```
**DISCUSSION POINT / PROPOSAL**: In this case, annotate BOTH mentions as coreferential; we may go through and fix the issue. If you find yourself doing this often, however, bring it up immediately with your annotation team to make sure you are making the right judgement calls. 



Decomposition Issues
--------------------

You'll notice that a word like "drawing" might sometimes be AMRed as:
```(t / thing :ARG1-of (d / draw-01))```

You might see it sometimes done as:
```(d / drawing)```

or even as:
```(d / draw-01)```

In these cases, we are essentially dealing with two, intertwined reference types -- the result of a drawing event, and the act of drawing.  If at all possible, you should simply assume that these are two separate identity chains, and try to assign each mention to one chain or the other. 


