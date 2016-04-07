


Part I. Introduction
====================

Where AMR captures "who is doing what to whom" within a particular sentence, multi-sentence AMR simply extends that to capturing "who is doing what to whom" within larger spans of text.   In practice, this means that we are taking a document or utterance where each sentence has already been given an AMR, and linking them up to a bigger unified structure.

This will be a task very grounded in how we do AMRs on single sentences.  For example, consider the three different instances of "b" in the following sentence:

"The boy worried, fearing he would not get a present"
```
(w / worry-01
      :ARG0 (f / fear-01
            :ARG0 b
            :ARG1 (g / get-01 :polarity -
                  :ARG0 b
                  :ARG1 (p / present)))
      :ARG1 (b / boy))
```

This "b / boy" gets mentioned for every element where the "boy" is the proper argument.  This means that within-sentence AMR is handling not only pronouns (boy <-> he) but arguments of predicates such as "fear", where we know that the "boy" is the person who is afraid.

If this sentence were to be split into two sentence, we want to be capturing roughly the same information.  

"The boy was worried. He feared he would not get a present"
```
(w / worry-01
      :ARG1 (b / boy)

(f2 / fear-01
      :ARG0 (h / he)
      :ARG1 (g / get-01 :polarity -
            :ARG0 h
            :ARG1 (p / present)))
```
We lose two things when that happens:
 - We need to now recover that "boy" and "he" are the same
 - We need to now recover that the thing worried about (":ARG0") is "fear-01".

More generally, the idea is that we need to:
 1) Do document-wide coreference between variables -- like "b / boy" and "h / he" -- so that we know when they refer to the same thing.
 2) We need to link unstated arguments -- such as the ":ARG0" of worry-01, above -- to the things they refer to.

There is a third, related task.  If we had a single-sentence AMR that said:
```
"John had three cats, one of which was named Mittens"
(h / have-03
      :ARG0 (p / person :name (n / name :op1 "John"))
      :ARG1 (c / cat :quant 3
            :ARG2-of (i2 / include-91
                  :ARG1 (c2 / cat :name (n2 / name :op1 "Mittens")))))
```

If we split this up into "John had three cats.  One cat was named Mittens", then the thing we are missing is not actually strict coreference, but rather is the relationship between "three cats" and "one", which we used "include-91" for above: 

```
"John had three cats.  One cat named Mittens"
(h / have-03
      :ARG0 (p / person :name (n / name :op1 "John"))
      :ARG1 (c / cat :quant 3))

(c2 / cat :name (n2 / name :op1 "Mittens"))
```
So we'll need this set/member ("include-91") relationship between the two as well, so that we can know that Mittens is a member of the set of three cats.  This gives us our third task:

 2) We need to link arguments with Set/Member and Part/Whole relations when appropriate (include-91 and have-part-91, in ARM lingo)


Walking through some examples
-----------------------------

< Here's where we introduce the editor more thoroughly; I'm skipping that for now>


General Guidelines -- What Should I Put in Identity Clusters?
=============================================================

"a / and" can be in a coreference chain when relevant
-----------------------------------------------------
Assume you have the following:
```
John and Mary ate dinner.
(e / eat-01
      :ARG0 (a / and
            :op1 (p / person :name (n / name :op1 "John"))
            :op2 (p2 / person :name (n2 / name :op1 "Mary")))
      :ARG1 (d / dinner))

They even ordered dessert.
(o / order-01
      :ARG0 (t / they)
      :ARG1 (d2 / dessert)
      :mod (e2 / even))

Naturally, the "John and Mary" should be linked to "they".  There are two specific things to remember about how:
 - "a / and"  can be used to represent the set of its arguments (in this case, John and Mary)
 - You don't need to add a "Set/Member" relationship between "and" instances and their component parts -- you can assume that they are generally there.









Reference that also makes statements about things
-------------------------------------------------

##### References that merely happen to be predicative

Let's say we have:

*Bill went to Trader Joes. The fool forgot to buy cookie butter.*

Now that mention "the fool" is admittedly doing two things -- referring to Bill, and making a statement about Bill.  Nevertheless, since it's a way of referring to Bill, you should add its variable (likely ```(f2 / fool)```) to your "Identical" cluster for Bill.  

In contrast, there are a bunch of things that we'll have to handle that are more complicated in this regard:


##### Decision Point: Identity or something else?  Allegations and identity linking are complicated. 

I'm putting the pros and concs into an endnote.  Ideally we want this to be handled elegantly for within-sentence AMR, rather than coming up with a special case for cross-sentence AMR. Some can be in an "Alledge-Identity" or something, but it's complicated.












### Equational/Copular/predicative issues

##### Remember the core AMR drive to reformulate equational constructions as predicates. 

- "John is a pilot for Southwest", "John is mary's doctor", etc. become "John has a pilot role in Southwest" and "John has a relational role of "doctor" with Mary".  In that kind of formulation, it is hopefully clear that we don't need two separate persons. 

- The example we give in the AMR guidelines is "the boy is a hard worker", which is AMRed as:

```
(w / work-01
      :ARG0 (b / boy)
      :manner (h / hard-02))
```
We don't need to even consider the two options when these are treated correctly, because there's only one referent. 

##### DISCUSSION POINT: what to do when these are wrong

- If someone annotates this as :
```
(p / person
      :ARG0-of (w / work-01
            :manner (h / hard-02))
      :domain (b / boy))
```
- Option 1: Tim's preference: Special code for this
- Option 2: These are both in "IDENTICAL" clusters


##### Genuine identity predications:

There's a small set of things that are done in AMR as ":domain", but really are identical, or are assertions of identicality:
- "Clark Kent is Superman"
- "Ted is the Zodiac Killer"

**DISCUSSION POINT, proposed language.**: Anything of this sort, where the document is positing identity between two identity chains, but where it's problematic to actually link them, should be done with the **allege-identicality-91**.  Note that this should be **very constrained in use*; anything that's just genuinely identical should be left out of this


##### Predicative things

A similar issue are things that could nominally be part of a chain or not.  Occaisionally these very transient references could actually be in their own coreference chains, as in:  
- "Bill thinks  Hillary will be the winner.  The winner will battle with Trump in the fall, and they will probably win."
- "John might be the tallest person in the group.  Whoever it is, they should wave our flag."

In these kinds of cases, we are clearly building a separate "Identical" chain for the tallest person in the group.  But what are you doing with something like:

- "John is the tallest person in the group."
- "I consider Bill an idiot"
- "We're treating this as assault"

For each of these, the "John" chain only links to "John", the "Bill" chain only links to "Bill", etc.  Many of these can be viewed as being "predicates" -- Jon is the tallest person" is a lot like "John is taller than everyone else"; "John is an idiot" is a lot like "John is idiotic".  A sentence like "John is an idiot" is being treated by AMR as saying "John has a property 'idiot'":
(i / idiot
   :domain (p / person :name (n / name :op1 "John")))
Thus, you don't want to pretend that that property "idiot" is the same as "john"; it's just a property. 











What Isn't Coreference
======================

Use Set/Member -- not coreference -- when related specific instances to kinds
-----------------------------------------------------------------------------

Two of these example sentences are:

< picture of a boa constrictor swalloing an animal>

< it said ...boa constrictors swallow their....> 


"Subevent" phenomena do not count as identity, and aren't annotated in this pass
--------------------------------------------------------------------------------

Sometimes you might see two events that are different granularities of the same actual event.  One might see one mention of "chewing food" and another of "eating dinner".  If it's clear that one concept is *part of a number of events that constitute the other concept*, then they are **not** coreferent.  This matches what you will see if you look at our within-sentence AMRs; as a rule, we do not conflate different granularities of events; we simply mention them all, usually without clear links between them. 

If it's any re-assurance, some of this data will undergo a later pass in which subevent relations **are** added.  So being strict about coreference when coreferring event-y concepts will be very helpful in providing later clean annotations. 



True generics (synonymous with "one","everyone") should not be linked to implicits
----------------------------------------------------------------------------------

AMR annotations are full of concepts such as "recommend-01" (used for modal verbs like "should").  It might be tempting, when given a nice well-defined explicit generic like "people" or "society" or a generic "you", to link them to other generic "you" instances.  The kind of "you" mentions that you see in the following AMR (which could be replaced with "...going through one's  house...")

The idea of some one going through your house is as bad as them taking Christmas presents.

(i / idea 
      :ARG1-of (b / bad-07 
            :degree (e / equal) 
            :compared-to (t / take-01 
                  :ARG0 s 
                  :ARG1 (p / present 
                        :mod (f / festival :wiki "Christmas" :name (n / name :op1 "Christmas"))))) 
      :topic (g / go-02 
            :ARG0 (s / someone) 
            :path (h / house 
                  :poss (y / you)))) 

- "you", when it applies to "anyone reading this sentence", should not be linked up with anything, nor should "one"
- This is relatively low frequency, but it's important because many implicit arguments could be construed as having that meaning, and we *don't* want you do













Decomposition Issues
--------------------

You'll notice that "picture", "drawing" and so forth are often represented in AMR as "thing :arg1-of draw-01".  This is a common treatment in AMR, especially for some kinds of nominalizations[endnote].  It also poses some problems: sometimes you will encounter systems in which one instance of, say, "drawing" is simply "drawing" and others where it is "thing :arg1-of draw-01", and others where it is "draw-01".  



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
"I would suggest an economic block and the sharing of nuclear technology within this block to ensure their sovereignty from both military and economic war."
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

# ::snt There are far more important political and economical reasons for military intervention or political sanctions.
```
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







Multi-sentence freak show: 
--------------------------


### "Three people left early.  One was Susan." vs "Susan was one of the people that left"

Within-sentence constructions and cross-sentence sequence patterns that encode Set/Member relationships should do just that.  So for AMR purposes, the relationship between "three people" and "one person" is going to be a clear-cut Set/Membership relation -- either one that you add, or one that's already present in the AMR as "include-91".  

(l / leave-11
   :arg1 (p / person :quant 3)
   :time (e / early))

(o / one
   :domain (p / person :name (n / name :op1 "Susan")))

However, if we had this in a single sentence, that "one" would not be present, as in:

"Susan was one of the people that left"

We would NOT see that "one"; annotators would hopefully capture the real meaning of:

include-91
   :arg2 person :quant 3
           :arg1-of leave-11
                  :time early
   :arg1 (p2/ person :name (n / name :op1 "Susan")))

So you will, in the same vein, want to ignore the "one" and encode the Set/Membership directly, encoding that "p / person :quant 3" in sentence 1 is a set containing Susan from sentence 2.

(l / leave-11
   :arg1 (p / person :quant 3)
   :time (e / early))

(o / one
   :domain (p / person :name (n / name :op1 "Susan")))







Appendix A. Theoretical and Background Considerations
=====================================================

[bridging endnote] Note that we are actually making a slightly different and more ontological judgement than "bridging" in the sense of Clark 1974 and later work.  There's a sense of "bridging" in which a given term is known to be in the common ground, or that a given sentence is known to be coherent with prior text, **because** of a relation such as part/whole or set/member.  We don't assume that our anotations are capturing any sort of coherence-relational, information-structural or cognitive relationships between the terms.  In that sense, technically by saying "bridging" we are just lumping a bunch of real-world relations between terms that happen to also lead to a "bridging" anafora. The tradition of "bridging" annotatoins in actual corefrence structures largely goes back to Poesio (XXXX).

[implicitness-endnode] We had to take a stance regarding whether multiple, coreferential mentions of the same unstated term should be coreferential.  This is a complicated question.  There is actually a scale of possible kinds of annotation here.  
At the "least reasonable" end would be linking non-explicit mentions with multiple mentions, when referring to the same event:
- Bill ate at noon.  He ate voraciously but unthinkingly, never leaving his desk.
The "thing "eaten" in such a context is mentioned twice, but as multiple mentions of the same coreferential event.  This is particularly troublesome because some propbank numbered argumetns are not as mentally salient (in the sense of being implied to exist, as in Gawron and Condoravid's "Existential" or Framenets "Indefinite Nul lInstantiation").  For example, to refer to the example from the guidelines:
"Sally threw the ball to bob. she threw it very hard"  
Both of these throwsa will have an ARG2 "distance thrown".  While it's true that the distiance thrown is going to be the coreferential, it's ahrd to pretend that this kind of link matters.  These issues arise even with non-coreferential arguemtns that are nevertheless part of event scripts, as in "sally threw the ball to bob, it floated over the plate", "we got together to brunch, but Suzie didn't eat", or "Bill was assaulted and punched in the face", all of whichinvolve not only unstated argumetns with corefernce information, but in which there can be wdie variance about whether or not the terms are coreferential (e.g. Bill may have been assaulted by five people, but likely only one of them punched him in the nose). 







# RED+AMR Entity Coreference Pass Guidelines

- We are labeling each entity we find as a Discourse Entity.
- Usually these are mentioned many times in a document, and each coreferent mention is put into the same Entity chain. 
- We are making a simple distinction between whether they a single unique entity, a bunch of members of a set of entities, or the actual definition of a set.
- We will also relate these Entity chains with relations like set/member and whole/part when they are related in ways that are not exactly coreference.
- Are are **only** looking at entities (not "events") in this pass.  

## Entity Referentiality -- What do we mean by "Entity"?

For entities, we look for a participant, location, organization, or other kind of things that might be tracked in the discourse. These are generally physical things, organizations and groups with some kind of physical presence, and some ideas. 

###### The "Playbill" heuristic

- One test for entity status is "who and what participated in this document's events?". 
- We are therefore NOT capturing non-entities like "nobody", which don't ground out in any kind of referential entity.
- We can think of this as asking what kinds of entity and events in our document should go into a knowledge-base or other big inference system. If we say "the man with the moustache", nobody is going to imagine tracking his moustache. 
- But we ARE looking at things that might have a "fuzzy" reference: "someone stole my speakers" refers to an entity even if you they aren't specific to the speaker. 

###### The "referentiality" heuristic

- Another test of the same question is whether an entity is "referential"
  - Could you refer to it with a pronoun in the sentence after it is mentioned?

###### The "cross-document" heuristic

- Could you imagine another document in which this object or person was also talked about or referred to? 
  - More precisely: "How fanciful and convoluted do you need to get in order to imagine another document referring to this entity?"

### What is **not** referential

##### Concepts used to define other entities are not entities
- Even concrete objects, if used to merely define the object in question, are not entities.  "donut" in "donut shop" or "police" in "police box" are not necessarily referential entities, since they are simply defining the nature of the object. (see exceptions below)
 - Relatedly, **attributes** of objects are generally not entities in their own right. 
- Exceptions: when an entity is more strongly referential elsewhere, or is a named entity (e.g. as in "Mary's car").
 - Document-level topics matter for this: we don't want "hot dog" in every mention of "hot dog stand" -- *even if we had three mentions of hot dog stand* --  but if our document was, for example, about food poisoning outbreak linked to "hot dogs"), then we would *do* want to keep track of every mention.  


##### Implicit Arguments (in light blue) are not entities unless coreferent with an explicit mention
- Anything without an explicit mention in the chain will be deleted in post-processing. 

##### Details of events are not entiteis
- Entities that can be viewed as natural components of an event should not be treated as separate entities
  - If you talk about two people playing frisbee, the "frisbee" may be a real object, but its relevance is tied to the event of playing frisbee.
  - If one might consider the sentence to *only* be introducing the event, and the entity is merely entailed, then it's not an entity. 
  - Can paraphrase the sentence without mentioning the entity as individuated from the event, or imagine a language in which you could? ("Let's frisbee on Tuesday!")

### Additional Details
###### Some things are assumed to be entities (no need for an Entity chain)
- Entities with :wiki links start as part of an existing Entity chain, and those with :wiki links other than ":wiki -" start with coreference to each other. 
  - Occasionally, these :wiki chains need to be re-examined.
      - "Someone stole my iPod" ... "I bought a new iPod to replace it"
      - Both might be (p / product :wiki iPod :name (n / name :op1 "iPod")), but should not be in the same chain
      - The "WikiRelation" box has a default to "IDENTICAL", but in these cases needs to be changed to "SetMember". 
- If you mark whole/part relations without marking the part as being an entity, it will be assumed to be a singleton.

###### Attributes and parts can be Entities when relevant

- We don't want an entity chain for "hands" in "the orange man with the small hands"
- Same for properties (we don't want "orange" either)
- Attributes and parts should be referential only when effected, or when they cause, enable or prevent some other activity
  - "This was a [racially] motivated attack", "we try to hire based on [competence]"


###### Objects, sublocations, and low-prominence entities

- Objects are non-referential if **merely** descriptions of an event manner, and if there's no chance of them having relevance outside of that event. 
   - **Disclaimer**: You need to use a tiny bit of world knowledge here: murder weapons and dining utensils are both instruments, but you know that the ongoing referential identity of a murder weapon matters, and the ongoing referential identity of a spoon does not. 
- Similarly, relative positions and distances are not entities, unless coreferential or otherwise clearly defining a "spot" 
- Ideas are only to be treated as entities when particular definitions of that entity are being discussed ("I dislike Romney's flavor of [capitalism]"), or when coreference is necessary for understanding. 
- Time expressions are not entities (we will get them in a later pass)
- Most quantities, if modifying something else with a ":quant" relation, will not be entities themselves.  If they are alone in the world, however, they might be (e.g. "Do you have the $1000 dollars?").

 
  
###### Referentially Bare Situational Unique Destinations

- "I went to work" , "I spent a week in hospital", "little Billy ran off to school", all refer to a unique entity in the world (the school, hospital, etc.), but in a way that seems to be part of the event itself.  
- For the sake of consistency, we treat these as referential and unique every time (*This is an exception to the referentiality rules above*). This allows us to be more consistent when we *do* get explicit mentions of one's workplace, school, hospital, etc.


##### Differentiating Entities from Events (is this something I'm annotating on this pass?)

There are two core rules here:
- If in doubt about the EVENT/ENTITY distinction, default to EVENT (i.e. don't mark it as anything in this pass).  
   - If you can imagine a coreferential form of this that is clearly an event to you, then treat this one as an event as well
   - Predicates (things with a Propbank roleset) are rarely part of entity chains; they should either be dealt with in the second pass are not referential at all. 
   
- If something represents both an ENTITY and an EVENT, you can annotate both -- as an ENTITY in this pass and then as an EVENT later. 
   - This is NOT for things that are ambiguous (see above), but only for when **both and entity and an event are implied**. 
       - The nearby pipe **[<sub>event & entity</sub> bomb]** disrupted the festival.
       - I kept Mary's **[<sub>event & entity</sub> text]**.
       - Some portion of these coreference chains will often *already* be split up using ```(t / thing :ARG1-of ...)``` constructions.
   - Do this only when the entity reading is strongly implied:
     - Texts, messages etc. are not entities (only events) unless there is discussion of their recorded or stored form.
     - Reports, summaries, etc.; if and only if one is talking about the physical or electronic form (I can't find the report), the release of an official report, etc.
     - Laws, acts, rules etc.: Only when talking about a particular law or act, rather than a general prohibition.  Being legal or against the law is more of a state than an entity. 
     - Weapons and their impact: Only when talking about the weapon/disease/virus itself rather than its deployment/consequences: I found [the virus] on my computer.
    - Be exceedingly sparing with such "dual" annotations

### Calibrating your instincts:

```
Mr. Vinken is chairman of Elsevier N.V. , the Dutch publishing group .
(h / have-org-role-91
      :ARG0 (p / person :wiki -
            :name (m / name :op1 "Mr." :op2 "Vinken"))
      :ARG1 (g / group :wiki "Reed_Elsevier#Elsevier_NV"
            :name (e / name :op1 "Elsevier" :op2 "N.V.")
            :mod (c / country :wiki "Netherlands"
                  :name (n / name :op1 "Netherlands"))
            :ARG0-of (p2 / publish-01))
      :ARG2 (c2 / chairman))
```
**entities**: p / person (g / group and c /country are entities, but already wikified)

```
There is no asbestos in our products now . ''
(a / asbestos
  :polarity -
  :time (n / now)
  :location (t / thing
              :ARG1-of (p2 / produce-01
                         :ARG0 (w2 / we))))
```
**entities**: t / thing, w2/ we


# Quantification -- Which box do I put a particular mention in?

### Unique

- Unique does **not** mean grammatically singular
- Unique means that the entity chain refers to a single entity in the world (or maybe in a possible world), or a single grouping of entities, **and identifies it as a single unit**. 
- If "w / wug" is a mention in the unique box, you can say (in a separate sentence) "This refers to exactly one wug".

### Multiple

- Anything that cannot pass the test of "there is just one X"
- Also this is not synonymous with English grammatical plural, things that are plural will be Muliple (or the "FullDefinition" category below). 
- Is anything *quantifiable*, regardless of whether it's discretely countable ('there are 12 wugs') or a mass ('there are four pounds of wug', 'i have a jug of wugs',etc.). 
  - This means that even when there's variation between plural (as in "these data validate our hypothesis") and mass (as in "the data is inconclusive")
- Ignore whether this is treated collectively or distributively!  Even for something extremely distributive, like "each mouse arrived on a different day", (m / mouse) stilll refers to many mice.  


### FullDefinition (Kind)

- If "w / wug" is a definitional mention, everything that is a "wug" in context is part of "w". 
- Generally default to "multiple" if not sure -- this should be a rare class.
- Can think of this as mentions of 'kind' 
- Ignore whether this is treated collectively or distributively

### Special Cases

###### If it's quantified over multiple times, it's almost assuredly "multiple"
- Everyone (multiple) in the building got a sandwich (multiple)

###### Generic indefinites get "FullDefinition" when referring to a whole set

- A politician (FullDefinition) can't fool all the people (FullDefinition)  all the time.

###### Generic "you"
- Generic "you" (French *on*) gets "multiple"



### Calibrating your instincts:

###### Mr. Vinken is chairman of Elsevier N.V. , the Dutch publishing group .
```

(h / have-org-role-91
      :ARG0 (p / person :wiki -
            :name (m / name :op1 "Mr." :op2 "Vinken"))
      :ARG1 (g / group :wiki "Reed_Elsevier#Elsevier_NV"
            :name (e / name :op1 "Elsevier" :op2 "N.V.")
            :mod (c / country :wiki "Netherlands"
                  :name (n / name :op1 "Netherlands"))
            :ARG0-of (p2 / publish-01))
      :ARG2 (c2 / chairman))
```
**entities**: 
- p / person = Unique

###### There is no asbestos in our products now .
```
(a / asbestos
  :polarity -
  :time (n / now)
  :location (t / thing
              :ARG1-of (p2 / produce-01
                         :ARG0 (w2 / we))))
```
**entities**: 
- t / thing = FullDefinition (the whole class of things we produce)
- w2 / we = Multiple (we treat we/they as a Multiple-type mention)

## Partial Relations

### WHOLE/PART

Two entities exist in a WHOLE/PART relationship if one can be thought
of as part of the other, larger composite entity. These can be simple
or more abstract:

- The **hand**<sub>part</sub> was broken when the boulder fell on
his **arm**<sub>whole</sub>.

Any number of PARTs may be included in a WHOLE/PART relation, although
only one Entity is allowed to fill the WHOLE slot.

- I didn't include enough **flour**<sub>part</sub> in this **cake**<sub>whole</sub>,
and used too much **sugar**<sub>part</sub>.

As with the CONTAINS-SUBEVENT TLINK, this relation can only be used
for cases of compositionality, i.e., narrow readings. In order for
an entity to be Part of another, it must be 100% contained by the
Whole, and compositionally part of it. Thus, the following examples
do not contain any WHOLE/PART relations:

- **Mt. Everest** lies on the border between **China** and
**Nepal**.

- In the **house**, there are several **visitors**.

Note that WHOLE/PART relationships are essentially *hierarchical*,
in that they may theoretically have a whole chain of relationships
(a hair is part of a dog, a dog is part of a pack, etc.) They are also used for spatial relations,
such as:

- We saw the **White house** while in **D.C.**.

The difference between these two previous examples reveals
a difficult boundary case that you will have to ponder – what counts
as compositionally part of a thing.
This is particularly salient when the WHOLE
is a larger spatial entity such as a city, county or country. When
in doubt, remember this compositionality
idea: If the removal of the potential part
would have the potential of changing the nature of the whole,
even a slight bit, then one might consider it compositional and use
WHOLE/PART. If, in contrast, the part is merely temporarily or arbitrarily
located in the space of the other item, do not use WHOLE/PART.

:bangbang: *Note that while IDENT, SET/MEMBER and BRIDGING will also be
used to mark EVENTS, WHOLE/PART is only for ENTITIES. Relationships between EVENTs
that you are tempted to mark as WHOLE/PART should probably be CONTAINS-SUBEVENT
or SET/MEMBER instead.*


### SET-MEMBER

A SET-MEMBER relationship exists when one entity or event can be thought
of as one or several members of a larger group. SET-MEMBER relations
can be between ENTITIES or between EVENTS (more on EVENT SET-MEMBER relations below).

- The **trustees**<sub>SET</sub> have to sign off on the ordinance
before we proceed; however, the trustee **Mr. Gamal**<sub>MEMBER</sub> says
agreement has been hard to come by.

- **Patients**<sub>SET(1)</sub> with **cancer**<sub>SET(2)</sub> are advised
to avoid this medication. Our **patient**<sub>MEMBER(1)</sub> has kidney **cancer**<sub>MEMBER(2)</sub>
and lung **cancer**<sub>MEMBER(2)</sub>, so we will not prescribe it. 

(Notice also that **Our** and **we** are in an IDENTICAL relation.)

- Patient has two **arms**<sub>SET</sub>. Her left **arm**<sub>MEMBER</sub>
is scarred.

You should note that in most examples of SET-MEMBERship, the MEMBER
will be a count noun, but in some cases, the MEMBER can itself be
a group or another set.

- **Terrorists** are among the most dangerous **criminals**,
and **Al Nuri** is perhaps the most dangerous **terrorist** alive.
> **Criminals** SET/MEMBER **Terrorists** 
> **Terrorists** SET/MEMBER **Al Nuri**, **Terrorist**

Any number of MEMBERs may be included in a SET/MEMBER relation, although
only one Entity is allowed to fill the SET slot.


### BRIDGING

BRIDGING is used in the following specific situations where it’s not tenable to use our other coreference links. Examples of both ENTITY and EVENT BRIDGING will be presented here.

**1) Links of asserted identity**, where the assertion is itself questioned
or questionable (in other words, relations that would be IDENT if they weren’t hedged; relations where we simply don’t know if they are in reality identical or not): 

- **John** was arrested last night, as authorities claim **he**
is the **killer** of a local cobbler, found Monday. 

> **John** IDENTICAL **he** 

> **John** BRIDGING **killer**

- **Grigory Kuznetsov**, long thought to be **"Rosebud"**,
a key Cold War CIA asset, died Friday. 

> **Grigory Kuznetsov** BRIDGING **"Rosebud"**

**2) Links that are temporally bound**, that is, where the relation either used to be true, will be true, or is only temporarily true:

- **Ratzinger** was **Pope** until his retirement in 2013.
>  **Ratzinger** BRIDGING **Pope**

- **Greg Bear**, former **Head** of the National Croquet society,
died Wednesday. 
>  **Greg Bear** BRIDGING **Head**

Refer to the section on IDENTICAL above, the fourth case of "X is Y," for more on this.

**3) Links of reframing/restating/equating**:

This can show up in a variety of ways:

a) When a text alleges that doing one event is analogous to doing another, either directly or in an attempt at metaphor:

- John **voted** to make waffles the state food, which amounts to **betraying** all his campaign promises.

>  **voted** BRIDGING **betraying**

b) Between ENTITYs and EVENTs where one is a metaphor for the other, or where one reframes the other:

- By **hiring** Mary, we’ll kill two birds with one **stone**

>  **hiring** BRIDGING **stone**

c) When a text suggests that two EVENTs are being equated:

- Would anyone be kind enough to give him a **lift** southwards? If anyone is willing to **help** out a fellow hipforumer…

>  **lift** BRIDGING **help**


**4) Links between EVENTs about which the author and a source disagree**:

- Mary claims she **ate** all the donuts, but she didn’t **eat** all the donuts.

> **ate** BRIDGING **eat**

Note that **ate** is BEFORE, POS, ACTUAL (it is reported as such by Mary and will be linked via REPORTING to **claims**; see REPORTING section for more on this); **eat** is BEFORE, NEG, ACTUAL.


These are the only situations where BRIDGING may be used.  Potential new contexts for BRIDGING should be brought up for discussion.  Note that this is the only situation where EVENTs and ENTITYs may be linked to each other (see example 3b).  BRIDGING between EVENTs and ENTITYs should take place in the first pass; EVENT-EVENT BRIDGING should take place in the second pass.


