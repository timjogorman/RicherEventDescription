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

###### Coordination

- Every time "and" is part of a coreference chain, it's assumed to have a set/member relation to all of its "opX" children.
- Do not label "and" coordination as a singleton entity unless it is coreferent, or there are strong reasons to consider it a collective unit. 
   - Test: If this document was famous/important, would the referent of this "and" get a wikipedia entry?
   - Test: If you were discussing the document, is this particular combination of entities easy to refer to?

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


