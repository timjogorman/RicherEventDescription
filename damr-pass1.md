# RED+AMR Entity Coreference Pass Guidelines

- We are labeling each entity we find as a Discourse Entity.
- Usually these are mentioned many times in a document, and each coreferent mention is put into the same DiscourseEntity chain. 
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
      - Check the "wiki relation(if present)" box to override the assumption that they are coreferent with the :wiki link. 
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


##### Differentiating Entities from Events

There are two core rules here:
- If in doubt about the EVENT/ENTITY distinction, default to EVENT (i.e. don't mark it as anything in this pass).  
   - Most things that get a predicate in AMR are either events or not referential at all. 
- If something represents both an ENTITY and an EVENT, you can annotate both -- as an ENTITY in this pass and then as an EVENT later. 
   - This is NOT for things that are ambiguous, but for situations where an object is presented in the real world that also implies its associated event.
       - The nearby pipe **[<sub>event & entity</sub> bomb]** disrupted the festival.
       - I kept Mary's **[<sub>event & entity</sub> text]**.
   - Examples of these "complex types":
     - Texts, messages etc. are not entities (only events) unless there is discussion of their recorded or stored form.
     - Reports, summaries, etc.; if and only if one is talking about the physical or electronic form (I can't find the report)
     - Laws, acts, rules etc.: Only when talking about a particular law or act, rather than a general prohibition.
     - Weapons and their impact: Only when talking about the weapon/disease/virus rather than its deployment/consequences: I found [the virus] on my computer

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

- Also does not refer to grammatical plural (although most plurals will be this). 
- Is anything *quantifiable*, regardless of whether it's discretely countable ('there are 12 wugs') or a mass ('there are four pounds of wug', 'i have a jug of wugs',etc.). 
- Ignore whether this is treated collectively or distributively

### Kind

- If "w / wug" is a definitional mention, everything that is a "wug" in context is part of "w". 
- Generally default to "multiplicity" if not sure.
- Can think of this as mentions of 'kind' 
- Ignore whether this is treated collectively or distributively

### Special Cases

###### If it's quantified over multiple times, it's almost assuredly "multiple"
- Everyone (multiple) in the building got a sandwich (multiple)

###### Generic indefinites get "kind" when referring to a whole set

- A politician (kind) can't fool all the people (kind)  all the time.

###### Generic "you" gets "kind"
- Generic "you" (French *on*) gets "Kind" as well



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
- t / thing = Kind (the whole class of things we produce)
- w2 / we = Multiple (we treat we/they as a Multiple-type mention)


