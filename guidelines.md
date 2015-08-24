<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Richer Event Description (RED) Annotation Guidelines (v.1.6)](#richer-event-description-red-annotation-guidelines-v16)
  - [Introduction](#introduction)
    - [The Pipeline and General Intuitions of Annotation](#the-pipeline-and-general-intuitions-of-annotation)
    - [Acknowledgements](#acknowledgements)
- [Markables and Entity Relations Stage](#markables-and-entity-relations-stage)
  - [Event/Entity Mentions](#evententity-mentions)
    - [Finding Entities and Events](#finding-entities-and-events)
        - [What is an EVENT?](#what-is-an-event)
        - [What is an ENTITY?](#what-is-an-entity)
        - [Differentiating ENTITY and EVENT](#differentiating-entity-and-event)
      - [When many words relate to one event](#when-many-words-relate-to-one-event)
      - [Words implying many events](#words-implying-many-events)
  - [Spans of Annotation](#spans-of-annotation)
      - [Minimum Span Annotation](#minimum-span-annotation)
    - [Annotating Features on Entities and Events](#annotating-features-on-entities-and-events)
    - [Entity Features - Polarity and Modality](#entity-features---polarity-and-modality)
    - [Event Polarity and Modality](#event-polarity-and-modality)
    - [Marking the relationship to document time (DocTimeRel)](#marking-the-relationship-to-document-time-doctimerel)
        - [DocTimeRel in relation to speech](#doctimerel-in-relation-to-speech)
      - [Event Type, Aspect and Implicitness](#event-type-aspect-and-implicitness)
      - [Annotating contextual aspect of EVENTs](#annotating-contextual-aspect-of-events)
          - [N/A](#na)
          - [INT - Intermittent](#int---intermittent)
      - [Type of EVENTs](#type-of-events)
          - [N/A](#na-1)
          - [ASP - Aspectual](#asp---aspectual)
          - [EVI - Evidential](#evi---evidential)
      - [Annotating representation of EVENTs](#annotating-representation-of-events)
          - [Default -- Explicit](#default----explicit)
          - [Implicit](#implicit)
      - [Annotating degree of EVENTs](#annotating-degree-of-events)
      - [N/A, MST - Most and LTL - Little](#na-mst---most-and-ltl---little)
      - [Marking Difficult annotations](#marking-difficult-annotations)
  - [Temporal Expressions](#temporal-expressions)
    - [Identifying and Annotating TIMEX3s](#identifying-and-annotating-timex3s)
    - [Annotating TIMEX3 class](#annotating-timex3-class)
      - [DATE](#date)
      - [TIME](#time)
      - [DURATION](#duration)
      - [QUANTIFIER](#quantifier)
      - [PREPOSTEXP](#prepostexp)
      - [SET](#set)
    - [TIMEX3s vs. Temporal Manner Adverbs](#timex3s-vs-temporal-manner-adverbs)
    - [DOCTIME and SECTIONTIME Annotation](#doctime-and-sectiontime-annotation)
  - [DUPLICATE marking for repeated spans of text](#duplicate-marking-for-repeated-spans-of-text)
      - [Guidelines for finding DUPLICATE text](#guidelines-for-finding-duplicate-text)
  - [Entity Coreference Relations](#entity-coreference-relations)
    - [IDENTITY and APPOSITION of ENTITIES](#identity-and-apposition-of-entities)
      - [IDENTICAL](#identical)
      - [APPOSITIVE](#appositive)
    - [WHOLE/PART](#wholepart)
    - [SET-MEMBER](#set-member)
    - [BRIDGING](#bridging)
    - [General Guidelines for Annotating Coreference](#general-guidelines-for-annotating-coreference)
      - [Never link EVENTs to ENTITIES (except with BRIDGING)](#never-link-events-to-entities-except-with-bridging)
      - [WHOLE/PART, SET/MEMBER, and BRIDGING relations are inherited by IDENT](#wholepart-setmember-and-bridging-relations-are-inherited-by-ident)
      - [Bridging relations are re-created for subsequent mentions](#bridging-relations-are-re-created-for-subsequent-mentions)
      - [Use SET/MEMBER to define groups of people](#use-setmember-to-define-groups-of-people)
      - [Don't link ACTUAL and GENERIC items](#dont-link-actual-and-generic-items)
      - [Identifiers are people too](#identifiers-are-people-too)
      - [Avoid annotating coreference links based solely on your personal](#avoid-annotating-coreference-links-based-solely-on-your-personal)
      - [Identity Annotation for very broadly GENERIC entities](#identity-annotation-for-very-broadly-generic-entities)
      - [IDENT over generic you, one, etc.](#ident-over-generic-you-one-etc)
- [Event Relations Pass: Linking Events Together](#event-relations-pass-linking-events-together)
  - [Narrative Containment](#narrative-containment)
    - [Temporal Containers vs Subevent Containers](#temporal-containers-vs-subevent-containers)
    - [Choosing the Anchors of Narrative Containers](#choosing-the-anchors-of-narrative-containers)
  - [When to add Temporal Links other than CONTAINS](#when-to-add-temporal-links-other-than-contains)
    - [TLINK all EVENTs to their narrative container, if possible.](#tlink-all-events-to-their-narrative-container-if-possible)
    - [Inferrable but unmarked Temporal Ordering is not labeled](#inferrable-but-unmarked-temporal-ordering-is-not-labeled)
  - [Temporal Relation Annotation](#temporal-relation-annotation)
    - [TLINK only when it captures more information than just marking DocTimeRel.](#tlink-only-when-it-captures-more-information-than-just-marking-doctimerel)
    - [TLINK all explicitly stated temporal relations.](#tlink-all-explicitly-stated-temporal-relations)
    - [Do not need to TLINK TIMEX3s to one another.](#do-not-need-to-tlink-timex3s-to-one-another)
    - [ACTUAL or UNCertain EVENTs should never be linked to HYPOTHETICAL](#actual-or-uncertain-events-should-never-be-linked-to-hypothetical)
    - [Try to only link EVENTs and TIMEX3s within the same sentence.](#try-to-only-link-events-and-timex3s-within-the-same-sentence)
    - [Avoid "Millisecond Reasoning"](#avoid-millisecond-reasoning)
  - [Discerning TLINK sub-types](#discerning-tlink-sub-types)
    - [BEFORE](#before)
    - [CONTAINS](#contains)
    - [CONTAINS-SUBEVENT](#contains-subevent)
    - [OVERLAP](#overlap)
    - [BEFORE/CAUSES, OVERLAP/CAUSES, BEFORE/PRECONDITIONS and OVERLAP/PRECONDITIONS](#beforecauses-overlapcauses-beforepreconditions-and-overlappreconditions)
    - [BEGINS-ON](#begins-on)
    - [ENDS-ON](#ends-on)
    - [SIMULTANEOUS](#simultaneous)
    - [Expressing TLINK Types in Point Algebra](#expressing-tlink-types-in-point-algebra)
    - [Annotating TLINK Features](#annotating-tlink-features)
    - [Annotating polarity of TLINKs](#annotating-polarity-of-tlinks)
    - [Annotating contextual modality of TLINKs](#annotating-contextual-modality-of-tlinks)
  - [Causation and Precondition Annotation](#causation-and-precondition-annotation)
    - [Distinguishing "Cause" from "Precondition"](#distinguishing-cause-from-precondition)
      - [Causality Annotation Rules and Regulations](#causality-annotation-rules-and-regulations)
      - [Causality is specific to the instance, not to the concept](#causality-is-specific-to-the-instance-not-to-the-concept)
      - [Focus on relations suggested in the text](#focus-on-relations-suggested-in-the-text)
      - [Look for causal language to guide causal annotations](#look-for-causal-language-to-guide-causal-annotations)
      - [Causal annotations can only link EVENTs to one another](#causal-annotations-can-only-link-events-to-one-another)
      - [Objects described as causes, effects, or preconditions must be METONYMIC](#objects-described-as-causes-effects-or-preconditions-must-be-metonymic)
      - [Do not create causal links between verbs and their arguments](#do-not-create-causal-links-between-verbs-and-their-arguments)
      - [EVIDENTIAL EVENTs should not be causally linked to those things which](#evidential-events-should-not-be-causally-linked-to-those-things-which)
      - [Assume the writer of the text is reliable](#assume-the-writer-of-the-text-is-reliable)
      - [Each EVENT can participate in multiple CAUSES or PRECONDITIONS links](#each-event-can-participate-in-multiple-causes-or-preconditions-links)
      - [Causal links can cross sentence boundaries](#causal-links-can-cross-sentence-boundaries)
      - [Causal links should be chained where possible](#causal-links-should-be-chained-where-possible)
      - [ALINK annotations should not be interpreted causally](#alink-annotations-should-not-be-interpreted-causally)
      - [When in doubt, leave it out!](#when-in-doubt-leave-it-out)
      - [Causation and Precondition TLINK Use](#causation-and-precondition-tlink-use)
      - [BEFORE/PRECONDITIONS](#beforepreconditions)
      - [BEFORE/CAUSES](#beforecauses)
      - [OVERLAP/CAUSES](#overlapcauses)
      - [Causal TLINK Properties](#causal-tlink-properties)
  - [Event Coreference](#event-coreference)
    - [IDENTITY](#identity)
    - [SET-MEMBER](#set-member-1)
    - [BRIDGING](#bridging-1)
    - [General Guidelines for Annotating Coreference](#general-guidelines-for-annotating-coreference-1)
      - [Never link EVENTs to ENTITIES](#never-link-events-to-entities)
      - [SET/MEMBER, and BRIDGING relations are inherited by IDENT](#setmember-and-bridging-relations-are-inherited-by-ident)
      - [Bridging relations are re-created for subsequent mentions](#bridging-relations-are-re-created-for-subsequent-mentions-1)
      - [Don't link ACTUAL and GENERIC events (use SET/MEMBER or BRIDGING)](#dont-link-actual-and-generic-events-use-setmember-or-bridging)
  - [Aspectual Link Annotation](#aspectual-link-annotation)
    - [ALINK sub-types](#alink-sub-types)
  - [REP - Reporting Annotation](#rep---reporting-annotation)
- [Appendix](#appendix)
  - [Edge Case Guides](#edge-case-guides)
    - [Hard Cases in EVENT vs ENTITY distinctions](#hard-cases-in-event-vs-entity-distinctions)
    - [Hard Cases when determining Markablability](#hard-cases-when-determining-markablability)
    - [Complex Predicates](#complex-predicates)
    - [Distinguishing Reporting events from Hedges](#distinguishing-reporting-events-from-hedges)
  - [Allowable explicit grammatical evidence](#allowable-explicit-grammatical-evidence)
    - [Permissable Evidence for BEFORE/OVERLAP](#permissable-evidence-for-beforeoverlap)
    - [Rules for Reporting verbs implying uncertain/hedged](#rules-for-reporting-verbs-implying-uncertainhedged)
    - [Permissable Evidence for Uncertain/Hedged](#permissable-evidence-for-uncertainhedged)
- [Document Revision History](#document-revision-history)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


# Richer Event Description (RED) Annotation Guidelines (v.1.7)

*Developed by Will Styler, Kevin Crooks, Mariah Hamang, and Tim O'Gorman
as a synthesis of the THYME-TimeML guidelines, the Stanford Event
coreference guidelines and the CMU Event coreference guidelines. These
guidelines have been developed with substantial input from Eduard
Hovy and Teruko Mitamura at Carnegie Mellon University, Rei Ikuta
at the University of Colorado, Boulder, and benefited from the discussion
at the NAACL Events Workshop.*

## Introduction

Richer Event Description is an attempt to bring together a number
of existing and well-researched veins of document annotation into
a single representation of the events and participants in a discourse.
It is not concerned with semantic role annotation in the traditional
sense -- the relationships between events and the entities participating
in them -- but rather the hierarchical structure of events, of time,
and of participants, and the tracking of those events and participants
over a document. 

On a more concrete level, the task of Richer Event Description annotation
is to mark which units in the text should be considered to be entities,
events or times in a document, to label those units with features
such as modality, and to mark temporal, causal, event-substructural
and coreference relations between them. 

The result of this annotation can be thought of as a timeline of events
within a document -- with labels for when each event occurred and
which are contained within another -- and a playbill of participants,
so that every mention of an ongoing character, location etc. might
be linked together into a continuous sense of an entity. The desired
result, in this sense, is something which would result in a rich understanding
of a document if combined with within-sentence understanding semantic
roles, and is therefore focused upon the capture of relations not
traditionally captured in semantic-role labelling tasks. 


### The Pipeline and General Intuitions of Annotation

This is an elaborate task, and each document will have many entities,
many events, and many relations between them. It is moreover an **adjudicated
task.** This means that each document will be annotated by two people,
and disagreements between those two annotators are resolved.

This leads to the two-stage pipeline used for RED
annotation. The first stage in this pipeline will involve the annotation
of events, entities, and the coreference and partial-coreference relationships
between entities. Those annotations are then adjudicated by a third
annotator, who makes a judgement call on all disagreements. The second
stage of annotation marks the relationships between events-- both
to show when those events are identical, and to mark relationships
between related events -- over those adjudicated events.

The structure of such a pipeline is to help improve the consisistency
of the annotation process. It is important for annotators to think
of such a question of consistency not simply in terms of avoiding
absolute errors, but in terms of whether our annotations themselves
are clear and predictable. Because document-level annotation involved
a great deal of rich understanding of the context, and your understanding
will often vary in subtle ways from your fellow annotators, we cannot
simply annotate every relationship that you observe in the text in
a haphazard fashion. The pervasive theme to attend to in reading these
guidelines, therefore, is that we are attempting to capture the rich
"meaning" of the document while doing so consistently,
and that a wide variety of rules and strictures defined below are
designed simply for that purpose.


### Acknowledgements

The project is based on work supported by Award R01LM010090 from the
National Library Of Medicine, and by DARPA FA-8750-13-2-0045, subaward
560215 (via LDC) DEFT: Deep Exploration and Filtering of Text.
The content is solely the responsibility of the authors and does not
necessarily represent the official views of the National Library Of
Medicine, the National Institutes of Health, or the Defense Advanced
Research Projects Agency.

# Markables and Entity Relations Stage

There are two different kinds of actions done during the first stage
of annotation. One is the annotation of events, entities and times, where you will be 
differentiating what is worth keeping track of, and marking those events, entities and times
with characteristic attributes. The other annotation being done is relationships between entities
-- coreference, part/whole relations, set/member relations and bridging
relations between entities.

These exist in the same stage precisely so that the anotation
of both may be done at the same time. When initally learning to annotate,
however, one is encouraged to start by annotating entities and events
first, and then adding entity coreference links. As one gains competence
at the task, you are encouraged to attempt to combine these tasks as much as possible.


## Event/Entity Mentions

### Finding Entities and Events

The first and most fundamental task in the first stage of annotation
is to label EVENT and ENTITY instances. When first annotating, one should 
thing of each such labelling act as *two* decisions: the first part being the decision
about **whether** something should be annotated, and the second part being
the decision about **what exact span of words** you should mark to designate
it. 

##### What is an EVENT?

We define an event as any occurrence, actions, processes or event
states which deserve a place upon a timeline, and could have any syntactic realization -- as verbs, nominalizations,
nouns, or even adjectives. It is important that one make the event/non-event
determination independently of syntax: we will consider syntactic
considerations for what the span of annotation will be, but not
for whether or not to consider something to be an event at all. Instead,
at this stage you should focus on the semantic questions of what is
actually happening, asking whether the words you are considering constitute
a sequences of changes, transitions or states occurring in the world
(or some possible world). 

This may be contrasted with verbs and nouns that amount of a purely
grammatical encoding of relationships between elements. For verbs,
many of the non-eventive cases will therefore be grammaticalized verbs
such as **go**, **seem**, **have**, etc. -- for example, there
is only one verb in example below:

- Your dog *seems to have eaten* the cupcakes.

In a more general sense, one can think of that criterion as being
about distinguishing whether a particular mention (like "have"
or "seems" above) constitutes its own event, or merely helps constitute
description of a single event. For example, a light verb like "take
a bath" does not constitute a separate "take" event and "bath"
event, but rather combine to jointly signal the bath-taking event. 

A second definitional question emerges with states and properties.
Consider the range of circumstances below ,ranging from very eventive to not eventive at all:

- The walls *yellowed* during the fire.  (most eventive)
- We came home to find the door *opened*.
- We came home to find the door *open*.
- I own a *yellow* canary   (very non-eventive)

Hopefully the reader will agree that the last example is dramatically
less "eventive" than the other instances. Yet naturally, all states
**exist** on a timeline, so mere existence on a timeline is not
suffient for this. However, the first two examples above do more than potentially having starts and ends; the 
mention itself implies, to many readers, an event initiating the start of the attribute.

Adjectives used as mere specifiers, to label or refer to particular
people, should therefore be viewed with skepticism in this regard. "I came home and saw
the door was open" evokes an act of someon opening it; "He walked through
the open door" does not. In short:

> An Attribute in an EVENT when its use implies actual occcurrences -- such as the events leading up to its own existence. 

The second kind of attribute that needs to be annotated as an EVENT are attributes that don't, themselves, pass this test, but which are clearly coreferential with those that do, or which could have SET/MEMBER relationships with those that do.

##### What is an ENTITY?

For ENTITY annotation, we will be going through the text, finding
all instances of things that consistute an ENTITY -- a participant,
location, organization, or other entity that might be tracked in the
discourse. 

Just like when finding events, you must first decide if there is one
entity being mentioned or many. This can be a nuanced decision; consider our various "hospital" descriptions for edge cases:

- **[<sub>Entity</sub> Boulder County Hospital]** said that most **[<sub>Entity</sub>those ]** seriously wounded now were treated at an emergency
**[<sub>Entity</sub> unit]** at the **[<sub>Entity</sub> hospital]**.
- The county **[<sub>Entity</sub> hospital]** said that most **[<sub>Entity</sub>those ]** seriously wounded now were treated at an emergency
**[<sub>Entity</sub> unit]** at the **[<sub>Entity</sub> hospital]**.

This gets at the first two very important distinctions we are making, namedly:

> If a proper name contains words that might also refer to other objects in  the discourse, do not "nest" such mentions; Proper names can be treated as inseparable units. 

The second rule is:

> If an entity reference contains a word that is merely clarifying the mention, but not an entity itself, then do not mark it, such as "county" in the mention above.  The exception to this is if that word is coreferential to a "real" mention of the same thing -- if "the county" was mentioned and clearly referential later in the document, then come back and tag this.

There is a special case of this, however, for instances like "Manokwari Hospital" below:

- The nearest **[<sub>Entity</sub> Manokwari]** **[<sub>Entity</sub> Hospital ]** said that most of **[<sub>Entity</sub>those ]** seriously wounded now were treated at an emergency **[<sub>Entity</sub> unit]** at the **[<sub>Entity</sub> hospital]**.

This is a separate term, because:
> If a term is not part of a name, but it is a named reference to a real, unique, named entity in the world, then make it a separate entity. 

Do this even when the term is technically an adjectival pertainym, such as:

- The **[<sub>Entity</sub> Indian]** prime **[<sub>Entity</sub> minister]**

Don't go overboard, however: when the actual named entity is not being evoked itself, but merely some stereotype, origin or style of that entity, then ignore it:

- **[<sub>Entity</sub> I ]** like american **[<sub>Entity</sub> music ]**
- **[<sub>Entity</sub> I ]** like indian **[<sub>Entity</sub>food ]**

A good example to remember for this is that we don't want to be keeping track of the idea of "hot dog" in every mention of "hot dog stand", but that if we had a document that was somehow about "hot dogs" (say, reporting a recall of bad hot dogs), then we *do* want to keep track of it.  

A more technical definition is that for "clearly referential" things, we are doing what is called *singleton annotation*, marking a referent even if it occurs only once in the document.  For less referential entities, we are abandoning singleton annotation and *only* mark an entity if it is coreferential with more important mentions.  "Less referential", in this case, means mentions that serve to clarify what you are referring to or doing (and therefore might not be being referred to themselves). 

:bangbang: *Remember that if something is subsumed by an event, make it an event!  Specifically, if a verb-object pair collectively constitute an event, such as a light verb or multi-word expression  -- "tell the truth", "take a bath", etc. -- then do not make the object an entity!*


##### Differentiating ENTITY and EVENT

Sometimes a mention will seem like both an ENTITY and an EVENT, often being technically a "thing" that also implies the process involving that thing:

- The **revolution** has spread to Misrata
- That **text** was really funny
- I recommended **Tylenol** three times a day.

The **revolution** might be considered either a group of people or a process of revolting; the **Tylenol** might stand for the physical pills or the act of taking them. If one talked about a disease like "carcinoma" it might be viewed both as objects and processes.  These are all subject to one core rule:

> If in doubt about the EVENT/ENTITY distinction, default to EVENT.  

We will, however, get more specific than this.  Many of these, like the mentions above, look like entities.  You can often have different answers for "when was this created" and "when does this start?", as the event they imply are usually different from the act of doing them.  In those cases, you will mark them as an EVENT, but show that they are implicit from an object, marking them with an IMPLICIT feature:

- He was **[<sub>event</sub> sentenced]** to *[<sub>duration</sub> five years]* of **[<sub>implicit-event</sub> prison]**

Prototypically these should be events that are implied by the event -- something that happens in that location (as in the captivity state implied by "prison"), that is the traditional thing done with that entity (such as the "pill comsumption" implied by "Advil"), and so forth (see CITATION for what we are getting at here).  For some of these -- often marked in the specific phenomena guide -- you shoud also annotate them as an ENTITY, such as laws, rules, and very referential places that imply an event (such as "prison"), and mark coreference for both the event and the entity:

- The nearby pipe **[<sub>implicit-event & entity</sub> bomb]** disrupted the festival. The **[<sub>implicit-event</sub> explosion]** from the **[<sub>entity</sub> device]** was heard for miles. 

-  **bomb<sub>event</sub>** IDENTICAL **explosion**
-  **bomb<sub>entity</sub>** IDENTICAL **device**

For others -- such as statements, messages, texts or medications -- the text is almost always referring to the event itself, and one should **only** annotate them as IMPLICIT EVENTS.  Examples of this are:

- "Make sure to eat something before your **[<sub>event</sub> vitamins]**."
- "**[<sub>event</sub> Loperamide]** helped to calm her stomach."




Be exceedingly sparing with such implicit-event annotations. For our purposes,
only use it when you are sure that a later relations phase will really
need to make reference to an entity's implied events. Otherwise, simply
annotate that entity as an ENTITY.


#### When many words relate to one event 

As mentioned in the prior section, if many words contribute to a single event or entity, we want them to all be represented by a single markable. Some of these will be relatively clear-cut, as with *light verbs*:

> John ~~took~~ a **[<sub>event</sub> bath]**.
> The burglar ~~committed~~ a heinous **[<sub>event</sub> crime ]**. 

These are most clear-cut with light verbs meeting the rule from Bonial (2014) that "the light verb plus its true predicate can often be paraphrased by a verbal form of the true predicate without loss of the core meaning of the expression. ".  In other words, "to give a lecture" is almost identical to "to lecture", "to give a look" is almost the same as "to look", etc.  For related reasons, we will also be not marking **support verb** constructions such as 

> The **earthquake** ~~occurred~~ during the **parade**.

In real annotations, there may be more nuanced instances than this, in which it's unclear whether one is dealing with two events or one. We will list some more specific constraints below, and you are encouraged to check the examples in the [complex predicates examples in the appendix](#complex-predicates). 

**General Rules for Complex Predicates**

- If you encounter an idiom, simply mark the head verb in the idiom, and assume that the meaning of the phrase is carried by that verb. So "The chickens have **[come]** home to roost for Bush." simply has a [come], which stands for your interpretation of the coming-home-to-roost event.
- Markers of epistemic status, like "seems to" or "appears to", are not events. When in doubt, you should follow the nearest case in the [Reporting vs Hedging distinctions](#Distinguishing Reporting events from Hedges) in the appendix.


####  Words implying many events

Sometimes a single word ends up implying many events, like the two colonoscopies implied in the following sentence (the hypothetical one and the one that occurred in the 1970s): 

- Her main concern is that she does not wish to have a **colonoscopy**, which she had back in the 1970s.

This also occurs with gapping phenomena, as in **raids**

- The **raids** in Phoenix **began** at 4am, in Denver, at 5.

We unfortunately will be annotating only one EVENT span per actual span in the context (it would be simply too complicated otherwise).  In these cases, pick the first event being implied and assume that the word refers to that first event. 



## Spans of Annotation

Once you have decided that a given phrase or word *qualifies* as an
EVENT or ENTITY, you'll need to decide what `span' (section of the
text) to annotate.

For each ENTITY and EVENT annotation, you might have found a long
phrase (or even, for EVENTs, a complex string of verbs and nouns)
which designates that concept. We will not be annotating that
entire string, but instead will designate a single
word, the syntactic "head" of the phrase, which will represent that whole idea.

Deciding whether or not a term should be one, many or no entities or events is entirely
a semantic decision described above; the details here are merely a decision about the span which
you should mark after that. A single noun phrase can have many ENTITYs
or EVENTs (every word in "United States Olympics Organization Chairwoman"
is an ENTITY), and the fact that a word is not the head of a larger
syntactic unit *in no way* disqualifies it from separate annotation.


#### Minimum Span Annotation

One might talk about "maximum span" annotation as being everything
encompassing what you are talking about (an approach we are *not*
 using here):

- **[<sub>max-span</sub> The 7.6-magnitude earthquake** ] had the consequences of **[<sub>max-span</sub> severe damage ]** to **[<sub>max-span</sub> multiple buildings ]** *last July*

We will take the opposite approach, using a "minimum span" style of annotation in which we only mark the syntactic head of each markable. This is because capturing everything about what makes an entity an entity, or an event an event, is not only difficult, but can lead to elaborate overlapping annotations. Instead of
the kinds of annotations you see above, we will annotate everything (except proper nouns and times) using a single word,
resulting in spans such as: 

- The 7.6-magnitude **[<sub>event</sub> earthquake** caused severe **[<sub>event</sub> damage** to multiple **[<sub>entity</sub> buildings** *last July*.

- The **[<sub>entity</sub> U.S.]** **[<sub>entity</sub> President ]** **[<sub>event</sub> maintained ]** his **[<sub>event</sub> stance ]** on the civil **[<sub>event</sub> war ]**.

This does not mean we are throwing this information away, but rather
that we assume this information to be recoverable. This emphasis upon
recoverability is important; we need to capture the word that lets
us "find" the rest of the phrase in question, or in other words,
the **syntactic head**. Consider a syntactic dependency tree of the above sentence in this
regard 

![DP](dependencygraph.png)

One might imagine that grabbing "stance" subsumes the whole bundle of dependents, "the stance on the civil war".  Grabbing "stance" in that sense essentially can be thought of as also grabbing its dependents. 

If you find syntax trees complex and scary, don't worry: all you need to do is follow some basic rules for what
we call "head finding", which generally just means that there is a word in each
phrase which is subsistutable for the whole phrase.  One casual way to test this is to ask what lexical term would be used in
a repeated version of the same phrase. If you constantly talk about "John's
insatiable hunger for more donuts", one might refer to that hunger
as "his hunger", but not by "his donuts".

For verb phrases and adjective phrases this will be simple, and there
is no need to think of things in terms of **syntactic heads**
at all. You will only be annotating the verb or adjective in the phrase,
and nothing more. Thus, look at the events in the following examples
(no other parts have been annotated):

- The stock price is **stable**.
- Patient **reports** **throwing** up.
- She's **unable** to **lift** her arms.
- Since her last **surgery**, she has seemed **disoriented** and
**moody**.
- She feels slightly **weak** but has **resumed** most of her normal
**activities**.
- The jury **finding** was in favor of the defendant.

Note that we take the single verb or adjective even when when dealing
with a multiword predication such as "throw up". The
exception to this tendency comes from "light verbs" and "support
verbs" mentioned above, where the verb itself is ignored:

- John ~~took~~ a **<sub>event</sub>bath**.
- The patient ~~underwent~~ **<sub>event</sub>surgery**.
- The burglar ~~committed~~ a heinous **<sub>event</sub>crime**. 

The same rules for minimal-span annotation will also apply to nouns.
Hopefully you will have some exposure to what the head of a noun phrases
is from syntactic courses, and this will be quite familiar. Start
by examining the example for participants which you desire to annotate;
say that you found the following:

- The most recent IED attack outside the Green Zone in Baghdad
- The shooting near the word-torn city
- That recision biopsy analysis of the sigmoid colon today

For each, rule out prepositional phrases and post-postitional adverbs:

- The most recent IED attack ~~outside the Green Zone in Baghdad~~
- The shooting ~~near the war-torn city~~
- That recision biopsy analysis ~~of the sigmoid colon today~~

Then for each sequence of nouns, the head is the rightmost noun:

- The most recent IED **attack** ~~outside the Green Zone in Baghdad~~
- The **shooting** ~~near the war-torn city~~
- That recision biopsy **analysis** ~~of the sigmoid colon today~~

This doesn't mean that other entities and events won't be within the
spans you considered. The same examples should result in annotations such as:

- The **[<sub>event</sub>shooting]** near the war-torn **[<sub>entity</sub> city]** 
- That recision biopsy **[<sub>event</sub> analysis]** of the sigmoid **[<sub>entity</sub> colon]** *today*

There will be two exceptions to this "minimal span" rule; proper
names and times. Proper names should be annotated with all name parts,
so that "Bill Clinton" is not "Bill **Clinton**" but rather
"**Bill Clinton**". Do not include determine determiners in
such terms:

- The most recent IED **attack** outside the **Green Zone** in **Baghdad**.

With such proper names, if the last term in a phrase is a generic term referring to the same thing, default to putting it into the proper name itself, even if not capitalized:

- I got a copy of **[<sub>entity</sub> Harper's magazine ]**.

Such a list of rules gives us the following heads (only showing the
nominals):

- **She** had experienced no **dizziness** until the **start**
of **chemotherapy**.

- The **Zetas'** latest **attack** resulted in the **killing**
of three Mexican **officials**.

- The **CT** showed a small rectal **abcess**.

- The long-awaited but ultimately brief **battle** outside the
**city** quelled the rebel **uprising**.

- The **patient** reports **nausea** and **vomiting**.

- **She** does note **darkness** of the **stools**.

- The **fire** quickly spread throughout the **valley**, resulting
in the **destruction** of 15 **homes**.

- Her **yelling** shocked **everybody** at the **conference**.

- **We** also discussed **some** of the **toxicities** of
fluoropyrimidine-based **chemotherapy**.


- **Levaquin** 750 mg p.o. q. day (will restart today)


Sometimes this head-finding will be difficult. For example, in clinical
texts, one might find fragmentary phrases in which prepositions have
been elided, as in "patient had CT chest pelvis". In such cases,
do feel free to attempt various paraphrases of what the phrase means,
and to pick the word that would be the head of those more full forms. 

- **[<sub>event</sub> CT ]** **[<sub>entity</sub>chest ]** **[<sub>entity</sub>pelvis ]**

### Annotating Features on Entities and Events

When you mark each entity or event, you will need to label basic features
on the events and entities. 


### Entity Features - Polarity and Modality

The majority of ENTITYs will be of the polarity POS for "positive",
meaning that they are actual entities. This is the default value.
You will occasionally find purpose to mark an ENTITY of a NEG polarity,
indicating that the ENTITY does not exist.

- **Mr. Black**<sub>POS</sub> spoke with **us**<sub>POS</sub> about
the new **facility**<sub>POS</sub>. 

- **Cincinnati**<sub>POS</sub> doesn't have an **airport**<sub>NEG</sub>.

- **John**<sub>POS</sub> couldn't attend the **concert**<sub>POS</sub>
for lack of **money**<sub>NEG</sub>.

A related feature is Contextual Modality, which identifies whether
the entity is a specific real entity, a class of entities, etc. The
majority of ENTITYs will be ACTUAL (they refer to real, specific entities), but one may define ENTITY as being GENERIC,
HYPOTHETICAL, or UNCERTAIN/HEDGED as well. 

The most obvious kind of GENERIC entity will be references to "kinds".
Such generics in English are often bare plurals, but can be indefinites
or definites too:

- **Terrorists**<sub>GEN</sub> in the **region**<sub>ACTUAL</sub> often attack
office **buildings**<sub>ACTUAL</sub>.
- The **lion**<sub>GEN</sub> is the proudest of **animals**<sub>GEN</sub>
- We do not normally recommend surgery to **patients**<sub>GEN</sub> with
a cardiac status similar to **Ms. James**<sub>ACTUAL</sub>.

One easy way to distinguish GENERIC ENTITYs from ACTUAL ENTITYs is
by "omniscient substitution". Consider "Union Leaders" in the examples
below:

- Teddy Roosevelt met with Union Leaders before writing the bill.
- Union leaders often push for tax breaks.

In the first, an omniscient person could put together a list of the
specific persons he met with and replace it with that list:

- Teddy Roosevelt met with *Samuel Gompers, John Lewis, Walter
Reuther, A. Philip Randolph, and Jimmy Hoffa* before writi																														ng the bill.

In the second, however, no such list could be made; it refers to the whole class of union leaders, and would thus be GENERIC.

Similarly, an omniscient annotator could know specific referents for
the below ACTUAL ENTITYs:

- Three unidentified **criminals**<sub>ACTUAL</sub> broke into my shed.
- Tomorrow's **participants**<sub>ACTUAL</sub> will be thrilled.
- **Vandals**<sub>ACTUAL</sub> have defaced a prominent prehistoric pictogram.

But no referents (outside of every member, past present and future,
of a generic class) could possibly be found for the below GENERIC
ENTITYs:

- **Criminals**<sub>GEN</sub> often plead "Not Guilty", even if they've
committed the crime.
- **Participants**<sub>GEN</sub> in Triathlons generally experience significant
chafing.
- **Vandals**<sub>GEN</sub> should be punished severely if caught.

The complexity of that annotation will occur with entities which are
sets, but where the set has been defined provisionally in context:

- Young Denver **voters**<sub>GEN</sub> only turn out in high numbers during presidential elections.
- My senior **class**<sub>ACTUAL</sub> performed quite well on the **SAT**<sub>GEN</sub>

For these, test whether you can paraphrase them using "the kind X that Ys" without changing the meaning. For example:

- same meaning: **The kind of young people in Denver that vote**<sub>GEN</sub> only turn out in high numbers during presidential elections.
- changes meaning: **The kind of people that are in my senior class**<sub>ACTUAL</sub> performed quite well on **the SAT**<sub>ACTUAL</sub>

A third kind of option for ENTITY modality is that of HYPOTHETICAL
entities. Hypothetical entities are not just entities participating
in a hypothetical situation -- all sorts of entities can be involved
in hypothetical worls -- but rather an entity that would not exist
outside of that hypothetical possible world. 

- If he did have a Mustang<sub>hypothetical</sub>, he would wreck it.

As will come up later for GENERIC vs HYPOTHETICAL events, note also
that generalizations with "if" are still GENERIC. You should test
this by whether you can paraphrase it with a true generalization instead:

- I'm not saying that
if a **couple**<sub>GEN</sub> both work stacking shelves, they should
be getting married in a supermarket<sub>GEN</sub>
> BECAUSE: this is paraphrasable with *I'm not saying that couples that work stacking shelves should get married in supermarkets*

The above example is not depicting "couples stacking shelves" as an entity which would functionally exist if certain conditions were met, but merely specifying a set of entities in the world.  Similarly you also may use UNCERTAIN/HEDGED for entities, but it follows the same constraint; it is only to be used when the actual existence of the entity is uncertain and being actively cast into doubt by the local context.

### Event Polarity and Modality

In order to express the polarity of an EVENT, the "polarity" attribute
of an event is specified. Polarity in this schema is relatively straightforward,
and there are only two possible types: POS and NEG.


**Positive Polarity (POS)**

The first and most common polarity value used is POS. This is the
marker of positive polarity. This is used for an EVENT that did, in
fact, occur. Most events annotated are of this polarity, and this
is the default value. POS need not be specified in annotation.

- Three **attacks** **occurred** last week.

- Despite international **condemnation**, North Korea is now
officially a nuclear **state**.

- The patient has **hepatosplenomegaly**.

- PO **changes** right pterional **craniotomy**

- The patient will **continue** treatment.


**Negative Polarity (NEG)**

The opposite of POS, as you might guess, is NEG, which is used to
indicate when the event didn't take place, or has an otherwise negative
polarity:

- Three attacks occurred last week, but one **attack** was prevented.

- There is no **sign** of the small plane, and rescuers located
no **survivors**.

- Otherwise, he has not had any **nausea**, **vomiting**,
**diarrhea**, chest **pain**, **shortness** of breath, or **fever**.

- She is not **interested** in pursuing **chemotherapy** at
this time.

- The patient did not **report** **nausea**.

- A cystic duct lymph **node** is not **identified**.

In the last two, there are two EVENTs being negated. The first
is a verbal EVENT of reporting, the second is a condition. In this
case, we can negate both the reporting of nausea and the identification
of the lymph node, as neither occurred. In addition, the nausea and
lymph node aren't present. So, both EVENTs in both examples are negated.




**Actual Modality (ACT)**

Alongside Polarity, you are almost marking ContextualModality -- whether or not an event is asserting things about the ACTUAL world, about GENERIC tendencies of events, HYPOTHETICAL events or UNCERTAIN events.  The majority of EVENTs are ACTUAL, having already happened or been scheduled (without hedging) to happen:

- The patient's new **tumor** is 3.5cm from the epiglottis.

- The patient did not **report** **nausea**.

- His anterior chest rash has not **reoccurred**.

Note that ACTUAL is about whether is it a claim in the "real world", and so NEG events are ususally ACTUAL as well .


**Uncertain/Hedged Modality (UNC)**

EVENTS are marked as UNCertain when we can point to some explicit
lexical or phrasal trigger that indicates some degree of uncertainty
about the reality of the EVENT. Put differently, these EVENTs are
presented with a sort of tacit claim that they're *probably*
real (unlike hypotheticals, which are explicitly irrealis), but with
a proviso from the author that they might be not be. Therefore:

> Only use UNCERTAIN/HEDGED when there is some explicit, local cue for that uncertainty within the document!  

By "local" we mean that you should not use utilize other mentions of the same event in order to  decide between UNCERTAIN or ACTUAL.  You will be allowed to make events coreferential which vary between ACTUAL and UNCERTAIN modalities, precisely because this level of certainty might vary from mention to mention.  

Some good bits of evidence for using UNCERTAIN/HEDGED are lexical or phrasal cues ("seems", "likely", "suspicious", "possible", "consistent with"),  doubtful epistemic cues ("claims", "I suspect that...", "It would seem likely that...") and accusations and charges ("She faces five counts of ....", "He is accused of ..")

Examples of good UNCERTAIN/HEDGED instances are therefore:

- Radiation levels and seismic disturbances were measured which
are consistent with nuclear **testing**.

- Fifteen missing miners, who are now widely presumed **dead**,
are still underground.

- All evidence seems to point to **kidnapping** in the disappearance
of Dr. Charles.

Note that full denial of an event, however is "NEG ACTUAL", as the denial is in the realm of certainty, so that following EVENTs would
*not* be marked UNC:

- She **denies**<sub>ACTUAL</sub> **vomiting<sub>ACTUAL,NEG</sub>

- There is no **evidence<sub>ACTUAL,NEG</sub> of **MS<sub>ACTUAL,NEG</sub>

If something is not quite negative, but close, is it almost always signalling UNCERTAIN:

- There is no concrete **diagnosis<sub>ACTUAL,NEG</sub>
of **MS**<sub>UNC, POS</sub>, but given her **symptoms<sub>ACTUAL,POS</sub>,
it seems extremely likely.

:bangbang: *Remember that this is for textually evidenced uncertainty. No amount of implausibility allows you to inject UNCERTAIN based upon your own opinions:*

- *Yesterday*, I was **[<sub>ACTUAL</sub> abducted ]** by aliens.


**Hypothetical Modality (HYP)**

If ACTUAL is for modality marking certain things known about the world, and UNCERTAIN is for things which are simply unknown, HYPOTHETICAL modality is for situations involving possible worlds; where the cocurrence of the event (in the past or the future) is conditional upon specific (albeit perhaps not specified) event happening. This should fit your usual intuitions about conditionals

- If the Israelis **strike<sub>HYP</sub>**, the US will surely be **dragged<sub>HYP</sub>**
into a larger conflict.

- Any possible **attack<sub>HYP</sub>** would draw widespread **condemnation<sub>HYP</sub>**.

- If she experiences a **fever<sub>HYP</sub>**, we will **treat<sub>HYP</sub>** **it<sub>HYP</sub>** on an outpatient basis.

It is worth noting that, in this schema, an EVENT occurring in the future does not imply that the EVENT is HYP (although most hypothetical
EVENTs will be AFTER DOCTIME); certain future events are ACTUAL.  Thus the following, though having DocTime AFTER, will be ACTUAL:

- The **close<sub>ACTUAL</sub>** of Market Friday will **mark<sub>ACTUAL</sub>** the **end<sub>ACUTAL</sub>** of Mr. Johnson's long career.

Use HYPOTHETICAL in combination with NEG only when one is considering what would happen if the lack of that event occurs, such as:

- The treaty will only hold if there are no more **attacks<sub>HYPOTHETICAL,NEG</sub>**".

In contrast, "counterfactual" contexts -- in which is has been made clear that the even did not happen -- are not actually hypothetical, but ACTUAL-NEG, as one is certain that they did not happen.  Mark only the fact that they did not happen using ACTUAL-NEG (*this therefore means that we will not be making hypothetical annotations of the "what might have happened" causation chains often expressed with counterfactuals, either*)

- Had they **withdrawn<sub>ACTUAL,NEG</sub>** the treaty would have **held<sub>ACTUAL,NEG</sub>**.

Note that using ACTUAL-NEG in the above context is only licensed because the counterfactual construction that is mentioning the events makes it clear that they did not happen.  Any more periphrastic ways of stating facts should be left as HYPOTHETICAL:

- If they **withdraw<sub>HYP</sub>** the treaty will **hold<sub>HYP</sub>**, but they will not **withdraw<sub>ACTUAL,NEG</sub>**

Here are some additional examples to solidify these patterns:

- If Will had stopped by the store, he'd have **bought<sub>NEG/ACT</sub>** cupcakes. But he was too lazy. 

- If Will stopped by the store, he probably **picked<sub>POS/HYP</sub>** up cupcakes. He lacks the fortitude to resist frosting.

- Will stopped by the store, so, of course, he **bought<sub>POS/ACT</sub>** cupcakes. Do you want one?

- If we had added this section to the guidelines earlier, our annotator agreement would have been **better<sub>NEG/ACT</sub>**.


**Generic Modality (GEN)**

Generic event modality is used to refer to two separate kinds of generic eventualities; generalizations and classes of events. You do not need to distinguish the two:

- In the **aftermath** of most **bombings<sub>GEN</sub>**, **trampling<sub>GEN</sub>** is a deadly **threat<sub>GEN</sub>**.

- In New Zealand, bills must be **approved<sub>GEN</sub>** three times by
Parliamentary **votes<sub>GEN</sub>** and then **receive<sub>GEN</sub>** Royal **Assent<sub>GEN</sub>** from the Governor-General.

- Adjuvant **chemotherapy<sub>GEN</sub>** following **surgery<sub>GEN</sub>** is generally **recommended<sub>GEN</sub>** in **situations<sub>GEN</sub>** similar to this.

- I explained that BRAF **mutations<sub>GEN</sub>** have no predictive value
with regard to cetuximab **sensitivity<sub>GEN</sub>**.

Although HYPOTHETICAL and GENERIC may seem similar, remember that
most HYPOTHETICAL EVENTs still refer to the specific content of the
article, depend on some eventuality occurring, and make reference
to specific EVENTs on the timeline.  In contrast, GENERIC events don't require
specific reference or conditions.

This provides an excellent test for GENERIC in practice: If a sentence
would be true if copy-pasted into any contemporaneous article, note,
or text, then it is most certainly GEN. For example, in:

- The terrorists **fled** Jordan via the Lebanese border.

The truth of this fleeing EVENT depends on the identity of the terrorists
and the context of the article to be true or false. Thus, it is ACTUAL. Compare with:

- Terrorists often **flee** to nation-states with crumbling
governments to avoid **interference**.

This fleeing EVENT would be equally true in any article about any
terrorists, international fugitives, or even in an article about governmental
collapse. Thus, both **flee** and **interference** are GENERIC.

The hard cases will be generalizations about ACTUAL, specific people and groups, such as:

- John always eats bananas on his Grape Nuts.

- I lose whenever I play chess.

- Florida voters disappoint me every time. 

- Jill usually got good grades in high school.


When these refer to seemingly habitual events with a clear timespan, you can make them ACTUAL.  Use GENERIC for such ACTUAL entities, instead, if you can robustly and easily paraphrase it in the past and future using a "whenever X, then Y" format:

- Whenever I play<sub>GEN</sub> chess I lose<sub>GEN</sub>

- Whenever John eats<sub>GEN</sub> Grape Nuts he uses<sub>GEN</sub> bananas



### Marking the relationship to document time (DocTimeRel)

DocTimeRel is short for "Document Creation Time Relation", and
represents the temporal relation between the EVENT in question and
the time when the article, post or record in question was created or published
(the "document time"). 

DocTimeRel allows us to avoid the linguistic ambiguities inherent
in explicitly marking the grammatical tense of the verb (like "past",
"present", or "past perfect"), instead marking the actual
temporal relations of the event to the time when the document was
created (marked with DOCTIME in this schema). We've chosen to use
a subset of the temporal relations present in TLINK annotations.

When annotating DocTimeRel on EVENTs, remember that this is the relation
of the EVENT in question relative to the moment in time and space
when the text was written. So an event which occurs before the time
of writing would be given the BEFORE value, but an EVENT which will
occur after DOCTIME will be given the AFTER value for DocTimeRel.
Thus we see that marking DocTimeRel on the EVENT can be thought of
as a faster, easier way to temporally link the EVENT to DOCTIME (rather
than making a TLINK for every event).

One thing to keep in mind when annotating DocTimeRel is that it is
not used to mark the permanence of events. Although it is true that
a person who is dead at DocTime will also be dead for the foreseeable
future, this idea of permanence is really a property of the event
itself, in the abstract, and doesn't need to be marked explicitly.
Similarly, when doing temporal relations annotation, one need not
say that all permanent states (death, birth, some chronic, untreatable
illness) BEGIN-ON DocTime, as they will be automatically processed
later in such a way that it is clear that they persist through the
rest of the timeline.

Unlike the other EVENT attributes, DocTimeRel has no default value,
as it should be filled in individually for every event. Currently,
our schema includes four relations between the event and DOCTIME:
BEFORE, AFTER, OVERLAP, and the combined relation BEFORE/OVERLAP.



**BEFORE**

BEFORE is used where the event ended before the document itself was
written. The bracketed events below would be marked as "BEFORE"
(and all other EVENTs and TIMEX3s are unmarked):

- The **[shooting]** **[shocked]** the small city.

- This is unchanged and may be related to treatment **[changes]**.

- Today's study demonstrates a marked improvement compared to
the prior 9-16-03 **[study]**.


**OVERLAP**

OVERLAP is used for events or states which are
happening or true at the time that the document was written:

- The fires **continue** to **burn** in the Mountains, despite
today's **rain**.

- Captain Smith of the Boulder County Sheriff's office is **requesting**
that anybody with information come forward.

- The patient **continues** to **do** well as an outpatient.

- The patient is **alert**, **cooperative**, and **appears**
to be in no acute **distress**.

- Moderate sized retention **cyst** or **polyp** in the right
maxillary antrum again **noted**.

- She is not **interested** in pursuing chemotherapy
at this time but is **interested** in continued **surveillance**.


**AFTER**

AFTER is used where the event is scheduled or planned to begin following
the document time:

- After the fires are **contained**, residents can **return**
home.

- Thursday's planned **strike** will put **pressure** on the
University to pay graduate teachers a living wage.

- **Levaquin** 750 mg p.o. q. day (will **restart** today)

- The patient will **return** tomorrow for **labs** and **exam**.

- She is not interested in pursuing chemotherapy at this time
but is interested in **continued** surveillance.

It is worth pointing out that in the last example, considered alongside \ref{twin},
shows the interaction between DocTimeRel and ALINK to cover the idea
of "already happening, and will now continue.

There is one specific situation which must be discussed. EVENTs with
a Contextual Modality of GENERIC (discussed in \ref{generic}) will
always have a DocTimeRel of OVERLAP, as stated truths are, presumably,
true at Document Time. See the following:

- I explained that BRAF **mutations** have no predictive value
with regard to cetuximab **sensitivity**.


**BEFORE-OVERLAP**

BEFORE-OVERLAP is used where an event clearly started before the DOCTIME and **continues into and through the DOCTIME**. This often (but not always) corresponds with the use of the English present perfect tense:

- The regime has been **arresting** suspected dissidents and
shows no sign of stopping.

- The fires have **burned** for eight days now.

- The patient has **felt** quite well and his appetite has been
**good**.

- She has not **seen** a cardiologist.

- She has had no **fever**.

- Based on last Thursday's MRI, her **swelling** is mostly gone.

This is not, however, any OVERLAP mention that extends into the past (after all, nearly everything extends *a little* into the past) but rather only for events that have clear and explicit encoding of being true in the past and present.  The following lists define exactly which bits of evidence are allowable for this. This need for evidence also means that multiple mentions of the same event might vary between BEFORE and BEFORE/OVERLAP, or between BEFORE/OVERLAP and OVERLAP, and that is ok.

Be sure that any time you are using BEFORE-OVERLAP, the fact that an EVENT started before DOCTIME and continues is explicitly encoded by the language of the text (rather than through your own inference or world knowledge).  [Here is a list of the kinds of things that are admissable evidence for BEFORE/OVERLAP use](#Permissable Evidence for BEFORE/OVERLAP).  While this should not be considered a closed list, other kinds of evidence for BEFORE/OVERLAP should be similarly explicit. 


##### DocTimeRel in relation to speech

When dealing with documents involving speech (as is often
the case in newswire), there can be a number of conflicting signals
about what the time of an event is.  The general rule to follow is that you are still attempting to encode the relation of the document itself, *not to the speech event*. 

The most obvious example of that is direct speech.  In direct speech, there is often no real cue as to the actual DocTimeRel of the spoken-of event, and thus one may need to utilize world knowledge, as in:

> - Napoleon declared<sub>BEFORE</sub> "I will conquer <sub>BEFORE</sub> Russia"

> - Musk declared<sub>BEFORE</sub> "We will get<sub>AFTER</sub> to Mars in my lifetime"




#### Event Type, Aspect and Implicitness


#### Annotating contextual aspect of EVENTs

We have two values for contextual aspect in the schema, N/A and INT.
Please note that this is unrelated to grammatical aspect, and these
two aspects give information about the temporal relations in the document,
not about the grammatical forms used to express them.


###### N/A

N/A is our default value for contextual aspect, and simply represents
that a given EVENT is not intermittent, and is true consistently.


###### INT - Intermittent

INT is used in situations where there may be a series of smaller events
within a single EVENT, rather than a single, constant event. Those
events are usually marked with words like "intermittently" or
"occasionally", and when such phrasing is used, the EVENT is marked
as INT. These indicate that, for instance, the patient has had vomiting
since a certain time, but he/she has not been vomiting 24/7 since
that point.

Please note that INT will only be used for irregular, unpredictable
periods (like the period of time between seizures or vomiting) and
not for things like medications or dialysis (which occur on a set
schedule). An event which occurs at an explicit interval can either
be treated as a constant ("the patient is taking **montelukast**
for asthma") or the interval can be marked as a TIMEX3 ("She undergoes
dialysis **every three days**"), which is then TLINKed to the
original event.

It is important to note that we are only marking INT when there is
an explicit mention of intermittency in the sentence. Even if you
happen to know that a given EVENT or disorder often manifests intermittently,
if it is not stated explicitly as doing so, you should not mark it
as such. As with all of these annotations, we are marking the relations
mentioned in the document, not those you can infer from your own background
knowledge.

- Occasional **protests** have occurred in the last six months.

- The region is on edge after 2 years of sporadic **violence**.

- He reports occasional bright red **bleeding** from the rectum.

- Patient complains of intermittent chest **pain**.

- She has had intense **headaches** on and off since her last
visit.

If you are unsure about the contextual aspect of a given EVENT, mark
it as N/A.


#### Type of EVENTs

Some EVENTs do not actually represent real-world events, but instead,
provide aspectual information (starting, stopping, continuing) about
other EVENTs. To differentiate these EVENTs from the traditional clinical
EVENTs which occur on a timeline, we use the "type" marker. It
has three values: "N/A", "ASP", and "EVI. 


###### N/A

N/A" is the default value, and represents the vast
majority of EVENTs in the schema, and unless explicitly mentioned
otherwise (below or in the ALINK section), represents all EVENTs used
in examples in the Guidelines. Unless the EVENT is of the specific,
relatively closed class listed below under ASPECTUAL, or providing
evidential information (see EVIDENTIAL), it will be marked as "N/A"
(or, as it is the default value, left blank).

One other note on the word "recurrence", which is often troublesome
for annotators working with the N/A/ASPECTUAL distinction. In an example
like:

- She has significant risk for tumor **recurrence**.

recurrence" does actually carry some aspectual information
(the tumor would have restarted). However, because the word "recurrence"
would not be aspectual in "she has risk of recurrence", we have
chosen never to mark the word as an ASPECTUAL EVENT. Instead, this
will be an EVENT of type N/A, with a span of "**recurrence**",
as shown above. No ALINK annotations will be made here.


###### ASP - Aspectual

The next EVENT type is ASP, which is used to indicate an event whose
function is to emphasize or code the aspect of a later event, like
"continues",restart", or "terminated.
Every EVENT of type "aspectual" must later participate in an ALINK.

- The community **continues** to worry about the possibility
of future strikes.

- Although there had been a period of relative peace, the desecration
of the temple **restarted** sectarian violence once again.

- The rash has not **reappeared** and we will monitor closely.

- We're going to **hold** her heparin until after her surgery.

- The patient will **continue** treatment.

- She is not interested in pursuing chemotherapy at this time
but is interested in **continued** surveillance.

These represent a relatively closed class, and you will find yourself
marking the same words as aspectual EVENTs over and over again. This
is expected, and should not be cause for concern.

A particularly good way of distinguishing between ASPECTUAL and non-aspectual
EVENTs is by substitution. A true ASPECTUAL can always be substituted
(even if losing some meaning) with similar ALINK triggers:

- We **completed** treatment today

Here, **completed** could be rephrased as "We stopped/ended/finished/finalized/terminated
treatment today. Compare that with:

- She **completed** the form

This **completed** cannot be replaced by "She stopped/ended/finished/finalized
the form" without significant coercion of meaning, and thus, is
not ASPECTUAL.

So, if you're marking an EVENT ASPECTUAL, the EVENT in question will
need to be able to be paraphrased (while retaining most of the meaning)
using words from one of the below four sets, each corresponding to
a different ALINK type (INITIATES, TERMINATES, REINITIATES, CONTINUES):


- started/began/initiated/got going
- stopped/ended/finished/finalized/terminated/held
- restarted/started over/began again/reinitiated
- continued/persisted in/proceeded in/didn't stop


If an EVENT cannot be paraphrased using any of the words above, it
is not aspectual.


###### EVI - Evidential

The other EVENT type is EVI, or "evidential", markings verbs of showing, demonstration, evidence, reporting, confirmation
or revelation.  An EVENT should be marked EVI *only* if it serves as the link
between a source of knowledge or observation and a piece of knowledge
gained from it, and can include any lexical items labeling that other examples are in question:

- Satellite photography **shows** increased troop movements
near the border.

- The Chicago newspapers **reported** the victory hours before
it was made official.

- Subsequent bloodwork **revealed** severe anemia, and the patient
was admitted.

- Dr. Green **pointed** out a patch of skin discoloration suspicious
for melanoma.

- We will plan to proceed with surgery unless her tests **indicate**
cardiac problems.

- His home health nurse **noticed** a mild increase in confusion
and fatigue during chemotherapy.

- CT scan **confirms** diverticulitis.

- She has a **confirmed** sulfa allergy.

It is worth reiterating that one does not mark the test, reporter,
or perceiver as EVI; instead, you will mark the verb of perception,
reporting, revelation, or indication as an EVI EVENT.

Finally, much like aspectual \textsc{event}s, you will be likely marking
the same verbs as EVI over and over again, and will very quickly learn
to recognize which verbs belong to this class and which do not.


#### Annotating representation of EVENTs

Some EVENTs that we will mark are not necessarily explicit EVENTs,
but rather, ENTITYs which are interpreted in context as representing
an EVENT.


###### Default -- Explicit

This is the default value, and corresponds to an EVENT whose span
itself represents an EVENT:

- There was an **attack** last week.


###### Implicit

The other possibility is an EVENT whose span looks like it should
only be a ENTITY, but which nonetheless represents an implicit EVENT
derived by metonymy.

- I've prescribed 15mg **Levaquin** for a UTI.

In \Last , "Levaquin" is an entity, but has an implicit "taking
Levaquin" EVENT.

- The **bomb** ended the festival three days early.

Here, "bomb" is metonymic for the attack itself, in addition to
representing the explosive device. The physical bomb did not end the
festival, rather, its detonation.

Because you may need to include IMPLICIT EVENTs' ENTITYs within larger
coreference chains (and thus, will need a marked ENTITY annotation),
please mark each METONYMIC EVENT both as an EVENT with the METONYMIC
type specified, and as an ENTITY.


#### Annotating degree of EVENTs

In order to express an incomplete degree of an EVENT, the "degree"
of an event is specified.

In practice, degree is used as a companion to polarity, as a way of
allowing us to say that something is "mostly" or "a little bit"
true, rather than forcing us to call every EVENT 100\% positive or
negative. Allowing something to be "a little true" ("She has
slight pain") or "largely false" ("her scar is nearly gone")
permits greater nuance in our representation of EVENTs than POS or
NEG generally allows.


#### N/A, MST - Most and LTL - Little


Our three different degrees are N/A, MST, and LTL. N/A is used where
there is no need to mark either of the other two degrees on the EVENT,
and is the default value for degree. These are used when there has
been "a little" of an event, or a large (but not complete) change:

- She was only slightly **injured** by the blast. (LTL)

- The temple was mostly **destroyed** in the recent violence.
(MST)

- There is a small amount of bright T1 **signal**. (LTL)

- Abdominal tenderness has nearly **disappeared**. (MST)

- She feels slightly **weak** but has resumed most of her normal
activities. (LTL)


#### Marking Difficult annotations

The RED schema includes a method for you, the annotator, to highlight
annotations which are particularly difficult to make, or which they
feel fall on the border between different categories.

The "Difficulty" marker automatically defaults to "None" for
every EVENT created. However, if you feel unsure about any aspect
of the annotation, whether the identification of the EVENT itself
or the properties of it, they can change this marker to "DIFFICULT",
simply as an indicator of uncertainty in the annotation. This will
serve to highlight the annotation for further examination.

If you find a particular ambiguity or question leads you to mark "DIFFICULT"
more than once or twice, you should reach out to your annotation supervisors
for clarification of the rules and policies involved.


## Temporal Expressions

Because we're looking specifically at temporal relations, the next
step of the annotation process is to find and annotate TIMEX3 objects.
These are definitive references to time, and will provide concrete
temporal references throughout the document or section. Examples of
these might be phrases like "today", "tomorrow", "24 hours
ago", "at this time" and "early March. In addition,
specific dates are annotated as TIMEX3 objects as well.


### Identifying and Annotating TIMEX3s

Our approach to marking TIMEX3s is identical to that used in ISO-TimeML,
and these guidelines are heavily based on the standard established
in \cite{pustejovsky2010iso}.

Unlike with EVENTs, we will not be selecting headwords only. Instead,
syntactically speaking, all TIMEX3 annotations should correspond to
a:

- Noun phrase ("this weekend", "tomorrow", "yesterday",
"Tuesday", "Last May", "May 16th", "6/9/1985"). 
- Adjective phrase ("two-hour-long", "half-hour--as
in "a half-hour trip", "preoperative", "post-partum") 
- Adverbial phrase ("lately", "recently", "shortly", "hourly",
"intraoperatively"). 

Importantly, this means that any prepositions which precede (or in
some cases, follow) a temporal expression are to be left unmarked,
*even when they seem to provide additional context for interpreting
the TIMEX3*. For example:

- During *the month of July*, she will come visit.

- From *May 1st* to *the 3rd*, she will refrain from eating
solid food.

- After *tomorrow*, she should be OK to walk with crutches.

- He'll come in for a follow up *two days* after his surgery,
and again *the next week*.

These prepositions (referred to as SIGNALs in ISO-TimeML), although
important in the interpretation of the meaning of the temporal expressions,
provide separate temporal information which will be automatically
extracted later.

Note that post-expression adverbs (often "ago") are still captured
in our spans, so:

- Patient s/p lumpectomy *2 yrs ago\

For the most part, if you have two separate temporal expressions,
they'll be two separate TIMEX3s, but two adjacent TIMEX3s which together
specify a single time can be treated as a single span. Look at the
contrast in \Next:

- \a. I'll come by to check on her at *3:30pm Tuesday* \b{.
I'll come by to check on her at *3:30pm* and on *Tuesday\

In (b), we know that the doctor is referring to two different timepoints,
so we mark two TIMEX3s, whereas in (a), the "3:30pm" and "Tuesday"
combine to specify a single timepoint.

The only exception to this rule is when the two temporally connected
TIMEX3s are syntactically separated, as below:

- On *Tuesday*, I'll come by to check on her at *3:30pm*.

- She'll come in for another consult *the day* after *tomorrow*.

In these cases, mark two separate TIMEX3s, even though they combine
to specify one timepoint. The sole exception to this rule comes with
long-form times:

- Mr. Mullins arrived at *5 minutes to five*.

But in medical texts, these are extremely rare.

As one might imagine, TIMEX3s which are separated by a conjunction
are to be treated separately as well:

- She should be fine for discharge on *Tuesday* or *Wednesday*.

- He will come in on *the 1st* and *the 5th* for followups.

Finally, please include in the TIMEX3 span things like time zone identifiers,
time offsets, or other information which provides information which
is helpful in establishing the point of time being discussed.

- He posted *Jan. 5th, 2013 at 6:00pm -700 UTC*\textquotedbl{

- We'll talk at *5pm Mountain\

- She called around *2pm (MDT)\

- His email was sent at *6:59pm (-500)*.

- Our meeting *tomorrow* is at *9pm Eastern/8pm Central*.

- The collapse occurred *at 2am, plus or minus an hour or so*.


### Annotating TIMEX3 class

Note that in the examples below, if there are multiple TIMEX3s, only
those which are of the indicated class will be marked.


#### DATE

The majority of TIMEX3 annotations you make will be of the class DATE.
DATE represents dates. These can be calendar dates (such as *January
4*) and other verbal expressions which can be mapped to calendar
dates either concretely (such as *Last week*, *This month*, *next
Friday*, or *this time*), or in a more fuzzy sense (*lately*,
*the past*).

- MRI of the brain without and with gadolinium contrast utilizing
tumor followup protocol compared with prior studies of *29, February
2005* and *28, January 2005*.

- His anterior chest rash has not reoccurred since the PCN VK
was discontinued *24-hours ago*.

- At *this time*, we see no reason to discontinue the treatment.

- The last cyclosporine level was 373 in *January*. His dose
was adjusted downward to 300-mg twice-daily. A cyclosporine level
will be repeated on *Friday morning*.

- I stated that if there is no other evidence of any disease recurrence,
in *approximately one-month's time* we would proceed with approximately
six-months worth of adjuvant therapy.

- The form was signed and scanned on *December 29, 2009*.

- I would probably restart her furosemide *tomorrow morning*.

- She came in *a couple months ago*.

- She had an appendectomy *two-to-three years ago*.

- Mr. Zegler was seen in the Hamilton University Medical Center
with Dr. Carr *the middle of December 2009*.

- Carotid artery disease, last checked *greater than two years\
prior.

- After *next week*, we will see where her pain level is.

- *June 6, 2008*, through *October 6, 2008*, treated with
FOLFOX.

As mentioned above, DATE is also used for very generic sorts of TIMEX3s,
where you may not be able to point at a specific day, week, or month
on a calendar, but can still gesture at the overall timeline. So,
for instance, expressions like "the past", "lately", "the
future", or even "previously", would be TIMEX3s of the type
DATE:

- She has experienced heavy bleeding in *the past*.

- She complains that she's felt tired *lately*.

- *Recently*, she has had several episodes of syncope.

- He wasn't sure he wanted surgery at *that point*.


#### TIME

TIME is used for specific time points within a day, for instance,
*3:00PM* or *23:45*, and once again can be relative (as in example
\NNext):

- The patient's MRI is scheduled for *5:30pm\

- Following the patient's latest seizure *20 minutes ago*, we
are re-evaluating her medications.

- At *the time of consultation* there is no operative report
or pathology available.

- Surgery will need to be completed by *2:45* to have the biopsy
to the lab sooner.

Put differently, temporal expressions which give minute-by-minute
or hour-by-hour detail are marked as TIME. Day-by-day (or larger)
detail is marked with DATE.


#### DURATION

Sometimes, you will be given a single temporal expression interpreted
as reflecting a span of time, rather than a point. These are things
like "for *24 hours*" or "All of February", and these are
marked with the class DURATION.

- The patient continuously experienced nausea for *nearly two
weeks*.

- For *the next 12 hours*, we will lower the patient's morphine
drip and then we will re-evaluate his pain.

- Since *August*, she has not had any episodes.

- Patient did well *overnight*.

- During *the last 12 months*, she's been nauseous frequently.

- Since *February 18th*, he hasn't seen his doctor.

- In *the last week*, his pain has significantly worsened.

- He has been doing this for *five years*.

- I stated that if there is no other evidence of any disease recurrence,
in approximately one-month's time we would proceed with *approximately
six-months* worth of adjuvant therapy.

- In *the time* between now and the 15th, she should attend
physical therapy whenever possible.

Note that in \Last, both *now* and *the 15th* would also be TIMEX3s,
but of type DATE.

Remember again that more abstract temporal expressions ("lately",
"in the past", "in the future"), although representing loosely
defined spans of time, are considered DATE rather than DURATION, as
they are predominantly only bounded at the start or the end, not both,
as above.

Finally, remember that two dates can be used to construct a duration,
but, because each represents a single point in time (rather than duration),
both will still be labeled DATE, rather than DURATION:

- From *May 1st*$_{\text{DATE}}$ to *the 3rd*$_{\text{DATE}}$,
she will refrain from eating solid food.


#### QUANTIFIER

Although it may seem odd at first, expressions like "Twice", "four
times", and "18 times in the month of May" are all TIMEX3s.
These are annotated with the QUANTIFIER class.

- The patient vomited *twice* before the surgery.

- We have seen Mr. Lastname *three times* for his ulcerative
colitis.

- On *two to three incidents* she has had blood in the stools.

Note that Quantifier only applies for number of occurrences of an
EVENT, not for quantifiers like "She has *two* eyes" or
"She lost *5* units of blood.


#### PREPOSTEXP

Similarly odd, Pre- and Post- expressions ("preoperative", "post-exposure",
"post-surgery", "prenatal", "pre-prandial") all actually
designate specific temporal spans ("The time before the surgery",
"The time after exposure") related to an implicit EVENT, and thus,
are TIMEX3s, marked with the class PREPOSTEXP. Usage of this TIMEX3
is discussed in more detail in Section \ref{prepostexp}.

- Patient underwent a partial hemicolectomy in July 2009. *Postoperative\
scarring noted during exam.

- The patient exhibits *post-exposure* changes.

These will not always begin with "pre-" or "post-.
Terms like "intraoperatively" are PREPOSTEXP as well, as in \Next:

- *Intraoperatively*, there were no difficulties securing his
airway. He received 4 liters of crystalloid, made 300 mL of urine
and estimated blood loss was 50 mL. He received a dose of DDAVP in
the OR out of concern for uremic platelet dysfunction.

And sometimes, you will have bare expressions which clearly express
the PREPOSTEXP meaning, but do not contain the whole expression.

- Pulmonary recommendations for *pre*, *peri* and *postop\
were made.


#### SET

SET is used exclusively in our schema for covering expressions which
give both a quantifier and an interval (like "Three times weekly",
"monthly" or "1/day") and represent a frequency. This is different
from QUANTIFIER ("twice") which only gives a quantifier, and different
from DURATION ("all week") which only gives a timespan.

Even though most sets could be interpreted as a QUANTIFIER and a DATE/TIME
juxtaposed, we should mark them as a single span ("*twice monthly*"
rather than "*twice* *monthly*").

- Will administer Lariam *twice daily*.

- Patient has checked into the ER *roughly three times a month*.

- We will proceed with *weekly* consultations to monitor the
patient's condition.

- Mirtazapine REMERON 7.5-mg tablet 1 tablet by mouth *every
bedtime*.

- Simvastatin ZOCOR 20-mg tablet 1 tablet by mouth *one-time
daily*.

TIMEX3s of type SET should always be TLINKed to EVENTs using the TLINKs
of the type OVERLAP.


### TIMEX3s vs. Temporal Manner Adverbs

Although TIMEX3s are generally uncontroversial and straightforward,
there is one ambiguity which merits further discussion. First, consider
the below examples:

- He **stopped** the polar bear's **rampage** quickly.

- He **stopped** the polar bear's **rampage** in *twenty
minutes*.

In \LLast, "quickly" is quite clearly not a TIMEX3. It is not
placeable on a timeline, it cannot be normalized to a date or time,
and really, it doesn't tell us much about time, but about the stopping.
Compare this to *twenty minutes*, which is clearly temporal. We
know that *twenty minutes* entirely contains the stopping, and that
it refers, on the timeline, to a period of 20 60-second intervals
beginning at the point on which he started trying to stop the rampage.

Compare these to the below sentences, where there's an ambiguity between
reading the highlighted word or words as a straightforward DURATION
TIMEX3, or as a manner adverb indicating speed of action:

- I can write that report up in <5 minutes>. 
> The report will
be ready at the time DOCTIME + 5 minutes. 
> When requested, I can write it up quickly, likely within 5 minutes.

- The party leader claims that Japan "can arm itself with nuclear
weapons <overnight>" in response to the continued aggressions. 
>  Japan can arm itself with nuclear weapons in the period of time from
dusk on the day of DOCTIME to dawn the next day. 
> Japan can arm itself, whenever it chooses to, in around 12 hours, or, in a figurative
sense, "abruptly.

In both, the first reading inteprets the marked expression
as being DURATION TIMEX3s, which CONTAIN the EVENTs (`write' and `arm'),
and which can be concretely placed on a timeline. In the second readings,
the marked expressions are effectively manner adverbs indicating "quickly",
which float above the timeline, and thus, are not TIMEX3s at all.

In situations like these, where both the TIMEX3 and the
manner adverb reads are possible, *interpret ambiguous DURATION/Manner
Adverb expressions as DURATION TIMEX3s*. This way, we consistently
teach the computer to recognize sequences of text which could be DURATION
TIMEX3s, and we are able to get more temporal information than would
otherwise be possible. Humans, reading the text down the road, can
always understand and interpret as a manner adverb, if it's helpful.


### DOCTIME and SECTIONTIME Annotation

Because all of these annotations are linking the EVENTs and TIMEX3s
to the time of patient service, it is important that we specify what
that time actually is. When there is information about the time of
writing or publication, we select that time as the DOCTIME. DOCTIME
can be considered a special sort of TIMEX3, and is annotated similarly.

It is worth noting though, that because of the complexities of medical
records or news articles, some sections might have a separate, local
time. These will always include a specific date, which will be marked
not with DOCTIME, but with SECTIONTIME. In these cases, any DocTimeRel
annotations will link to this section-specific time. **If no separate
date is explicitly given for a section, assume that it shares the
overall DOCTIME**.

- **head start date=**12/13/2010**" rev=0002**

Here, the **12/13/2010** would be marked as DOCTIME, as "start
date" is the closest thing to the "Document Time" that we have
for this record.

- Published **June 15th, 2013** by Jackson Teller-Morrow

Here, obviously, the Doctime is the publication time.

- UPDATE: **Saturday, February 20, 2010 at 3:34 PM**: According to Broomfield county sheriffs, the victim of the shooting
has died at St. Joseph Hospital.

Here, **Saturday, February 20, 2010 at 3:34 PM** would be considered
SECTIONTIME, as all that follows it will be true as of this new timestamp.




## DUPLICATE marking for repeated spans of text 

Some documents may have significant amounts of copy/pasted or automatically
quoted text. If, as you are annotating, you come across a section
or paragaph which is identical to one previously found (and fully
annotated) in the document, you should *not} annotate EVENTs,
TIMEX3s, ENTITYs, or any relations in that section or paragraph, and
instead should select the entire paragraph or section which is repeated
and mark with DUPLICATE.


#### Guidelines for finding DUPLICATE text

As to avoid throwing out otherwise good data, DUPLICATE does have
a few hard and fast laws of usage to keep in mind:
- Even if a section or paragraph is repeated several times in a note,
*the first instance of that section or paragraph which occurs
must be fully annotated}. DUPLICATE is only used for subsequent repetitions. 
- DUPLICATE text must stand off from novel text in some way. An inline
quote or repetition does not qualify as DUPLICATE, even if it is a
verbatim repetition. For example:


- Earlier, Will wrote "DUPLICATE text must stand off from novel
text in some way". This is completely accurate, and you should trust
him. He knows these things.


The quoted portion would *not* be eligible for DUPLICATE annotation,
and you would want to reannotate the EVENTs, ENTITYs, and LINKs between.
Were that same sentence presented as an offset quote (as in an email
reply), though, it would be eligible.

- DUPLICATE sections must be exactly duplicate, excepting formatting
changes. Even if two paragraphs differ by only a few words, they are
no longer considered DUPLICATE. Changes to line-breaks, formatting,
or the addition of quoting characters (e.g. ">" or "")
are not important enough to merit full re-annotation, and you're still
welcome to mark as DUPLICATE.
- DUPLICATE sections must be intentionally duplicated (automatically
or copy/pasted), rather than a part of human-generated text. In a
discussion forum post about cat ownership, many people may say "I
have a cat." (although it's unlikely to be offset from the matrix
text, as discussed above). Multiple people saying the same things,
even if they use the same words, does not constitute DUPLICATE.


Remember that DUPLICATE means that a section of text will *not
be annotated at all at any point in the process*, and improper use
(on text that isn't actually duplicated) will rob us of valuable data.
If you're unsure as to whether something is sufficiently similar,
offset, or automated to be DUPLICATE, err in favor of fully annotating
the text.


## Entity Coreference Relations


While you are annotating the EVENT/ENTITY markables pass, we want
you to also annotate all Coreference\textquotedbl{
relations betweene ENTITIES. These can be thought of in two categories
-- relations that show that two things are the same (IDENT and APPOS)
and relations that show that they have a structural relationship,
such as PART/WHOLE, SET/MEMBER, or the catch-all BRIDGING relation.

These guidelines for coreference annotation have been adapted from
the OntoNotes v. 7.0 (\cite{pradhan2007ontonotes}) and ODIE (2010)
guidelines as needed to accommodate the objectives of the RED schema.
Additional concepts and information were synthesized from Poesio et
al. 2004 (\cite{poesio2004centering}), Poesio 1997 (\cite{poesio1997conversational}),
and Savova et al. 2011 (\cite{savova2011anaphoric}).


### IDENTITY and APPOSITION of ENTITIES


#### IDENTICAL 

Two entities have an IDENTICAL relation if they refer to the same
discourse referent. The IDENTICAL relation has several important semantic
characteristics(Following the MUC-7 specifications): 

- The relation is symmetrical, i.e., non-directional: (if A is IDENT
to B, then B is IDENT to A). This is different from relations like
WHOLE/PART and SET/MEMBER, which are directional by defition. 
- It is also transitive: if A is IDENT to B and B is IDENT to C, then
A is IDENT to C. . 

The canonical example of this, and perhaps the bulk of IDENT annotation
work, will be the marking of pronominal antecedents:

- Mr. **Smith**$_{N1}$ complained of a headache. **He**$_{N2}$
also had a sore throat.

Yet in many instances on will be linking together lexical nouns that
refer to the same thing. Two different ways of refering to the same
thing -- like Michele Obama, she, and First Lady in the example below
-- belong in the same chain.

- **Michele Obama**$_{e1}$ is a busy **lady**, **she**$_{e1}$
visits many schools around the country during the year. Just last
week, the **First Lady**$_{e1}$ was in Wisconsin teaching kids
why it is important to eat healthy and exercise.

Yet the above example also illustrates this question of what to
do with attribution, as in the entity is a busy **lady**.
The fundamental rule we'll follow with this is the following: 

- If X is Y is actually showing the equivalence
of the identities of two mentions (such as Clark Kent
is Superman), then these are IDENT. 
- If X is Y asserts a SET/MEMBER relations,
mark it as such. The such as test is
a good metric in this case -- you can restatae the relationship in
\ref{Mobama} as busy ladies such as Michele Obama,
but one can't say Supermen like Clark Kent 
- If X is Y doesn't show Y as a set, and
the two described entities are the identical, but the attribute is
a role (Joe is the vice president),
a defined role that is not a separate referent (Joe
is the tallest man in the room), then use BRIDGING. 
- If X is Y is very predicative (the Y
is less of a separate referent and more of an attribute of X) and
cannot be framed as a SET/MEMBER or BRIDGING relationship, then do
not mark any relation at all. 

#### APPOSITIVE

Two entities have an APPOSITIVE relation if two NPs having the same
semantic meaning occur adjacent to one another, separated only by
punctuation - almost always a comma, colon, dash, or parenthesis.

Remember that when we talk about adjacency, you have to think about
the larger noun phrases that each single entity mention represents,
including relative clauses. So the example in \ref{apposlong} is
an appositive, even though the head words are not next to each other.
This may make sense if one looks at the syntactic tree -- note that
their separate noun phrases are split:

- My **friend** who works there, **John Smith**, makes bread.

- \Tree [.S [.NP [.NP [.NP [.DT my ] [.NN friend ] ] [.RelativeClause who works there ]] [.NP John Smith ] ] [.VP makes bread ]]

Unlike IDENT chains, which may contain many different referents in
the same relationship, this is a relationship with only two points.
The leftmost term must always be the HEAD and the right mention is
the ATTRIBUTE, except when one of the two phrases is a proper name,
in which case the proper name must be the HEAD regardless of position:

- The U.S. **President**$_{\textsc{attribute}}$, **Barack
Obama**$_{\textsc{headsc}}$

We will only consider the Head of an APPOSITIVE relation as eligible
to participate in other relations with entities outside the APPOSITIVE
relation, not the ATTRIBUTE.

There are a number of specific nominal constructions that we will
count as APPOSITION. One is any sequence of titles -- either in normal
speech, or during the description of titles as in:

- **Smith**$_{\textsc{head}}$, MD, FFF, **Pathologist**$_{\textsc{attribute}}$.

Unit conversions are also considered appositives.

- **37.00C**$_{\textsc{head}}$ (**98.60F**$_{\textsc{attribute}}$)

In some cases, APPOSITIVES may include multiple entities. In the case
that there are more than 2 markables in the apposition, we will nest
these using multiple, separate APPOS relations.

- **AUTHOR**: Company **President**, **Mr. Johnson**

We would create one APPOSITIVE in which **Mr. Johnson** would be
the Head, and **President** would be the Attribute. Then, we would
create a second APPOSITIVE with **President** as the Head, and **AUTHOR**
as the Attribute. In these cases, we still would only include the
HEAD of the first APPOSITIVE in other relations, thus, **AUTHOR**
and **President** would not be eligible for inclusion in any other
relation. You probably noticed that due to the nature of the nesting
and the specificity of the proper name **Mr. Johnson**, the nesting
worked right-to-left instead of left-to-right. We could not have had
**President** be the attribute of both APPOSITIVE relations. The
proper name takes precedent in determining APPOSITIVE phrases with
multiple ENTITYs, as it is more specific on the specificity hierarchy:
\\


\centerline{Proper noun > pronoun > definite NP > indefinite specific
NP > non-specific NP

If both ENTITYs have the same level of specificity, select the left-most
ENTITY as the head.


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
for cases of compositionality, i.e. narrow readings. In order for
an entity to be Part of another, it must be 100\% contained by the
Whole, and compositionally part of it. Thus, the following examples
do not contain any WHOLE/PART relations:

- **Mt. Everest** lies on the border between **China** and
**Nepal**.

- In the **house**, there are several **visitors**.
Note that WHOLE/PART relationships are essentially *hierarchical},
in that they may theoretically have a whole chain of relationships
(a hair is part of a dog, a dog is part of a pack, spatial relations,
such as:

- We saw the **White house** while in **D.C.**.

The difference between these two previous examples reveals
a difficult boundary case that you will have to ponder -- what counts
as compositionally part of a thing.
This is particularly salient when the whole\textquotedbl{
is a larger spatial entity such as a city, county or country. When
in doubt, remember this compositionality\textquotedbl{
idea. If the removal of the potential part\textquotedbl{
would have the potential of changing the nature of the whole,
even a slight bit, then one might consider it compositional and use
WHOLE/PART. If, in contrast, the part is merely temporarily or arbitrarily
located in the space of the other item, do not use WHOLE/PART.

:bangbang: *Note that while IDENT, SET/MEMBER and BRIDGING will also be
used to mark EVENTS, WHOLE/PART is only for ENTITIES. Relationship
that you are tempted to mark as WHOLE/PART should probably be CONTAINS-SUBEVENT
or SET/MEMBER instead.*


### SET-MEMBER

A SET-MEMBER relationship exists when one entity or event can be thought
of as one or several members of a larger group. SET-MEMBER relations
can be between ENTITIES or between EVENTS.

- The **trustees**$_{S}$ have to sign off on the ordinance
before we proceed; however, the trustee **Mr. Gamal**$_{S}$ says
agreement has been hard to come by.

- **Patients**$_{S1}$ with **cancer**$_{S2}$ are advised
to avoid this medication. Our **patient**$_{M1}$ has kidney **cancer**$_{M2}$
and lung **cancer**$_{M2}$, so we will not prescribe it. 

(Notice also that **Our** and **we** are in an IDENTICAL relation.)

- Patient has two **arms**$_{S}$. Her left **arm**$_{M}$
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

If you are unable to use one of the previously discussed links, but
it is apparent that some sort of link exists which entails that the
events have some sort of link, then use the BRIDGING relation.

There are a few specific cases in which BRIDGING can (and should)
regularly be used:


Links of asserted identity, where the assertion is itself questioned
or questionable: 


- **John** was arrested last night, as authorities claim **he**
is the **killer** of a local cobbler, found Monday. 
> **John** IDENTICAL **he** 
> **John** BRIDGING **killer**

- **Grigory Kuznetsov**, long thought to be **"Rosebud"**,
a key Cold War CIA asset, died Friday. 
> **Grigory Kuznetsov** BRIDGING **"Rosebud"**

Links that would otherwise be IDENTITY or APPOSITION, but are no longer valid. For
instance:

- **Ratzinger** was **Pope** until his retirement in 2013.
>  **Ratzinger** BRIDGING **Pope**

- **Greg Bear**, former **Head** of the National Croquet society,
died Wednesday. 
>  **Greg Bear** BRIDGING **Head**

Because BRIDGING is intended as a last resort, there are other contexts in which bridging may be used to link entities, but such new instances should be brought up for discussion to check if it is truly BRIDGING. 


### General Guidelines for Annotating Coreference


#### Never link EVENTs to ENTITIES (except with BRIDGING)

In all coreference relations (IDENTICAL, APPOSITIVE, WHOLE/PART, AND
SET-MEMBER), Entities can be linked to Entities, and Events can be
link to Events, but Entities and Events will never be linked within
the same coreference relation. If you encounter an occasion where
you are tempted to do this, check that your Entity is not actually
an Event, or that your Event is not actually an Entity, as the case
may be.

Occaisionally one will encounter an ENTITY and an EVENT which are
essentially two facets of the same complex markable.
Usually we strongly bias towards EVENTs, but this will occaisionally
occur, and the two should be linked using BRIDGING. 

>The company says it stores your **<sub>entity</sub> texts**
on its server for thirty days after you **<sub>event</sub>
text** them

> texts BRIDGING text

#### WHOLE/PART, SET/MEMBER, and BRIDGING relations are inherited by IDENT
chains

If you have an IDENT chain represented by A-A-A-A-A, and A participates
as the PART in a WHOLE/PART relation or as the MEMBER in a SET/MEMBER
relation, conceptually, all mentions of A are PARTs of the WHOLE or
MEMBERs of the SET, too. You do not need to include every mention
of A as a PART of the WHOLE or as a MEMBER of the SET. Only the most
recent mention of A ought to be included in the relation. The other
mentions will be connected to their place as a PART or a MEMBER through
spider-webbing.


#### Bridging relations are re-created for subsequent mentions

In bridging relations (i.e. WHOLE/PART, SET/MEMBER), any new mention
of the WHOLE (or the SET) that is followed by mentions of the PARTs
(or the MEMBERs) merits a new relation. For example, consider the
relations in the following:

- **I**$_{M1}$ met with the **patient**$_{M2}$ today. **We**$_{S1}$
discussed treatment options for **her**$_{M2-1}$ cancer. **We**
also reviewed in **our**$_{S2}$ discussion the results of **her**$_{M2-2}$
recent CT-scan. **My**$_{M1}$ recommendation is adjuvant chemotherapy.
\a. SET **We**$_{S1}$: MEMBERs **I**$_{M1}$, **patient**$_{M2}$,
**her**$_{M2-1}$ 
> SET **our**$_{S2}$: MEMBERs **her**$_{M2-2}$,
**My**$_{M1}$

In this example, **I**$_{M1}$ and **My**$_{M1}$ are IDENTICAL;
**patient**$_{M2}$, **her**$_{M2-1}$, and **her**$_{M2-2}$
are IDENTICAL; and **We**$_{S1}$, **We**, and **our**$_{S2}$
are IDENTICAL.


#### Use SET/MEMBER to define groups of people

The members of groups of people (i.e. **we**, **they**, the **board**
of directors, etc.) are always annotated with SET/MEMBER relations,
as in \Last, not WHOLE/PART.


#### Don't link ACTUAL and GENERIC items

In analogy with the principle for not TLINKing HYP/GEN to ACT/UNCERTAIN
events, ACTUAL and GENERIC items can never be in an IDENTICAL, APPOSITIVE,
or WHOLE/PART relationship. They can, however, be SET/MEMBER, as in
\Next:

- **I** discussed with **Mrs. Ambry**<sub>ACTUAL</sub> the results
of a local clinical trial in which **patients**$_{GENERIC}$ with
**cancer**$_{GENERIC}$ recovered successfully on the **drug**
without reoccurrence. Given **her** colon **cancer**<sub>ACTUAL</sub>
and the success of the **drug**, **I** recommend **it**. \a.
SET **patients**: MEMBER **Mrs. Ambry** 
> **Mrs. Ambry**
IDENTICAL **her** 
> SET **cancer**$_{GENERIC}$: MEMBER **cancer**<sub>ACTUAL</sub>

> **I** IDENTICAL **I** \e. **drug** IDENTICAL **drug**,
**it**


#### Identifiers are people too

Email addresses (and other person-specific identifiers) can be linked
to their referent humans using IDENTICAL or APPOSITIVE.

- You should contact **Bill Franklin** for more information.
**He**'s **bill.franklin@hotmail.gov** \a. **Bill Franklin**
IDENTICAL **He**, **bill.franklin@hotmail.gov**

- **George Maddox** (**exampleguy6969@hotmail.gov**) should
be able to help you out. \a. **George Maddox** APPOSITIVE **exampleguy6969@hotmail.gov**

- Did you ask **Herbie** (**prairiedog1564** on here)? **He**
might know! \a. **Herbie** APPOSITIVE **prairiedog1564**, **He**

- Ms. **Jenny Tutone** (SSN: **867-53-0900**) was arrested
last week. \a. **Jenny Tutone** IDENTICAL **867-53-0900**

Phone numbers are not person-specific, and thus, are not eligible
for these relations.


#### If Identity is uncertain in the document, use BRIDGING (even if you know the truth)

Occasionally, authors (or context) will suggest
coreference or identity, or will explicitly state the uncertainty
of coreference.

- **Hans Holbein**, a local **man**, was arrested in connection
with the murder of a local blacksmith. The **alleged killer** is
being held without bond. The **killer** reportedly had a large tattoo
of a squid on **his** face, similar to the one present in **Mr.
Holbein's** booking photo. 
> **Hans Holbein** IDENTICAL **man**, **alleged killer**,**Mr. Holbein's** 
> **killer** IDENTICAL **his**

In this example, all that we can be sure of is the two IDENTICAL chains
above. It is incredibly tempting, especially given the seemingly irrefutable
squid, to jump to conclusions and merge (a) and (b) into one massive
IDENTICAL chain. However, in our schema, all ENTITYs are different
until proven IDENTICAL, and Mr. Holbein deserves a fair trial.

However, there is irrefutably *some sort of relationship* between
Mr. Holbein and the killer. Whether this relationship is of legal
identity, actual identity, or simply a mistaken prosecution by an
over-zealous district attorney, we cannot know, but we know that there
certainly is one. To mark an ambiguous relationship like this, we
use the non-specific BRIDGING link:

- **Hans Holbein**, a local **man**, was arrested in connection
with the murder of a local blacksmith. The **alleged killer** is
being held without bond. The **killer** reportedly had a large tattoo
of a squid on **his** face, similar to the one present in **Mr.
Holbein's** booking photo. \a. **Hans Holbein** IDENTICAL **man**,
**alleged killer**,**Mr. Holbein's** 
> **killer** IDENTICAL **his** 
> **killer** BRIDGING **Mr. Holbein's**

By doing this (alongside the other necessary annotations), we've established
two clear IDENTICAL chains, and made clear that there is a link between
them, even though the nature of that link is unclear in the text.

Here's another example of a relation based purely on judgement:

- In response to the bombing, the US has dispatched agents to
**Yemen**, **Somalia**, **Norway** and **South Sudan**. An
official in a later conference stated that terrorists often seek out
**countries** with little law and order as a safe haven.

Here, it's tempting to use one's knowledge of the world to SET/MEMBER
**countries** with **Yemen**, **Somalia**, and **South Sudan**
(and to likely exclude **Norway**). However, no such relation is
given in the text, and therefore, one should not be created.

Finally, there are cases where a relation might be unclear in the
text, and recoverable only by guesswork. For instance, imagine a series
of discussion forum posts like the below (which have been adapted
from an actual document, and in no way represent the political views
of anybody associated with RED):

- **Barack Obama** was born in Nigeria, he's not American, and
his presidency is illegal. That's why **he** loves **immigrants**!

- It's terrible, I hate these illegal **immigrants** taking jobs
from hard-working **Americans**. 
- **Barack Obama** IDENTICAL **he** 
- **immigrants** SET/MEMBER **immigrants** (representing the fact that illegal immigrants are a subset of immigrants)

In addition to the (uncontroversial) relations above, there are three
pitfalls, all based on external knowledge.


- Americans SET/MEMBER Barack Obama


This is fairly uncontroversial in most circles, but is contradicted
in the text. We cannot mark it based on our understanding of the world.

- Americans SET/MEMBER immigrants, immigrants


Again, this is a matter of perspective, and should not be marked without
support in the text.

- immigrants SET/MEMBER Barack Obama


That Obama is an illegal immigrant is strongly implied by these posts.
However, it's not explicit, and therefore, we cannot mark it.



So, again, in summary, your annotations need to be sourced from the
text itself, rather than from your knowledge of the entities, people,
and places involved, and asserted IDENTITY links can be made using
BRIDGING.


#### Identity Annotation for very broadly GENERIC entities

Some set/member relations are so general that they define huge, all-encompassing
sets. This is most clear when considering terms such as everything,
which may sometimes be worth marking yet which we don't want to mark
as containing all other entities.

This is different from the question of entities in which set-membership
is in doubt; instead, these are cases in which the set membership
is clear but somewhat trivial. For the sake of tractability (and your
own sanity as annotators), a small set of extremely broad GENERIC
instances will be defined as being out of the scope of our annotation.

Terms to omit from SET/MEMBER annotation: 
- Everyone, people,
and generic you: When these are used
in the truly broad sense (so that they encompass all persons mentioned
in the text), omit them from annotation. 
- generic we, everyone,
and people, when they do not describe
a document-specific set like americans\textquotedbl{
but rather some broader generic set like humanity,
does not get set/member relations. 
- someone, anyone,
one: These do not entail set/member
relationships between themselves and the possible candidates. 

#### IDENT over generic you, one, etc.

We do, however, want to grab identity relations with very generic
terms, and especially want identity relations with terms like you.
The question that arises -- especially with terms like you,
one, etc. -- is whether these should
all be contained within the same IDENT chain.

Many times with GENERIC you, as with
somebody, we initiate a possible world
that would be true for any member of the set, and continue that hypothetical.
In such a hypothetical, we want an identity chain between the same
mentions. Put more concretely; given two mentions of generic you,
you can usually replace the first with either somebody,
one or anyone\textquotedbl{
in English. In that case, the question is whether later mentions can
be replaced with pronoun such as they,
he or she\textquotedbl{
without changes in the implied meaning. If so, they deserve to be
IDENT in the same chain; otherwise they are probably different. So
for example:

- If you get out on parole, what happens then, and how long does
it last? (and, specifically, who takes you home once you get out of
jail, or do you just get turfed out and expected to check in with
your parole officer the next day?).

rephrasing attempt:

- If *someone} gets out on parole, what happens then, and
how long does it last? (and, specifically, who takes *them
home once *they} get out of jail, or do *they} just
get turfed out and expected to check in with *their} parole
officer the next day?).

In consider two other sentences, presumably from the same document.
While these both fit into the idea of GENERIC you, the second doesn't
pass this same hypothetical somebody\textquotedbl{
test:

- If you choose not to vote, then you choose to give your opponents
all the power. This is another case of well what did
you bloody well expect to happen?

the rephrasal attempt seems to change the meaning in this one, and
thus these should be different IDENT chains:

- If *someone} chooses not to vote, then *they
choose to give *their} opponents all the power. This is another
case of well what did *they} bloody well expect
to happen?



# Event Relations Pass: Linking Events Together


The next step of RED annotation is to take those EVENTs and TIMEX3s annotated in EVENT annotation and mark relations between them.  For example, in a simple sentence as follows, the "temporal structure" that we need to capture is that the leaving event happened on Sunday:

> John **[left** <sub>event</sub>**]** for China on **[Sunday** <sub>Timex3</sub>**]**

We have a set of labels we use for marking what the actual temporal relationship is between two events or times, such as:

> - **Before:** We **[ate** <sub>event</sub>**]** before we **[left** <sub>event</sub>**]**.
> - **Begins-on:** We were **[listening** <sub>event</sub>**]** to the radio as soon as we started **[driving** <sub>event</sub>**]**.
> - **Contains:** During the **[vacation** <sub>event</sub>**]** we **[visited** <sub>event</sub>**]** my aunt.

If you glance at any story or newspaper article, however, you will find that a given story or document will have many, many eventualities and times, and that for any two of them, you can often discern some temporal ordering.  That would be a lot of relations to annotate! 

Instead, we will be avoiding such a "spiderweb" of temporal relations by attempting to mark *small amounts* of *very informative* temporal relations between notes, using the idea of **narrative containers**.

## Narrative Containment

Temporal structure of a narrative is often hierarchical. If, on a particular Tuesday, you go on a series of errands, one of which is going to the store, and during that visit you get milk, you could say that that Tuesday temporally contains the errands; that they temporally contain your trip to the store, and that it temporally contains the event of getting milk.  

![nesting1](narratcon.png)

The importance of that is that if someone were to know that an event happened before Tuesday, they then inherently know that it also happened before *all of Tuesday's events*.  

While we build narrative containers using this temporal relation CONTAINS, the idea of "Narrative containers" is not simply the idea of that relation, but this goal of using these increasingly large temporal "buckets" to cleanly capture the temporal essence of a passage in an informative manner (as detailed in [Pustejovsky and Stubbs 2011](http://www.aclweb.org/anthology/W11-0419) and [Styler et al 2014](http://www.aclweb.org/anthology/Q/Q14/Q14-1012.pdf)).



 A narrative container can be thought of as a temporal bucket into which an EVENT
or series of EVENTs may fall. These narrative containers are often
represented (or "anchored") by dates or other temporal expressions,
but may also be anchored by a reference to an EVENT capable of containing
another EVENT -- a surgery might contain an incision, or a war may
contain battles. By focusing on placing events in progressively larger
temporal buckets, you eliminate the need for most relationships between
individual events -- if container A is BEFORE container B, we know
that all events inside A are before the events in B, without needing
to make those annotations manually. As such, rather than marking every
possible temporal relation (TLINK) between each EVENT, we instead
try to link all EVENTs to a narrative container, and then link those
containers so that the contained EVENTs can be linked by inference.

While TIMEX3 and EVENTs can be temporal containers, we also have another kind of temporal container; the DocTimeRel itself.   The "Tuesday" above is therefore a temporal "bucket" that is within a larger bucket of BEFORE -- the set of all events happening before the document creation time.



### Temporal Containers vs Subevent Containers

Labeling temporal containment properly is primarily a task of marking which *temporal* spans contain other temporal spans.  This means, specifically, that we mark containment purely on whether it is temporally marked as containing other events when no semantic connection at all, such as:

> - While I was writing this paper, some couple has met, been married and had a child.
> - In 1841, Martin Van Buren was elected and the First Opium War began
> - During the surgery, a butterfly in Kashmir flapped its wings three times.

These are in contrast with temporal structure that also conveys a kind of "essential" structure between related events, as in:

> - The battle of the bulge was an important battle in world war II
> - During the surgery, most of the tumor was excised.

While the temporal span of "surgery" contains all of the events going on in the universe during that period of time,
only some events -- such as the excision -- could be characterized as being subevents of that surgery, sharing participants, locations, and consequences with the larger event.  We will define these as a subtype of containment, CONTAINS-SUBEVENT.  






### Choosing the Anchors of Narrative Containers

When creating narrative containers as discussed above, you will need
to choose either a TIMEX3 or an EVENT to be the "anchor" of the
container, the temporal span which all of the other EVENTs fall within
(or begin/end on). Choosing which temporal span to be the anchor of
a given narrative container can be difficult, so here are a few ground
rules to help make these decisions easier and more consistent:

- The majority of TIMEX3 annotations will be narrative container
anchors. 

- If you have a choice between using an EVENT or a TIMEX3 as
the narrative container anchor, you should pick the TIMEX3. 

- If you use an EVENT as a narrative container anchor, try to
TLINK it to a few other container anchors to avoid it being stranded. 

- If stuck between two possible containers, use the one with the larger
temporal span. 

- Remember that if an event contains multiple different "steps"  -- even if they are connected in a sequence -- they will be separate subevents. 


## When to add Temporal Links other than CONTAINS


Temporal Links (TLINKs), as previously mentioned, are relations you
can mark between EVENTs, between TIMEX3s, or across the two categories
to show the temporal relations present within the document and to
clearly define the bounds of the narrative containers at work beyond
what DocTimeRel will naturally give us. As mentioned previously, we
will display these links in this document using the following format:

- **EVENT1** RELATION **EVENT2**

The containment relations discussed above are expressed using two of these: CONTAINS and CONTAINS-SUBEVENT.  The remainder of the temporal links are BEFORE, OVERLAP, BEGINS-ON, ENDS-ON and SIMULTANEOUS, and two of those (BEFORE and OVERLAP) can also be subtyped into whether they also contain causal information (BEFORE/CAUSE, BEFORE/PRECONDITION, OVERLAP/CAUSE, OVERLAP/PRECONDITION).  

Which relation to select will be detailed in specific sections that follow.  First, one must decide whether a relation should be annotated at all.  Without any constraint, one could see making TLINKs between every
EVENT in the document, which leads to exponential growth of TLINKs
and a tangle of relations which nobody, let alone a machine, would
like to unpack.  So we use a series of rules -- structured to rely upon these intuitions about temporal containers -- in order to determine which things actually should get temporal links


### TLINK all EVENTs to their narrative container, if possible.

As previously discussed, most EVENTs will fall into a narrative container
of some kind. If a given EVENT is in a narrative container (like "August
22nd" or "during her recovery"), you should always TLINK that
EVENT to the TIMEX3 or EVENT which represents that narrative container,
using the appropriate link. 

When annotating, not every EVENT will be a part of a detailed narrative
container (i.e. one specific than just the BEFORE, AFTER or OVERLAP relation to DOCTIME). However,
it is vital that you, as an annotator, stop to ask yourself whether
each EVENT you examine is a part of a narrative container, and whether
you have marked that with a CONTAINS TLINK. 

In this pursuit, you should almost never be marking more than one containing event.  We assume that if  you label that A contains B, and that B contains C, you do not need to also mark that A contains C.  For example, if Wednesday CONTAINS football game, and that football game CONTAINS a throwing event, we don't need to also know that the throwing event happened on Wednesday -- it's inferrable from the annotations already done. 





## Temporal Relation Annotation

#### Causal links should be chained where possible

In the same way that we are trying avoid redudancy by thinking of temporal structure as being "nested" into larger and larger containers whenever possible, we also want to think of causation as amounting to a series of chains of causation. In general, you may assume that:

* If Event A CAUSES or PRECONDITIONS Event B, and Event B CAUSES or PRECONDITIONS Event C, we don't need to mark causation between A and C
* If Event A CAUSES  or PRECONDITIONS Event B, and Event B CONTAINS-SUBEVENT Event C, we don't need to mark causation between A and C

This means that an example such as the following only needs two causal relations -- while the burglaries do lead to an eventual "jailed" event, we can assume that it is inferrable:

- **He** was **jailed** after **pleading** guilty in **court**
following a series of **burglaries**
> **burglaries** BEFORE/PRECONDITIONS **pleading**
> **pleading** BEFORE/CAUSES **jailed**

Similarly:

- The death toll from a **bombing** in Bangkok **rose** to
three on Monday after a doctor **confirmed** that a six-year-old
girl had **died** from her **injuries**. 
> **bombing** OVERLAP/CAUSES **injuries** 
> **injuries** BEFORE/CAUSES **died** 
> **confirmed** REPORTS **died** 
> **died** BEFORE/CAUSE **rose**
> **confirmed** BEFORE/CAUSES **rose**

Here, again, we can infer that bombing
caused the death toll to rise, without explicitly marking all possible causation links. These chained annotations, much like narrative containers, allow us
to leave easily inferable links unspecified. In this way, we can fully
capture the causal nature of the situation without specifying every
small step.




### Mark temporal order only when it adds information not inferrable from containers or DocTimeRel

Remember that every EVENT  with a doctimerel of BEFORE is in a large narrative container (the events happening before the document time), every EVENT with a doctimerel of OVERLAP is in a container that defines the document time, and so forth, adn that these containers have a natural order.  Marking that a BEFORE event happens before and OVERLAP event, then is redundant information: we already know that due to the DocTimeRel containers that they are a part of.  

This also means that TIMEX3s such as "now" or "in the past", if they are synonymoous with the DocTimeRel containers themselves, do not need to be linked to, as they provide no additional information about the event. 



### TLINK all explicitly stated temporal relations.

If the writer goes out of his or her way to make a temporal statement,
a TLINK should be made to reflect that statement. So, if the sentence
reads:

- The patient **developed** a **rash** after **treatment**.
>  **treatment** BEFORE **rash** 
> **treatment** BEFORE **developed**

You should explicitly mark the treatment as being BEFORE both **developed**
and **rash**, using a TLINK, regardless of the fact that **developed**
and **rash** will also be ALINKed. Note, though, that if no explicit
temporal language is used, no TLINK should be created, and annotator
knowledge should not be used to fill these TLINKs in.

### Don't mark temporal order (BEFORE, BEGINS-ON, etc) that lacks explicit evidence in the text

Because of the difficulty of capturing detail within a given narrative
container, not all relations between EVENTs will be captured. For
instance, in the following example, containment alone doesn't tell us the relationship between [dinner] and [session]:

> During the [conference] there was a [session] in which they [thanked] Mr. Smith and a catered [dinner]

In many cases, sufficient world knowledge, inference or research may let an annotator guess what the order of these events is.  However, unless there is explicit grammatical evidence for the ordering -- most obviously, prepositions and connectives like "Before", or thing like "and then" -- do not infer anything about the relationships between them. 


### Do not link TIMEX3s to one another.

Although there is certainly a temporal relation between, say, "January
15th, 2009" and "March 2013", part of the post-processing of
these annotations is the normalization of these Temporal Expressions,
which will allow us to order these expressions on a timeline based
on the times they represent. Although you will certainly still TLINK
EVENTs and TIMEX3s, the TIMEX3s in the document can almost always
be temporally ordered without the annotator's help.


### GENERIC events should only link to other GENERICS, HYPOTHETICAL to other HYPOTHETICALs

HYPOTHETICAL and GENERIC EVENTs aren't really on the same timeline as other EVENTs in the discourse. Because of this, it can be quite tricky to
link them to the overall timeline, and we need to take care to avoid
having non-real EVENTs showing up on a timeline. To avoid the
complications and potential broken relations when non-real EVENTs
are pruned from timelines, ACTUAL or UNCertain EVENTs should never
be linked to HYPOTHETICAL or GENERIC EVENTs, and vice versa. In this
way, "real" EVENTs are never linked to non-real ones.

- Adjuvant **chemotherapy** following her upcoming **surgery**
would generally be recommended, but given her poor **health**, this
is not an option.

Here, because the **chemotherapy** is HYPOTHETICAL, it cannot be
TLINKed to **surgery**, even given the explicit mention.



### Causal temporal relations should be within the same paragraph whenever possible


### Non-causal, non-CONTAINS relations should only go outside of the sentence in specific situations

Both for the sake of consistency, and because they require explicit evidence in order to be annotated, you should avoid annotating temporal ordering relations (such as BEFORE, OVERLAP or BEGINS-IN) across sentences.

The exception to this, ususally, will be adjacent sentences in which the main events to the two sentences are related.  When those adjacent sentences define a clear temporal order, but cannot be represented as having one contain another or one cause another, you may link them using BEFORE. 






### EVENTs may participate in many ordering links, many causal links, but should only have one CONTAINS relation

There can be multiple causes and preconditions for a single event:

- After **loading** **his** **pistol** and **chambering**
a **round**, the **instructor** **pulled** the **trigger**
and **fired** a **shot** as a **demonstration**. \a. **loading**
BEFORE/PRECONDITION **fired** 
> **chambering** BEFORE/PRECONDITION
**fired** 
> **pulled** BEFORE/CAUSE **fired**

Similarly, a single EVENT can cause or precondition several other
EVENTs:

- **He** has **seen** **people** **decapitated** by barrel
**bombs** and **others** who **lost** **their** **limbs**.
\a. **bombs** OVERLAPS/CAUSES **decapitated** 
> **bombs**
OVERLAPS/CAUSES **lost** 
> **others** IDENTICAL **their**

However, if an event is contained by multiple narrative containers, you should only be linking it to one -- see [the section on selecting narrative containers](#choosing-the-anchors-of-narrative-containers) for more information on which one to select.




## Discerning TLINK sub-types

There are ten different temporal relations often used in this schema,
BEFORE, BEFORE/CAUSES, OVERLAP/CAUSES, BEFORE/PRECONDITIONS, OVERLAP,
SIMULTANEOUS, BEGINS-ON, ENDS-ON, CONTAINS, and CONTAINS-SUBEVENT.
There is no default relation type for TLINKs.


### BEFORE

BEFORE is fairly straightforward and simply orders two events in time.

- The 8th Infantry will **arrive** before **sundown**. 
>  **arrive** BEFORE **sundown**

- She **vomited** shortly before **surgery**. 
> **vomited** BEFORE **surgery**

- His anterior chest **rash** has not **reoccurred** since
the **PCN** VK was **discontinued** *24-hours ago*. 
> **discontinued** BEFORE **reoccurred**<sub>NEG</sub> 
> **rash** BEFORE **reoccurred**<sub>NEG</sub>
> **rash** ENDS-ON **discontinued** (Discussed below.)
> *24-hours ago* OVERLAP **discontinued**

(**PCN** will be linked to **discontinued**, 
using an ALINK of the type TERMINATES, as described in [the Section on ALINKs](#alink-sub-types).

When annotating, remember that "X occurred after Y" can be expressed
by saying "Y occurred before X: 

- The **shooting** came shortly after the drug dealer's **release**. 
>  **release** BEFORE **shooting**

- She was **seen** by Dr. Jones in cardiology following the
stent **placement**. 
> **placement** BEFORE **seen**

- He had a car **accident** shortly after his **visit**. 
>  **visit** BEFORE **accident**

- He had a **neckache** after **surgery**. 
> **neckache** BEFORE **surgery**


### CONTAINS

CONTAINS signals that the beginning and the end of the CONTAINed EVENT
is completely temporally contained within the temporal span of the
EVENT or TIMEX3 it is related to. In other words, the contained event
occurs entirely within the temporal bounds of the event it is contained
within. This relation is most often used to mark when an EVENT is
contained entirely by a narrative container.

CONTAINS is a very specific relation implying complete containment
within a narrative container, and if you annotate that X CONTAINS
Y, it is assumed that there is also an OVERLAP relation between the
two. You should only use CONTAINS when you are sure that the nature
of the overlap is one of complete containment.

- In *2007*, 15 people were **killed** outside Mumbai. 
> *2007* CONTAINS **killed**

- During the US-led **invasion**, reporters **rode** along
with actual military units. 
> **invasion** CONTAINS **rode**

- *March 2005* - Patient underwent **appendectomy** 
> *March 2005* CONTAINS **appendectomy**

- **Levaquin** 750 mg p.o. q. day (will **restart** *today*)
> *today* CONTAINS **restart**

- **Comparison** is made with prior MRI head **examination**
without and with gadolinium from *10-23-03*. 
> *10-23-03* CONTAINS **examination**

- An ENT performed the ** my** during *Friday*'s **surgery**.
> *Friday* CONTAINS **surgery**

- **Gengraf** 300-mg p.o. b.i.d. (**decreased** in *early
June*) 
> *early June* CONTAINS **decreased**

In addition, we have made one specific regulation involving the use
of CONTAINS: All test results or observations are to be linked to
the test which generated them (their narrative container) using a
CONTAINS relation, *assuming there is actually temporal containment*.
This is not always intuitive, because as humans with some inferencing
ability, we realize that the tumor likely existed before the CT scan
which revealed it, but from a machine-learning perspective, it is
important to have that consistency. So, in a section like:

- **Colonoscopy** (*January 7, 2010*): Fair/adequate **prep.**,
Limited **Colonoscopy** to the distal sigmoid due to an obstructive
**lesion**. Diminutive **polyps** of the rectosigmoid. 
> *January 7, 2010* CONTAINS **Colonoscopy** 
> **Colonoscopy** CONTAINS **lesion** 
> **Colonoscopy** CONTAINS **polyps**

:bangbang: *There are many relations which seem like a sort of semantic
containment (things like part/whole, cause/effect, disorder/symptoms).
However, the CONTAINS relation should only
be used when there exists strict temporal containment (the temporal
span of the container fully encompasses that of the contained).



### CONTAINS-SUBEVENT

Similarly to the way that we've chosen to consider causality as a
temporal relation, we are treating event/sub-event relations as temporal
as well, as they too have an inherent (and necessary) temporal relation,
this time, of CONTAINment.

Anything that is truly a sub-event, an EVENT which is a necessary
component part of a greater whole EVENT, will necessarily be temporally
contained within the greater whole, in the same way that a part of
an object is spatially contained (in most cases) within the whole
of the object. Put differently, if the temporal span of one event
does not contain the entire duration of another event, the two are
not in a CONTAINS-SUBEVENT (nor CONTAINS) relation but rather, they
are two different events, perhaps causally linked, or, perhaps just
temporally linked.

When one finds one EVENT which temporally contains another, one must
decide whether they are simply in a CONTAINS relation, or whether
they are in a CONTAINS-SUBEVENT relation. We've chosen to take a very
narrow view of events and sub-events: if an EVENT is a necessary subpart
of another event, as viewed in an encyclopedia or generic semantic
representation of the larger EVENT's type, it is a sub-event.

- There were 5 different **skirmishes** during the marathon
**battle**. 
> **battle** CONTAINS-SUBEVENT **skirmishes**

- During *Friday's* **surgery**, the patient's heartrate **spiked**
during the initial **incision**. 
> **surgery** CONTAINS-SUBEVENT
> **surgery** CONTAINS **spiked** 
> **incision**  CONTAINS **surgery**

- The **tornado** was accompanied by high **winds** and multiple
funnel **clouds**. 
> **tornado** CONTAINS-SUBEVENT **winds**
> **tornado** CONTAINS-SUBEVENT **clouds**

- **Colonoscopy** (*January 7, 2010*): Fair/adequate **prep.**,
Limited **Colonoscopy** to the distal sigmoid due to an obstructive
**lesion**. Diminutive **polyps** of the rectosigmoid. \a. **Colonoscopy**
CONTAINS-SUBEVENT **prep.**

If there is no such link of necessity, or if this event is a part
of this particular instance, but is not expected in the majority of
instances, the relationship is simply containment:

- There was a **thunderstorm** during the marathon **battle**.
\a. **battle** CONTAINS **thunderstorm**

- During *Friday's* **surgery**, the patient's heartrate **spiked**
when she **fell** off the table. \a. **surgery** CONTAINS **fell**

> **surgery** CONTAINS **spiked** 
> *Friday* CONTAINS
**surgery** 
> (**spiked** BEGINS-ON **fell**) -- Discussed
below in Section \ref{corefannotation}.

- The **earthquake** occurred during the **parade**. \a.
**parade** CONTAINS **earthquake**

- There was a large **interruption** when the colonel and his
guards **burst** into the parliament **debates**. \a. **debates**
CONTAINS **interruption** 
> **debates** CONTAINS **burst**

> (**interruption** BEGINS-ON **burst**) -- Discussed below.

:bangbang: *Remember, CONTAINS-SUBEVENT is still a CONTAINS temporal relation.
If you have two items that are event/sub-event, but where the EVENT
does not temporally CONTAIN the sub-event, use the generic BRIDGING
relation.*

### OVERLAP

OVERLAP is a single temporal relation that encompasses all the different
notions of two things happening at the same time, but is less specific
than CONTAINS or SIMULTANEOUS. This can refer to two nearly simultaneous
events, an EVENT that occurs during another larger EVENT or time reference
(but where containment is not entirely sure), or any other sense in
which two events are occurring in the same time frame:

- While the mayor **spoke** to reporters about his latest anti-cartel
**initiatives**, his home was being **raided** by state officials.
> **spoke** OVERLAP **raided**

- The hurricane **struck** while G8 members **discussed**
climate change just a few hundred miles away. 
> **struck** OVERLAP **discussed**

- The patient's first **MI** occurred while she was undergoing
**chemotherapy**. 
> **chemotherapy** OVERLAP **MI**

- The patient had some rectal **itching** and mild **pain**
*today*, mostly *this morning*. 
> *today* CONTAINS **itching**
> *today* CONTAINS **pain** 
> *this morning* OVERLAP **itching** 
> *this morning* OVERLAP **pain**

- He does have a history of peri-rectal **abscess** with his
last round of **chemotherapy**. 
> **chemotherapy** OVERLAP **abscess**

- She is not **interested** in pursuing chemotherapy at *this
time*. 
> *this time* OVERLAP **interested**<sub>NEG</sub>

In short, OVERLAP is meant for situations where two events overlap
in some way, but where you are not sure (or do not have enough information
to tell) whether there is containment of the events' boundaries.

OVERLAP is also used for linking TIMEX3s of type SET with other EVENTs,
as in \Next:

- We will keep her on rate-control **medications** 100 mg *twice
daily* \a. *twice daily* OVERLAP **medications**

:bangbang: *OVERLAP provides relatively little information for the actual
processing of text compared to our other temporal relations. If you
are reasonably sure that the relation is one of containment, you should
use one of the CONTAINS relations instead, and often, one can represent
a potential OVERLAP more specifically using narrative containers and
a bit of additional thought.*


### BEFORE/CAUSES, OVERLAP/CAUSES, BEFORE/PRECONDITIONS and OVERLAP/PRECONDITIONS

Although these are included in the list of TLINKs during annotation,
and carry the same temporal information and properties as BEFORE and
OVERLAP, they carry additional causal meanings, and are fully explained
in the causation section.


### BEGINS-ON

BEGINS-ON signals that the EVENT begins on the EVENT or TIMEX3 it
is related to. This type of TLINK will only occur with EVENTs which
have a non-trivial temporal span. Relations with punctual EVENTs will
usually be marked with BEFORE instead.

Note that BEGINS-ON is to be used only where there is no causal relationship.

- *2008* marked the **start** of the rebels' brutal **campaign**
\a. **start** BEGINS-ON *2008\

- She has had Abdominal **Cramping** since *January*. \a.
**Cramping** BEGINS-ON *January\

- He reports intermittent chest **pain** since his prior **MI**.
\a. **MI** BEFORE **pain**


### ENDS-ON

ENDS-ON signals that the EVENT ends on the EVENT or TIMEX3 it is related
to. As with BEGINS-ON, this type of TLINK will only occur with EVENTs
which have a non-trivial temporal span. Relations with punctual EVENTs
will usually be marked with BEFORE instead.

- The "occupy" **protests** largely **ended** when the
weather grew too **cold** for **camping**. \a. **protests**
ENDS-ON **cold**

- She has had no **bleeding** since her **stitches** were
**removed**. \a. **bleeding**<sub>NEG</sub> ENDS-ON **removed**

Note that ENDS-ON can be used in concert with BEGINS-ON to mark a
duration.

- She was on **chemo** from *March* through *July*. \a.
**chemo** BEGINS-ON *March* 
> **chemo** ENDS-ON *July\


### SIMULTANEOUS

SIMULTANEOUS means exactly that: Two EVENTs have the same temporal
boundaries and extent.

SIMULTANEOUS is, technically speaking, a more specific type of OVERLAP
relation, and SIMULTANEOUS is to be used only when there is strict
simultaneity, that is, both the start- and endpoints of two temporal
entities are *exactly* the same.

In the real world, such simultaneity does not often arise from coincidence
(and when it happens to be the case, it is widely commented on and
celebrated). Generally, true simultaneity only happens by coordination
(So long as the president is **aboard**, the carrier
will be on high **alert**) or by necessity (I'll
**drink** as long as my cup is **full**).

- She **listened** to music during her whole **drive** home.
\a. **listened** SIMULTANEOUS **drive**

In this case, she started a music-listening EVENT when she began her
ride, and ended when the ride ended. There is a functional relationship.

- Cell phones must be **turned** off while in **flight**.
\a. **turned** SIMULTANEOUS **flight**

The start and end of **flight** represent the start and end of the
prohibition, so, necessarily, SIMULTANEOUS.%
\footnote{Of course, the event is "turned off", but the head of this multi-word
expression is "turned".%


- For the duration of her **surgery**, the anesthesiologist
**monitored** her pulse at the wrist. \a. **surgery** SIMULTANEOUS
**monitored**

The anesthesiologist's monitoring would necessarily start and end
with the surgery.

In many cases of true simultaneity, there is a relationship which
borders on causality. However, these are usually not true causality
(representing strong correlation, rather than necessary causation),
and *when two EVENTs are unquestionably SIMULTANEOUS and questionably
causal, we will mark the more specific SIMULTANEOUS relation, rather
than using OVERLAP-CAUSE*.

- While they **recorded**, the red light stayed **on**. \a.
**recorded** SIMULTANEOUS **on**

- The whole time that John **raced** around the track, his **frightened**
mother **clutched** her seat with white knuckles. \a. **raced**
SIMULTANEOUS **clutched** 
> **raced** BEFORE-CAUSE **frightened**

In this case, the clutching is likely to start and end with the racing,
but alas, the fear persists.

There are many instances of false or one-sided simultaneity to avoid:

- He was **sad** when she **visited**. \a. We're not sure
that the sadness began or ended when she arrived or left. OVERLAP.

- The bombers **shouted** while they **ran**. \a. It's unlikely
that they began shouting when they began running, persisted throughout,
and stopped when they stopped running. OVERLAP.

- The Colorado fires **burned** throughout the **summer**.
\a. Colorado did not catch fire on June 21st, and promptly extinguish
itself on September 23rd. **summer** CONTAINS **burned**

- She **talked** with her Mom while I **made** dinner. \a.
It is not asserted that she started the call when I picked up a spatula,
nor hung up as the food hit plate. If you can get from context that
the talking is CONTAINS, do it; otherwise, OVERLAP.

Be very cautious in your use of simultaneous, as each SIMULTANEOUS
relation you make is asserting that both the start- and endpoints
of two EVENTs are either strongly and purposefully linked, or correspond
exactly as part of a massive coincidence or conspiracy.

Put differently, there are instances of SIMULTANEOUS out there, but
they are rather like running into a celebrity at your local supermarket:
your first reaction should be skepticism and doubt, and if you manage
to remain convinced despite careful consideration, it's cause for
celebration and excited Facebook posts%
\footnote{The authors of these guidelines are not responsible for friends lost
due to excited "SIMULTANEOUS EVENT/EVENT TLINK!!!" facebook posts%
}.

Unless you are sure that the start of the first EVENT is
the start of the second, and similar for the end, use CONTAINS or
OVERLAP.

:bangbang: *You do not need to create SIMULTANEOUS TLINKs for EVENTs which
are in an IDENTICAL chain. Two identical EVENTs share both temporal
bounds, and thus, are SIMULTANEOUS, but we will generate those links
later. Only mark SIMULTANEOUS for non-coreferent EVENTs.*


### Expressing TLINK Types in Point Algebra

A more precise (although perhaps more esoteric) way to express temporal
relations is using point algebra. In the style of [Allen 1983](https://en.wikipedia.org/wiki/Allen%27s_interval_algebra),
we can take the start and end of event A to be A- and A+, respectively,
and compare those points to the start and end of EVENT B, B- and B+,
using < ("less than") and > ("greater than") to indicate position
on the timeline.

Given this notation, our TLINK types can be expressed as below:

| Relation |  Notation | Meaning | 
| -------- | --------- | ------- |
| BEFORE  | A+ < B-  | A is before B | 
| CONTAINS  | (A- < B-) AND (A+ > B+)  | A contains B |
| CONTAINS-SUBEVENT  | (A- < B-) AND (A+ > B+) | A contains B |
| OVERLAP  | (A- < B- < A+) OR (B- < A- < B+)  | A and B overlap |
| BEGINS-ON  | A+ = B-  | B begins-on A |
| ENDS-ON  | A- = B+  | B ends-on A |
| SIMULTANEOUS | A- = B- AND A+ = B+  | A is simultaneous with B |

Note that our definitions of OVERLAP and SIMULTANEOUS are symmetrical,
in that "A OVERLAP B" and "B OVERLAP A" mean the same thing.
For OVERLAP, which EVENT starts first is not recoverable from the
annotation without prior knowledge of both A- and B-.

### Annotating TLINK Features

### Annotating polarity of TLINKs

Polarity of TLINKs is identical to polarity
in EVENTs, although naturally the applications will differ slightly.
Polarity is used and applicable with TLINKs of all types.


**POS - Positive**

As with EVENTs, the default and most common polarity value used is
POS. This is the marker of positive polarity. This is used for a temporal
specification that is not negated. Most TLINKs are of this polarity,
and this is the default value. POS need not be specified in annotation.

All examples in this guideline, unless otherwise marked, represent
POS TLINKs.


**NEG - Negative**

TLINKs are marked as NEG only when they are both explicitly asserted
*and* asserted to be false.

- The **bombing** did not take place on *the 18th* as expected,
but on *the 24th*. \a. *18th* CONTAINS -- NEG **bombing** \b{.
*24th* CONTAINS -- POS **bombing**

- The **earthquake** did not cause the **fire**, instead,
**it** was caused by an electrical **short** . \a. **earthquake**
BEFORE/CAUSES -- NEG **fire** 
> **short** BEFORE/CAUSES --
POS **it** 
> **earthquake** BEFORE -- POS **fire**

- The **meeting** was not on *Thursday*. \a. *Thursday\
CONTAINS -- NEG **meeting**

It is important to contrast these with the below:

- The **meeting** on *Thursday* didn't occur. \a. *Thursday\
CONTAINS -- POS **meeting<sub>ACTUAL,NEG</sub>

In the negated TLINKs, the EVENTs themselves are not negated, but
instead, the temporal relation \textit{itself} is negated. It is quite
possible (and in fact, far more common) to have negated EVENTs occuring
as a part of a POS TLINK. These most often occur as links between
two POS EVENTs, which are specified as NOT having a certain temporal
relation.

:bangbang: *TLINK negation is used only when the temporal relation itself
is negated. It is completely independent from EVENT negation, and
the negation of EVENTs in no way implies negation of the TLINK. NEG
TLINKs are far less common than NEG EVENTs, and should be pondered
carefully before creation.*



### Annotating contextual modality of TLINKs

TLINKs can take the same
contextual modalities as EVENTs: ACT, UNC, HYP, and GEN. These modalities,
as with EVENTs, represent claims about the reality or certainty of
the TLINKs, and are independent of the modalities or certainties of
the EVENTs they claim.

TLINKs are marked as UNC, HYP, or GEN only when the temporal relation
itself is uncertain, hypothetical or generic.


**ACT - Actual**

The first modality for TLINKs is ACTUAL, which is used most of the
time, and is the default option (that need not be specifically marked).
An overwhelming majority of TLINKs are ACTUAL, and are asserted as
true without any hedging or hypotheticality.

All examples in this guideline, unless otherwise marked, represent
ACTUAL TLINKs.


**UNC - Uncertain/Hedged**

TLINKs, like EVENTs, are marked as UNCertain when we can point to
some explicit lexical or phrasal trigger that indicates some degree
of uncertainty about the reality of the temporal relation. These TLINKs
are presented with a sort of tacit claim that they're \textit{probably
real (unlike hypotheticals, which are explicitly irrealis), but where
the author is unsure.

This also includes TLINKs that are mentioned with any sort of hedging.
This hedging can be lexical ("seems", "likely", "suspicious",
"possible", "consistent with", "claims"), or phrasal ("I
suspect that...", "It would seem likely that"). These TLINKs
are strongly implied, but, for safety, liability, or due to lack of
comprehensive evidence, are not stated as fact. As with EVENTs, it
is very important that these uncertain temporal relations be included
as part of the timeline, but be marked so that they can be easily
differentiated from known facts.

- He likely **escaped** on the *18th* during a *guard change*,
although authorities cannot be sure. \a. *18th* CONTAINS **guard
change** <ACTUAL> 
> **guard change** CONTAINS **escaped**
<UNCERTAIN>

- The chairman will, in all likelihood, **step** down on *Monday*.
\a. *Monday* CONTAINS **step** <UNCERTAIN>

- We have every reason to expect that her incision will **heal**
before her **tournament**. \a. **heal** BEFORE **tournament**
<UNCERTAIN>

- The **fire**, very likely caused by a lightning **strike**,
is **growing** due to high **winds**. \a. **strike** BEFORE/CAUSE
**fire** <UNCERTAIN> 
> **winds** OVERLAP/CAUSE **growing**
<ACTUAL> 
> **strike** BEFORE **growing** <ACTUAL>


**HYP - Hypothetical**

The third modality for TLINKs is HYP. This is useful when annotating
theories, future possibilities, or other hypothetical temporal relations.
Again, this is unrelated to the modality of the EVENTs, and is only
when the temporal relation itself is hypothetical, theoretical, or
otherwise dependent on an external factor.

- Her **surgery** may take place on the *18th*. \a. *18th\
CONTAINS **surgery** <HYPOTHETICAL>

- If the **explosion** was caused by a natural gas **leak**,
the insurance will not **cover** the **reconstruction**. \a.
**leak** BEFORE/CAUSE **explosion** <HYPOTHETICAL> 
> **explosion**
BEFORE/PRECONDITIONS **reconstruction** <ACTUAL>

- Obama's **visit**, if **it** occurs on a *weekday*, is
expected to cause traffic **headaches**. \a. **it** OVERLAPS/CAUSE
**headaches** <HYPOTHETICAL> 
> *weekday* CONTAINS **it**
<HYPOTHETICAL>

Great caution must be exercised before marking a relation itself as
HYPOTHETICAL, as hypothetical EVENTs are not necessarily members of
hypothetical relations. See the below example:

- If the group **attacks** during the **Olympics**, Russia
has promised swift **retaliations**. \a. **Olympics**$_{\text{ACT}}$
CONTAINS **attacks**$_{\text{HYP}}$ <HYPOTHETICAL> \a. **attacks**$_{\text{HYP}}$
BEFORE/CAUSE **retaliation**$_{\text{HYP}}$ <ACTUAL>

In this example, we have a hypothetical attack, an actual Olympic
games, and a hypothetical retaliation. The timing of the attack is
hypothetical, but the causation of retaliation is certain.

As with EVENTs, polarity and modality of TLINKs do not interact.


**GEN - Generic**

GENERIC is our fourth contextual modality, and is used for TLINKs
which may be mentioned in a document, but are only mentioned in a
general sense, and do not appear on the timeline of the overall document.
These usually occur to provide background or information, or as generalized
information when no specific information is yet available.

Generic temporal information (which is true in any document) is marked
with GENERIC:

- **Attacks** in the region generally don't occur on *Holy
days* \a. *Holy days* CONTAINS **attacks**$_{\text{NEG}}$ <GENERIC>

- US Presidential **Elections** are held on the *Tuesday after
the first Monday in November* \a. *Tuesday after the first Monday
in November* CONTAINS **Elections** <GENERIC>

... but remember that specific mentions do not get <GENERIC>:

- The last US Presidential **Election** was held on *November
4th, 2008* \a. *November 4th, 2008* CONTAINS **Election** <ACTUAL>

:bangbang: *As with TLINK polarity, TLINK modality is seldom anything
but the default, ACTUAL. If you are considering marking a TLINK with
UNC, HYP or GEN, double-check to make sure that it is the temporal
relation itself which is uncertain, hypothetical, or generic, rather
than just the EVENTs within it.*



##Causation and Precondition Annotation

In our schema, we want to be able to understand not just the relative
orderings of different EVENTs, but to also annotate when one event
*causes* or *preconditions* another event.

At first glance, it may seem like an odd choice to mark causation
and preconditioning as a subtype of temporal link rather than as a
link of its own. However, causation and preconditioning are inherently
temporal: a precondition necessarily must occur BEFORE the EVENT which
it has preconditioned. In case of causation, the cause will start
BEFORE the effect in the vast majority of cases, but the cause and
the effect can eventually OVERLAP, like running and sweating. Nevertheless,
CAUSE indicates that the cause started BEFORE the effect, and thus,
for causation and preconditioning, there is always a temporal relation
involved.

So, rather than forcing annotators to first decide on the temporal
relations between two events and then make a separate annotation indicating
causality, we simply merge the two tasks: the annotator must decide
whether the pair is in any causal relationship, and if so, they are
necessarily also in a BEFORE or OVERLAP relationship. Thus, we can
save a step in annotation, and simplify the mental task of classifying
these EVENT-EVENT relations.

So, depending on the temporal and causal relation between the two
EVENTs, we use three annotation types for causally linked EVENTS:
BEFORE/CAUSES, OVERLAP/CAUSES, and BEFORE/PRECONDITIONS.


### Distinguishing "Cause" from "Precondition"

In our view of causality, we claim that "X CAUSES Y" if (and only
if), according to the writer, the particular EVENT Y was inevitable
given the particular EVENT X. Put differently, the existence of X
was not just helpful in allowing Y to happen, nor associated with
Y, but the occurrence of X triggered or immediately necessitated the
occurrence of Y:

- The **rockfall** made the **over-full** **dam** **burst**,
**flooding** the **town** below. \a. **rockfall** BEFORE/CAUSES
**burst** 
> **burst** BEFORE/CAUSES **flooding**

Here, the rockfall is what immediately caused the burst (although
the over-full nature of the dam may have preconditioned it), just
as the burst caused the flooding. Put differently, had the rocks not
fallen, and had the dam not burst, according to the author, there
would have been neither bursting nor flooding.

- The **sheriff** **fired** **her** **gun**, **killing**
the **injured** **deer**. \a. **fired** BEFORE/CAUSES **killing**

> **sheriff** IDENTICAL **her**

Here, although the injury may have eventually led to the deer's demise,
the killing was caused directly and immediately by the firing of the
gun.

- **Christchurch**, the first **city** **established** in
**New Zealand**, had endured a **series** of **earthquakes**
that **destroyed** **its** **infrastructure**, **homes** and
**communities**. 
> **earthquakes** OVERLAP/CAUSES **destroyed** 
> Coreference relations: **Christchurch** APPOSITIVE **city**
>  **Christchurch** IDENTICAL **its**
> WHOLE **New Zealand**: PART **Christchurch** 
> WHOLE **its**: PARTs **infrastructure**, **homes**, **communities**
> SET **series**: MEMBER **earthquakes**

In that last example, it is the case that the destruction would not have happened
without the earthquake, and that once the earthquake began (and through
its duration, hence OVERLAP/CAUSES), the destruction was inevitable.

- Although **it** took *many years*, the **discovery** of
**Uranium** outside **Moab** would eventually **revitalize**
the local **economy**. 
**discovery** BEFORE/CAUSE **revitalize** 
**it** IDENTICAL **revitalize**

This shows an example where, although there was significant time
lag between the cause (the discovery of Uranium and the effect: revitalization),
we are led to believe that in this case, the discovery did directly
and inevitably trigger revitalization, and therefore, the link is
causal.

So, again, causality is marked in our schema only if EVENT Y was inevitable
given this particular instance of EVENT X.

Preconditioning, in our view of the world, carries no such inevitability.
In RED, we annotate "X PRECONDITIONS Y" if, according to the writer,
had the particular EVENT X not happened, the particular EVENT Y would
not have been able to happen. Put differently, although a preconditioning
EVENT is not *sufficient* to cause another EVENT, its occurrence
is *necessary* in order for the other EVENT to have happened.

- The **rockfall** made the **over-full** **dam** **burst**,
**flooding** the **town** below. \a. **rockfall** BEFORE/CAUSES
**burst** 
> **burst** BEFORE/CAUSES **flooding** \b{.
***over-full** BEFORE/PRECONDITIONS **burst**

Here, we are led to believe that the over-full nature of the dam helped
promote bursting, and thus, was a precondition of the burst itself.
However, the over-fullness of the dam alone, in this particular case,
was not enough to cause the burst, thus, is only a precondition.

- The **sheriff** **loaded** **her** **rifle**, then **fired**
at the **target**. \a. **loaded** BEFORE/PRECONDITION **fired**

> **sheriff** IDENTICAL **her**

Were the rifle not loaded, it could not have fired, and therefore,
loading is a precondition to firing (although the firing is separately
caused).

- The **strikes** came in **retaliation** for recent terrorist
**attacks**. \a. **attacks** BEFORE/PRECONDITIONS **retaliation**

> **strikes** IDENTICAL **retaliation**

In \Last, although something else (a pilot pushing a button, or a
general's orders) was the direct cause of the strikes, we are told
(via the meaning of "retaliation") that the strikes would not
have happened were it not for the attacks.

Similarly, note that occaisionally an ongoing state can be a motivation
or other precondition for an action; in those cases, you can use OVERLAP/PRECONDITION:

- I feel that they are **punishing** him for his **condition**
by keeping him after school, \a. **condition** OVERLAP/PRECONDITIONS
**punishing**

Remember as well that SUBEVENT, CAUSES, and PRECONDITIONS relations
are mutually exclusive, and one event pair can only have one of these
relations. Therefore, if an event pair has more than one of these
three relations, there is an order of importance.
If the relation is clearly some sort of outcome or causation (cause
or precondition) of an event, then default to the CAUSES or PRECONDITIONS
reading, as they are easier to consistently capture. If torn between
CAUSES and PRECONDITIONS, check the special cases
section to see if there are special hints for your phenomenon, and
otherwise default to CAUSES.

To sum up, CAUSES implies that the occurrence of one EVENT is *sufficient*
to trigger another, whereas PRECONDITIONS only states one EVENT was
*necessary* for another to later take place.

Once this distinction is fully understood, proper annotation is simply
a matter of understanding the temporal nature of each, and creating
the proper annotations.


#### Causality Annotation Rules and Regulations

Because causality is a difficult concept, easy to over- or under-apply,
we do have some specific guidelines below which you should use to
guide your annotation of BEFORE/CAUSES, OVERLAP/CAUSES, and BEFORE/PRECONDITIONS,
referred to collectively below as "Causal links" or "Causal
annotations":



#### Causation relations to ENTITIES with implicit EVENTS must reference the EVENT

Remembeer that if an inanimate object is described as a cause/effect/precondition,
we are marking it as a IMPLICIT EVENT, so that it can be linked:

- The **drug** **raised** **her** **blood** **pressure**.
> **drug** OVERLAPS/CAUSES **raised**

Here, the administration or the chemical effects of the the drug are
causing the raise, rather than the drug itself. Thus, we can mark
the drug as IMPLICIT.  

However, when events that are also entities do agentive, entity-like things, that agency does NOT count as causation

- The **Olympics** **demands** infrastructure improvements of the host country
> Do **not** link "Olympics" and "demand" causally.

Similarly, verbs that create entities like "dinner" should not be construed as causing the event involved:

- **Kevin** **cooked** Thanksgiving **Dinner**. 
> **cooked** BEFORE **dinner**



#### Sources of information are generally not part of a causal chain

Many times, it is theoretically possible to think of a chain of events as being mediated by all of the sources of information involved.   For example, in the example sentence below, it the departure caused by the "cheating" or by the finding out?

- John found out that Bill was cheating, and left.

Similarly one might ask whether the sending of troops in the next example is caused by atrocities, or the revelation of atrocities:

- "recent revelations of atrocities in the region caused the president to send in troops"

For the sake of consistency and sanity, we will attempt to link between actual events (rather than sources of information or reports) whenever possible.  You can generally assume that the complexities added by the sources of information are approximated by REPORTING relations, rather than trying to capture their impact using causal relations.  

Similarly, do not get into the causal relationships between communication and knowledge/revelation, such as:

- **Obama's** **statement** **revealed** the **extent**
of the **drone** **program**.

Here, the statement does not CAUSE revelation (nor does the revelation CAUSE the extent).  

:bangbang: *These rules are mainly to rule out unnecessary causal chains, where event A causes report B and report B causes event C.  However, sometimes (particularly with false reports, etc.), one simply cannot remove the claims from that equation, as the original event did not happen (as in "Bush's revelations of WMDs got us into Iraq") and the chain of causation really boils down to the report.  You can use causal links in this kind of exceptional circumstance.*


#### Assume the writer of the text is reliable

For quoted speech or reporting, assume that the narrator or writer
is reliable, unless otherwise indicated:

- On *Sunday*, he **said**, **one** of the **bombs** **wrecked**
the family's home. \a. **one** OVERLAPS/CAUSES **wrecked** \b{.
*Sunday* CONTAINS **wrecked** 
> **bombs** SET/MEMBER **one**

- **Frank** **claims** that an **alien** mind-control **beam**
made **him** **rob** the **bank**. \a. **beam** OVERLAP/CAUSES
**rob** 
> **Frank** IDENTICAL **him** 
> **claims**
REPORTING **beam**

Remember, you are not a jury, and it is not your role to determine
the accuracy of asserted causal claims, but to simply annotate them.


#### Causal links can cross sentence boundaries

As with other forms of TLINK, CAUSES/PRECONDITIONS links can cross
sentence boundaries, where necessary:

- She **said** the **bombs** **rained** down on them for
two days. The children are **terrified** as a result, she **said**.
\a. **rained** BEFORE/CAUSES **terrified**

However, EVENTs that are too far apart (crossing multiple sentence
boundaries) should not be linked to each other, as there is likely
no way to determine causation besides human inference:

- A terrorist group has **claimed** responsibility for the suspect
packages. (...) The group **formed** just before the London **Olympics**
in 2012. \a. **formed** BEFORE **Olympics** 
> Do not annotate
as **formed** BEFORE/PRECONDITIONS **claimed**




#### Causation and Precondition TLINK Use

If, even after evaluating the EVENTs in light of the regulations above,
you belive there to be a markable causal relationship, you must choose
among the three causal annotation types.


#### BEFORE/PRECONDITIONS

As such, if you understand two EVENTs to have a relationship of preconditioning,
your sole choice is to create a BEFORE/PRECONDITIONS link.

- **She** **unlocked** the **vault**, **disabled** the
**cameras**, and **distracted** the **guard** so that **he**
could **steal** the **gold**. \a. **unlocked** BEFORE/PRECONDITIONS
**steal** 
> **disabled** BEFORE/PRECONDITIONS **steal**

> **distracted** BEFORE/PRECONDITIONS **steal**

Because preconditions are defined as EVENTs which must have happened
in order for a later EVENT to happen, temporally speaking, all PRECONDITIONS
must start BEFORE the EVENT which they precondition.


#### BEFORE/CAUSES

If the relation between two EVENTs is causal, that is, that one EVENT
\textit{necessarily} causes the other, you must evaluate its temporality.

In many cases, the causing EVENT will have ended before the effect
fully takes place. In these cases, BEFORE/CAUSE is the only prudent
annotation.

- The **bear's** **visit** forced the **city** to **adopt**
a new **trash-can** **design**. \a. **visit** BEFORE/CAUSE
**adopt**

It is clearly the case that the adoption did not happen while the
bear was still in town, so the cause is BEFORE the effect, and BEFORE/CAUSE
is prudent.

- **France's** **declaration** caused **tension** with **Russia**.
\a. **declaration** BEFORE/CAUSE **tension**

The declaration did not, itself, cause tension with Russia in the
same way that an earthquake causes damage. Instead, its interpretation
and analysis by the Russians caused the tension. This means that there
was a non-trivial lag between cause and effect, and that BEFORE/CAUSE
is prudent.

- **Switching** **textbooks** led to **improvements** in
**scores**. \a. **switching** BEFORE/CAUSE **improvements**

Again, it is not the case that the improvement occurred \textit{during
the switch, so BEFORE/CAUSE is prudent.

- **He** **shot** and **killed** the **attacking** **soldier**.
\a. **shot** BEFORE/CAUSE **killed**

**shot** here refers to the act of discharging a firearm. Even assuming
an immediate and painless death for the attacker, there is a (very
small) lag between the discharge and the death. Put differently, it
is not the case that at any point, this specific shot and killing
were occuring at the same moment. So, BEFORE/CAUSE.

- The **bus** **kneeled** to allow **access** to the elderly
**man**. \a. **kneeled** BEFORE/CAUSE **access**

Although kneeling has a non-trivial duration, we have no reason to
believe that the elderly man entered the bus mid-kneel. Thus, BEFORE/CAUSE.

So, if it is the case that the causing EVENT ended before (even if
milliseconds before) the EVENT it caused, BEFORE/CAUSE is the only
prudent choice.


#### OVERLAP/CAUSES

OVERLAP/CAUSES is intended for those cause/effect pairs where the
cause, during its inherent duration, is continuously or periodically
resulting in the effect. Put differently, there is a temporal overlap,
where the cause is ongoing, and the effect is already partly or completely
present.

- The **earthquake** **destroyed** the **palace**. \a.
**earthquake** OVERLAP/CAUSES **destroyed**

At some point in time, the destruction had begun while the earth was
still quaking, and thus, the two EVENTs are in an OVERLAP/CAUSES relationship.

- **His** **coldness** made **Kerri** **uncomfortable**.
\a. **coldness** OVERLAP/CAUSES **uncomfortable**

Her discomfort and his coldness are both durative EVENTs, and it is
extremely likely that she began feeling discomfort before his coldness
had ended. Thus, OVERLAP/CAUSES.

- The **attacks** resulted in 89 **deaths**. \a. **attacks**
OVERLAP/CAUSES **deaths**

It's likely that deaths occurred during each individual attack, and
when taken as a plural sum, it is certain that the span of the "attacks"
contains at least one death.

Note that the semantics of participating EVENTs have a strong role
in the choice of BEFORE/CAUSES vs. OVERLAP/CAUSES. For instance:

- The **explosion** caused mass **hysteria**. \a. **explosion**
BEFORE/CAUSE **hysteria**

Here, it's fairly clear that the hysteria began after the explosion,
rather than the physical blast causing the hysteria as it propagated.
Compare to:

- The **explosion** caused many **injuries**. \a. **explosion**
OVERLAP/CAUSE **injuries**

Here, the blast itself, the physical reality of the expanding gas
and debris, caused injuries. Although other injuries may have occurred
after the explosion (due to trampling in the evacuating crowd, or
collapse of damaged structures), it is still the case that some of
the injuries occurred while the explosion was in progress.

Finally, remember that OVERLAP/CAUSES does NOT imply that the effect
is contained within the span of the cause. Take, for example, the
temporal relationship between an earthquake, and the destruction it
causes. It is certain that some destruction, if not the majority,
occurs while the earthquake itself is ongoing, that is, the ground
is still shaking. However, in any earthquake, there is damage which
occurs well after the shaking has stopped, whether by subsequent collapse
of weakened structures, fires, looting, or any of the myriad other
things which can go wrong.

So, although the earthquake OVERLAPs a non-trivial part of the destruction,
it is BEFORE other destruction. In these cases, remember that OVERLAP
means only that there is an overlap, and that in situations like the
earthquake described above here, OVERLAP is accurate, while BEFORE
is not. Thus, when a cause is both BEFORE and OVERLAPping the effect,
OVERLAP should be used.

:bangbang: *If you find yourself attempting
to justify OVERLAP/CAUSES by saying "Well, there was probably a
few milliseconds of hysteria which started before the end of the bomb's
explosion..." or "Maybe he was injured slightly by the shockwave
ahead of the sub-sonic bullet which hadn't yet left the barrel, thus,
during the **shot**...", stop. OVERLAP/CAUSES is intended for
those causal EVENTs which are durative and causing an effect throughout
their duration, rather than for those with coincidental or miniscule
overlap between cause and effect. These annotations will be difficult
enough without adding this additional agony.*


#### ALINKs trump causation

Do not create CAUSES/PRECONDITIONS links between the source (e.g.
*started* and the target (e.g. *attacking*) of ALINKs:

- The **terrorists** **started** **attacking**. 
> ALINK: **started** INITIATES **attacking**

Although it is tempting to claim that the start of the attack causes
the attack, it's somewhat tautological, and completely useless to
us. Similarly:

- **We** will **restart** the **investigation** after the
**holiday**. 
> ALINK: **restart** REINITIATES **investigation**

The investigation has already been caused by something else, and its
reinitiation is in no way causal.

Note that ASPECTUAL events can CAUSE or PRECONDITION other EVENTs
which are not the target of the associated ALINK:

- Several months after **quitting** **smoking**, his **singing**
got so much **better**.
> **quitting** BEFORE/CAUSES **better**
> ALINK: **quitting** TERMINATES **smoking**




## Event Coreference

While linking up events in terms of their temporal, causal and subevent
structure, you will also be marking them for event coreference. These
guidelines for coreference annotation have been adapted from the OntoNotes
v. 7.0 (\cite{pradhan2007ontonotes}) and ODIE (2010) guidelines as
needed to accommodate the objectives of the RED schema. Additional
concepts and information were synthesized from Poesio et al. 2004
(\cite{poesio2004centering}), Poesio 1997 (\cite{poesio1997conversational}),
and Savova et al. 2011 (\cite{savova2011anaphoric}).


### IDENTITY

Two events have an IDENTICAL relation if they refer to the same event
in space and time. The IDENTICAL relation has several important semantic
characteristics(Following the MUC-7 specifications):
 
- The relation is symmetrical, i.e., non-directional: (if A is IDENT
to B, then B is IDENT to A). This is different from relations like
WHOLE/PART and SET/MEMBER, which are directional by defition. 
- It is also transitive: if A is IDENT to B and B is IDENT to C, then
A is IDENT to C. . 

### SET-MEMBER

A SET-MEMBER relationship exists when one event can be thought of
as being an instane of a larger set of events. In annotating this
over events, you are to decide between SET-MEMBER and CONTAINS-SUBEVENT.
You should remember to use CONTAINS-SUBEVENT for all cases in which
an event is temporally within, and part of the script of, a larger
event. 

SET-MEMBER can occur between multiple ACTUAL events when the SET is
an actual agglomeration of instances that are not a temporally continguous
unit, as in \Next 

- A series of **earthquakes**$_{S}$ struck the province of
Manokwari last Tuesday. The largest **earthquake**$_{M}$ alone
caused \$73 million in damage.

Other SET/MEMBER relations will be between generalizations and their
instances
\begin{examples
- Presidents usually **\textsubscript{SET} pardon** a turkey for
Thanksgiving, and today the lucky convict he **\textsubscript{MEMBER
pardoned** was named Ginny Fawell. 
\end{examples

### BRIDGING

As with entities, if you are unable to use one of the previously discussed
links, but it is apparent that some sort of coreference link exists
which entails that the events have some sort of link, then use the
BRIDGING relation. For dealing with EVENT coreference, an important
option that this opens up is when a text alledges that doing one event
is analogous to doing another, either directly or in an attempt at
metaphor:
\begin{examples
- John **\textsubscript{head} voted** to make waffles the state food,
which **\textsubscript{attribute} amounts** to betraying all his
campagin promises.
\end{examples
Because we define CONTAINS-SUBEVENT as involving temporal containment,
you may also use BRIDGING for any subevent which seemed to be "part
of", yet temporally outside of, another event.

- After a week of attempted repairs, the palace **collapsed**
Friday, the most disheartening part of the already-terrible **earthquake**.
\a. **earthquake** BEFORE-CAUSE **collapsed** 
> **earthquake**
BRIDGING **collapsed**


### General Guidelines for Annotating Coreference



#### Never link EVENTs to ENTITIES

In all coreference relations (IDENTICAL, APPOSITIVE, WHOLE/PART, AND
SET-MEMBER), Entities can be linked to Entities, and Events can be
link to Events, but Entities and Events will never be linked within
the same coreference relation. If you encounter an occasion where
you are tempted to do this, check that your Entity is not actually
an Event, or that your Event is not actually an Entity, as the case
may be.


#### SET/MEMBER, and BRIDGING relations are inherited by IDENT
chains

If you have an IDENT chain represented by A-A-A-A-A, and A participates
as the PART in a WHOLE/PART relation or as the MEMBER in a SET/MEMBER
relation, conceptually, all mentions of A are PARTs of the WHOLE or
MEMBERs of the SET, too. You do not need to include every mention
of A as a PART of the WHOLE or as a MEMBER of the SET. Only the most
recent mention of A ought to be included in the relation. The other
mentions will be connected to their place as a PART or a MEMBER through
spider-webbing.


#### Bridging relations are re-created for subsequent mentions

In bridging relations (i.e. WHOLE/PART, SET/MEMBER), any new mention
of the WHOLE (or the SET) that is followed by mentions of the PARTs
(or the MEMBERs) merits a new relation. For example, consider the
relations in the following:

- **I**$_{M1}$ met with the **patient**$_{M2}$ today. **We**$_{S1}$
discussed treatment options for **her**$_{M2-1}$ cancer. **We**
also reviewed in **our**$_{S2}$ discussion the results of **her**$_{M2-2}$
recent CT-scan. **My**$_{M1}$ recommendation is adjuvant chemotherapy.
\a. SET **We**$_{S1}$: MEMBERs **I**$_{M1}$, **patient**$_{M2}$,
**her**$_{M2-1}$ 
> SET **our**$_{S2}$: MEMBERs **her**$_{M2-2}$,
**My**$_{M1}$

In this example, **I**$_{M1}$ and **My**$_{M1}$ are IDENTICAL;
**patient**$_{M2}$, **her**$_{M2-1}$, and **her**$_{M2-2}$
are IDENTICAL; and **We**$_{S1}$, **We**, and **our**$_{S2}$
are IDENTICAL.


#### Don't link ACTUAL and GENERIC events (use SET/MEMBER or BRIDGING)

In analogy with the principle for not TLINKing HYP/GEN to ACT/UNCERTAIN
events, ACTUAL and GENERIC items can never be in an IDENTICAL, APPOSITIVE,
or WHOLE/PART relationship. They can, however, be SET/MEMBER, as in
\Next:

- **I** discussed with **Mrs. Ambry**<sub>ACTUAL</sub> the results
of a local clinical trial in which **patients**$_{GENERIC}$ with
**cancer**$_{GENERIC}$ recovered successfully on the **drug**
without reoccurrence. Given **her** colon **cancer**<sub>ACTUAL</sub>
and the success of the **drug**, **I** recommend **it**. \a.
SET **patients**: MEMBER **Mrs. Ambry** 
> **Mrs. Ambry**
IDENTICAL **her** 
> SET **cancer**$_{GENERIC}$: MEMBER **cancer**<sub>ACTUAL</sub>

> **I** IDENTICAL **I** \e. **drug** IDENTICAL **drug**,
**it**


## Aspectual Link Annotation

The next annotation performed on the data is the ALINK (or "aspectual
link") annotation. ALINKs are created between an aspectual EVENT
and a non-aspectual EVENT. Any EVENT previously marked with the class
ASPECTUAL will be ALINKed to another, non-aspectual event, and you
will never make an ALINK which includes a TIMEX3 or two non-aspectual
EVENTS. ALINKs only occur when you have an aspectual EVENT, and are
much less common in the text than TLINK annotations. Relatively few
EVENTs will have an associated ALINK.

As with TLINKs, they are created interactively, and have the basic
form:

- EVENT1 **aspectual relation** EVENT2

But unlike TLINKs, no matter the circumstance, an ALINK should never
cross a sentence boundary.


### ALINK sub-types

There are four different aspectual relations used in the schema, CONTINUES,
INITIATES, REINITIATES, and TERMINATES.


**CONTINUES**

CONTINUES is used when an aspectual event shows the continuation of
another event:

- We **continue** to **fight** tyranny in all its forms. \a.
**continue** CONTINUES **fight**

- The rebels have announced that they will **keep** **pressing**
towards Damascus. \a. **keep** CONTINUES **pressing**

- The patient will **remain** on **dialysis** until her condition
**changes**. \a. **remain** CONTINUES **dialysis** 
> **remain**
ENDS-ON **changes**

- She is not interested in pursuing chemotherapy at this time
but is interested in **continued** **surveillance**. \a. **continued**
CONTINUES **surveillance**

- We will **continue** to **monitor** heart rate and rhythm
along with serial cardiac markers and electrocardiograms to rule her
out for any cardiac involvement. \a. **continue** CONTINUES **monitor**

**INITIATES**

INITIATES is used when an aspectual event indicates the start or initiation
of another event:

- *2008* marked the **start** of the rebels' brutal **campaign**.
\a. **start** BEGINS-ON *2008* 
> **start** INITIATES **campaign**

- Patient will **begin** a high-fiber **diet** upon **release**.
\a. **begin** INITIATES **diet** 
> **begin** BEGINS-ON
**release**

- We will **start** Ms. Miller on a normal saline **infusion**
at 75 an hour for a total of 1 L. \a. **start** INITIATES **infusion**

Note that INITIATES carries an implied sort of causality (beginning
something, by definition, causes it to start). This causality need
not be marked, so long as the ALINK is present.


**REINITIATES**

REINITIATES is used when an aspectual event indicates that another
event will be restarted or reinitiated:

- The latest **bombing** broke the treaty, **resurrecting**
**violence** throughout the city. \a. **resurrecting** REINITIATES
**violence**

- **Levaquin** 750 mg p.o. q. day (will **restart** *today*)
\a. **restart** REINITIATES **Levaquin** 
> *today* CONTAINS
**restart**

- His anterior chest **rash** has not **reoccurred** since
the **PCN** VK was **discontinued** *24-hours ago*.
>  **discontinued** TERMINATES **PCN** 
> **discontinued** BEFORE **reoccurred**<sub>NEG</sub>

> **discontinued** OVERLAP *24-hours ago\

As with INITIATES, reinitiates carries an implied sort of causality.
This causality need not be marked, so long as the ALINK is present.


**TERMINATES**

TERMINATES is used when an aspectual event indicates the ending of
another event:

- The latest **treaty** should finally **end** the **bloodshed**.
\a. **end** TERMINATES **bloodshed**

- Because of this **reaction**, **Allegra** will be **discontinued**.
\a. **discontinued** TERMINATES **Allegra**

- We will **hold** her **heparin** until after the **surgery**.
\a. **hold** TERMINATES **heparin** 
> **hold** ENDS-ON
**surgery**

- Patient **nausea** was successfully **stopped** by 1-mg
**Ativan** p.r.n. \a. **stopped** TERMINATES **nausea**

:bangbang: *ALINKs are much less common than TLINKs, usually only a few
per document, but they are no less important and easy to overlook.
Remember that any time you have an EVENT which has the type ASPECTUAL,
you will need to create at least one ALINK.*


## REP - Reporting Annotation

Reporting Annotations link EVIDENTIAL EVENTs to those EVENTs that
they report. For instance:

- A Kurdish newspaper **said**$_{R}$ Wednesday that Iraqi members
of an Al Qaeda- linked group, a Kurd and an Arab, **blew**$_{E}$
themselves up in northern Iraq on February 1, **killing**$_{E}$
at least 105 people.

- The newspaper **added**$_{R}$ that bin Mahmud is the brother
of a man whose alias is Abdullah Al-Shami, an Ansar al-Islam leader
who was **killed**$_{E}$ last year while **fighting**$_{E}$
a US-backed **onslaught**$_{E}$ by the PUK that **forced**$_{E}$
the group out of its enclave near the Iranian border at the end of
March last year.

Here, we are linking the Report itself with the Event that was reported.
The EVENTs that can serve as a Report appear to be a restricted class,
mostly the verbs "say", "tell", and "report", and will
always be an EVENT of the type EVI. The events serving as Event, what
was being reported, are restricted to only the EVENTs in the remainder
of the sentence, unless we have some explicit rationale we can point
to that the report does not cover an in-sentence event, or that the
report continues outside the sentence boundary. In the latter case,
it should only be for cases of direct quotations including multiple
sentences.

- Mr. Jones **said**$_{R}$, "I'm not **sure**$_{E}$ when
our company will go **public**$_{E}$. It will not be before we
**acquire**$_{E}$ Vandelay Industries.\textquotedbl{

If there are multiple EVENTs reported by the same EVI event, as in
the examples above, only one REPORTING link will be created, with
all of the reported events linked to the same EVI event in the same
relation.


# Appendix

## Edge Case Guides

### Hard Cases in EVENT vs ENTITY distinctions

| Type | example | treatment | see
| ---- | ------- | --------- | ----
| communications | I finished an article for submission | EVENT - make these eventive when can be paraphrased with write/read/send  | 
| communications | This [article] is part of TIMES EXPRESS. | just an ENTITY, does not imply an event  | 


### Hard Cases when determining Markablability

| Type | example | treatment | see
| ---- | ------- | --------- | ----
| marking participation | his **role** in **helping** to... | "role" is not an event | 
| aspectual pre-nominals | The **renewed** **investigation** of Morsi | "renewed" is an event because it gets an ALINK | 
| event as its goal | for assault, not ** attempted** **murder** | make BOTH events, "murder" is neg, "attempt" actual | 
| mentions of time periods | he spent a brief period in the US | make period's phrase a TIMEX | 
| mention of time periods with semantic content | john finished his probation period | these can be EVENT | 


### Complex Predicates

| Type | example |  two events? | markable features   | relation? |
| ---- | --- | --- | --- | --- |
| denial of a fact  | the mayor denies any involvement with the cartels | yes | make second event UNCERTAIN/HEDGED | no relation |
| denial, which it means "prevent"  | the troops denied the protestors entry to the square | yes | make second event NEG-ACTUAL | no relation |
| denouncement  | The international community was quick to **denounce** the **bombing** | yes | make second event ACTUAL (unless other cues say otherwise) | no relation |
| endorsement  |  Three different countries have **endorsed** the trade **agreement**. | yes | no effect -- likely ACTUAL for e2 | no relation (unless endorsement/support enacts the endorsed thing) |
| light verbs | John **took** a **bath** | no, only BATH |  | |
| light verbs | The burglar **committed** a heinous **crime** | no, only **crime** |  | |
| reporting  | NYT first reported the strike in october | yes | make second event ACTUAL unless reporting verb marks doubt | REPORTING |
| reporting, absence of  | and the right hilar lesions were not **reported** as being **prominent**.  | yes | make second event UNCERTAIN/HEDGED if the absence of a report implies any doubt about its occurence  | no relation |
| request | The Syrian rebels have repeatedly **requested** international **aid** | yes | default to HYPOTHETICAL for e2 |  one of the two PRECONDITION relations |
| revealing/showing  | examination shows a decreased pulse | yes | make second event ACTUAL unless reporting verb marks doubt | REPORTING |
| seeming  | John seems to like chocolate | no | can be a hedge, and justification for marking UNCERTAIN/HEDGED | no relation |
| support verbs | After ~~undergoing~~ extensive **transformation**... | no, just **transformation** | | |
| support verbs | at that time, he ~~experienced~~  **discomfort**... | no, just **discomfort** | | |
| support verbs | The **earthquake** ~~struck~~ during the parade | no strike, just **earthquake** | | |
| usage of objects |  Police **used** tear ~~gas~~ to disperse the ... | just "used" (but "gas" is an entity) | | |
| willingness | He is **willing** to **meet** with our Pauahi Wing Queens Hospital. | yes | default to HYPOTHETICAL for e2 | one of the two PRECONDITION relations |



### Distinguishing Reporting events from Hedges

Remember that hedges are NOT events, but merely good evidence for using UNCERTAIN/HEDGED on the events they modify

| Reporting, Hedging or Separate Event? | type | example |  Reasoning |
| ---- | --- | --- |
| I [found] it difficult to put down
| Separate Event | denial  | the mayor denies any involvement with the cartels |  |
| Reporting | revealing/showing  | examination shows a decreased pulse |  |
| Reporting | actual reporting  | NYT first reported the strike in october | |
| Reporting | prepositional reporting | **according to* John, they closed in February | | 
| Reporting AND evidence for UNCERTAIN/HEDGED | reporting verbs that imply doubt | North Korea claims that they can hit NYC | see [Examples of reporting verbs implying uncertain/hedged](#Rules for Reporting verbs implying uncertain/hedged)





## Allowable explicit grammatical evidence

### Permissable Evidence for BEFORE/OVERLAP

| Context | Example |
| ------- | ------- | 
| Event has "have been Xing" or present tense "has" |  I have been doing yoga for years |
| |  The fires have been burning for eight days |
| |  He has felt good. |
| There seems to be grammatical implication that the event is ongoing, and past-tense aspectual INITIATES verb exists that you will ALINK to | this *kicked off* what may be a long court *proceeding* |
| event is explicitly/grammatically ongoing, and also has a link to a TIMEX3 before document time. | He has cancer, first noted in 1996 | 
| The event is modified by the temporal use of "still" or "yet" | He still drive that old Ford he had in college. | 
| Modified by an aspectual verbs that will have the aspectual link CONTINUES | That reporter keeps on investigating tobacco companies | 

One context that is *not* valid evidence for BEFORE/OVERLAP (being somewhat slippery to pin down) is that of indirect speech acts.  While many would infer from the following example that the bankruptcy was true both today and yesterday, we cannot actually infer that from the sentence:

> - The boss said yesterday that we are bankrupt$_{\text{OVERLAP}}$.



### Rules for Reporting verbs implying uncertain/hedged

- The following verbs should probably imply UNCERTAIN/HEDGED: allege/allegation, accuse/accusation
- The following verbs might seem to imply uncertainty, but aren't sufficient for uncertain/hedged: reports that, claims that, according to,... 


### Permissable Evidence for Uncertain/Hedged




# Document Revision History

- 9/22/13 -- Major revisions to add more non-medical examples, remove
material remaining from THYME-TimeML, improve Subevent section 
- 9/17/13 -- Figured out what RED means, added this to the title. 
- 9/12/13 -- Changed title to RED annotation guidelines, removed permanence,
added short discussion of the idea of permanence to the DocTimeRel
section. Added warning to CONTAINS-SUBEVENT which points to BRIDGING
when containment is lacking. - Will 
- 7/24/13 -- Merged the two documents initially 
- 9/19/13 -- Minor terminology revisions. - Kevin 
- 10/16/13 -- Terminology and typos fixed - Kevin \& Mariah 
- 10/25/13 -- Causation marked as Under Construction; Hedged changed
to Uncertain - Kevin and Will 
- 10/27/13 -- Added more discussion to hedging. - Will 
- 2/20/14 -- Causation expanded, clarified, and no longer under construction
- Rei 
- 3/6/14 -- More information, examples, and discussion added to Annotating
Entities and Coreference Annotation. Clarification of how to treat
discussions and quantifying phrases. Elimination of "risk of X-type
guidelines. General revision. - Mariah 
- 7/5/14 -- Accepted all prior tweaks, and began v.1.5, a clarification
for completing the pilot. 
- 7/6/14 -- Implemented Mariah's suggestion for emotive vs. assertive
emphatics. 
- 7/27/14 -- Added `Avoid millisecond reasoning', `hypotheticals, negation
and the past', and a made a few other repairs. - Will
- 4/4/15 -- moved everything to github  - Tim

