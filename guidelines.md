# Richer Event Description (RED) Annotation Guidelines (v.1.6)

Developed by Will Styler, Kevin Crooks, Mariah Hamang, and Tim O'Gorman
as a synthesis of the THYME-TimeML guidelines, the Stanford Event
coreference guidelines and the CMU Event coreference guidelines. These
guidelines have been developed with substantial input from Eduard
Hovy and Teruko Mitamura at Carnegie Mellon University, Rei Ikuta
at the University of Colorado, Boulder, and benefited from the discussion
at the NAACL Events Workshop.

## Introduction

Richer Event Description is an attempt to bring together a number
of existing and well-researched veins intra-sentence annotation into
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
many events, and many relations between them. It is moreover an *adjudicated
task.* This means that each document will be annotated by two people,
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
``meaning'' of the document while doing so consistently,
and that a wide variety of rules and strictures defined below are
designed simply for that purpose.


### Acknowledgements

The project is based on work supported by Award R01LM010090 from the
National Library Of Medicine, and by DARPA FA-8750-13-2-0045, subaward
560215 (via LDC) DEFT: Deep Exploration and Filtering of Text\textquotedbl{}.
The content is solely the responsibility of the authors and does not
necessarily represent the official views of the National Library Of
Medicine, the National Institutes of Health, or the Defense Advanced
Research Projects Agency.


### About the examples in this guide

In our examples, words in *brackets* are to be annotated with
the type of annotation or attribute under discussion. The brackets
represent the proper span. Spans of text in **Curly Brackets** represent
TIMEX3 annotations which are marked, even if not being discussed explicitly
in the example.

In these guidelines, relations will be represented with the below
format:

1. Item A comes before Item B \a. (Item A) BEFORE (Item B)

Where the first line is the actual sentence, Item A is the first EVENT
or TIMEX3, Item B is the second EVENT or TIMEX3, and BEFORE (or CONTAINS,
OVERLAP, etc) is the TYPE of the LINK, described in Section \ref{tlinktypes}.

Also, *brackets* indicate Entities and EVENTs, and **curly brackets\
indicate TIMEX3s.

## Markables and Entity Relations Stage

There are two different kinds of actions done during the first stage
of annotation. One is the annotation of events, entities and times,
differentiating things worth keeping track of from other words in
the text. The other annotation being done is entity relationships
-- coreference, part/whole relations, set/member relations and bridging
relations between entities.

These exist in the same ``stage'' precisely so that the anotation
of both may be done at the same time. When initally learning to annotate,
however, one is encouraged to start by annotating entities and events
first, and then adding entity coreference links. As one gains competence
at the task, you are encouraged to attempt to interleaf these tasks
into a single read through the document; section XXXXXXX details the
``pre-annotation'' which annotators actually will encounter in context,
and discuss how to interact with in. 


### Marking Entities and Events


#### Finding-Entities-and}Finding Entities and Events

The first and most fundamental task in the first stage of annotation
is to label \textsc{event} and \textsc{entity} instances. Conceptually,
you are invited to split up the act of annotating \textsc{event}s
and \textsc{entity}s into two parts -- the first part being the decision
about whether something should be annotated, and the second part being
the decision about what exact span of words you should mark to designate
it. This section focuses only upon that first question. 


##### What is an EVENT

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
such as ``go'', ``seem'', ``have'', etc. -- for example, there
is only one verb in example \ref{Your-dog-see} below:
\begin{examples
- \label{Your-dog-see}Your dog \textbf{seems to have eaten} the cupcakes.
\end{examples
In a more general sense, one can think of that criterion as being
about distinguishing whether a particular mention (like ``have''
or ``seems'' above) constitutes its own event, or merely helps constitute
description of a single event. For example, a light verb like ``take
a bath'' does not constitute a separate ``take'' event and ``bath''
event, but rather combine to jointly signal the bath-taking event. 

A second definitional question emerges with states and properties.
Consider the range of circumstances from XXX to XXXX, in which XX
is very eventive and YYYY very non-eventive:
\begin{examples
- The walls \textbf{yellowed }during the fire.
- We came home to find the door \textbf{opened}.
- We came home to find the door \textbf{open}.
- I own a\textbf{ yellow} canary
\end{examples
Hopefully the reader will agree that the last example is dramatically
less ``eventive'' than the other instances. Yet naturally, all states
\emph{exist} on a timeline, so mere existence on a timeline is not
suffifient for this. Yet the span on the timeline in example XXX is
a speciifc type -- it is an \emph{inherent }property of the entity
in question, and thereofre might be considered to not have any sort
of temporal proeprties separate from the canary itself. 

In general, we will consider a state eventive if it is not inherent
\emph{and }if it has a clear moment of occurrence or emergence. ``I
saw the door was open'' is not simply a state that might not permanently
be true, but a state which elicits the implication of other events. 

```
insert figure here
```


Adjectives used as mere specifiers, to label or refer to particular
people, should be viewed with skepticism in this regard. ``I saw
the door was open'' evokes an act of opening; ``He walked through
the open door'' does not. \emph{This will be one of the difficult
boundary-lines in our annotation task, and one should check with other
annotators whenever possible to build concensus.


##### What is an ENTITY

For ENTITY annotation, we will be going through the text, finding
all instances of things that consistute an ENTITY -- a participant,
location, organization, or other entity that might be tracked in the
discourse. Importantly, while we are doing entity coreference in this
pass (as discussed ion sectio nXXXXXXXXX), that does not mean that
the only entity mentions worth annotating are those in a referential
relationship. Instead, we are using a 

Just like when finding events, you must first decide if there is one
entity being mentioned or many. The part about nouns that makes this
hard are noun phrases like ``The Manokwari Hospital'' in example
\ref{manokwari}, which could be viewed one entity (the hospital )
or two mentions (reference to the hospital and to the town of ``Manokwari''): 

- The Manokwari *Hospital* said that most
of *those* seriously wounded now were treated at an emergency
*unit*7 at the *hospital*.

This will get to a tricky concept; we will talk generally about whether
a term is **referential**. This can be understood in some ways
but looking at why we have it and what we are trying to avoid. On
one hand, we don't want to keep track of every single noun ever mentioned
in a discourse:

- *I* went down the *street* to the local *food* and *drug*
*store* and talked to the *meat* *guy* in *their*
*deli * *section*.

A general way of thinking of this is that we usually don't want to
be keeping track of ``hot dog'' in ``hot dog stand''. Yet the
important issue is that if you were tracking a story about tainted
hot dogs, then knowing whether the ``hot dog'' in a particulra hot
dog stand is part of a set of ``tainted hot dogs'' is an important
part of understanding what the document would be saying. How can we
tell the difference?

Our distinction will be essentially that anything which seems to be
a plausible candidate for reference will be worth marking, and anything
coreferent with a referential thing in the document is *also*
worth marking. In practice, all salient arguments -- direct object,
subjects, etc. -- that represent real entities with the world should
pass this bar. Nouns modifying other nouns, pertainymic adjectives,
etc. will be more tricky:
\begin{examples
- Indian *food* is wonderful \$\textbackslash{}leftarrow\$ is not
introducing ``India'' as a topic of discussion
- The *Indian* *PM* is visiting *DC* \$\textbackslash{}leftarrow\$
many would consider ``India'' accessed here
\end{examples
Some of these will be edge cases which you will learn over time (tune
your instincts at the end of this section). But here are some hard
and fast rules:
\begin{itemize
- If the thing that the words refer to is identical to another mention
in the document that is clearly ``referential'' in this sense above,
then this mention, too, must be treated as referential. *This
is one of the only times that your other annotation decisions should
be factored into current decisions*! 
- Entities that validly have other entity-coreference relations (discussed
below) such as PART-WHOLE or SET-MEMBER are also relevant and should
be annotated. 
- You can almost always assume that a subject or object, *if they
refer to an entity at all*, will be referential. 
\end{itemize
This idea that something must be referring to an entity is important.
If a Verb+Object pair collectively constitute an event -- ``tell
the truth'', ``take a bath'' -- then generally refers to an event
alone. The exception -- complex typing instances like ``run a marathon''
or ``send a text'' in which the event also can be thought of as
an entity -- are covered below. 


#####  Distinguishing EVENT from ENTITY

Certain phenomena have characteristics of both events and entities.
Ongoing processes may often have referential characteristics -- a
revolution, for example, is clearly an event, but during the process
of its occurrence a revolution might take on some characteristics
of a concrete entity (as in \textit{``the revolution has spread to
Misrata''}). Similarly, many diseases might be thought of either
as ongoing processes applying to the body, or as amalgams of symptoms
that have referential status. Such questionable instances will always
default to EVENT.

This pattern of defaulting to EVENTs is particularly strict in our
annotation. Diseases such as ``carcinoma'', although often of long
duration and unclear origin, will always be treated as events rather
than as entities. This is because, when a ``carcinoma'' appears
in a medical record, it is usually to refer to the patient's state
of ``having a carcinoma'', rather than to the cancerous tissue itself,
and this patient's state with regards to carcinonoma merits as much
attention in a medical record as a battle or bomb blast would in a
news report.

Another good test for eventiveness is to check for temporality of
onset or for temporal relation to the document's writing. If you're
unsure, ask ``when did this thing start?'', or perhaps, ``when
did it occur relative to the time of writing?'', and gauge your reaction
to the question, even if you're not sure of the answer.

- The patient came in with a fever. \a. ``When did the fever
start?'' - ``Well, probably in the last few days. Definitely before
this was written.'' \b{.} ``When did the patient start?'' - ???

If such a question does not seem felicitous, or only makes sense by
interpreting it as ``when was this created?'', then the element
in question is probably an ENTITY rather than an EVENT.

However, if you find yourself in a situation where you can answer
both ``when did this happen'' and ``when was it created'', and
those dates are different, you're likely looking at a metonymic event,
discussed below.


##### Complex Types

It is worth emphasizing that is it not the case that the world is
cleanly seperable into events and entities at all times. In an abstracted
level, one might note that if you talk about an official statement
from a public figure, there is an entity (the words being stated or
the text of the statement) and the act of expressing it. If one talks
about a laws, it refers to both a thing in the world -- a set of rules
written down somewhere -- and the complex of what it does to the world.
These kinds of patterns can be viewed as complex types (XXXX Pustejovsky
XXX), having characteristics of both entities and events. 

For most things, we will default to events.  Especially with *statements*, with *messages*, and with 
other ways of packaging information, try to default to treating them as events, and to only use them as
entities when the context specifically depands an entity treatment. For communication events, the contexts for using 
entities should be references to literal stored forms of the communication (such as stored texts, where one's emails live, etc.).  

For laws, contracts and rules, you can treat them as both entities and events. 

##### When is an ENTITY also an EVENT?


It is also worth noting that in some of those edge cases, we have
an entity which carries with it an implied EVENT. For instance:

- ``Make sure to eat something before your vitamins.''

- ``Loperamide helped to calm her stomach\textquotedbl{

This is an example of an implicit, or what we call metonymic, event,
in which ``vitamins'' stands in for ``taking your vitamins'',
and ``loperamide'' stands for ``the administration of loperamide\textquotedbl{}.
You do not want to apply identity relationships between the taking
action and the vitamins themselves, nor do you want to assume that
temporal relationships like ``before'' and ``after'' apply to
an object like a pill. Instead, these will be labeled as an EVENT
but given the METONYMIC feature. You should also mark IMPLICIT EVENTs
as ENTITYs since these events can corefer with ENTITYs or with EVENTs.
These are realized as \textit{both} EVENTs and ENTITYs, so that relations
can be made to both. Consider \Next.

- The nearby pipe *bomb* disrupted the festival. The *explosion*
from the *device* was heard for miles. \a. *bomb*$_{EVENT,METONYMIC}$
IDENTICAL *explosion* \b{.} *bomb*$_{ENTITY}$ IDENTICAL
*device*

Be exceedingly sparing with such metonymic annotations. For our purposes,
only use it when you are sure that a later relations phase will really
need to make reference to an entity's implied events. Otherwise, simply
annotate that entity as an ENTITY.


#### Multiword Predications - When are they multiple events?


##### Separate Predications

The following kinds of patterns tend to involve multiple events, but
these are to be treated as separate events, each given their own EVENT
annotation:
\begin{itemize
- Revelation: \subitem *Examination* *shows* decreased bilateral
peripheral *pulses*. \subitem Satellite *photos* *revealed*
signs of *fueling* at the missile complex.
- Reporting: \subitem ... and the right hilar *lesions* were not
*reported* as being *prominent*. \subitem The New York Times
first *reported* the *strike* in October. \subitem Refugees
*claim* that government troops *opened* fire on a crowded
marketplace.
- Denial or Denouncement: \subitem The mayor categorically *denies*
any *involvement* with the cartels. \subitem He *denies*
any chest *pains*, chest *pressures*, *shortness*-of-breath,
or exertional *symptoms*. \subitem The international community
was quick to *denounce* the *bombing*.
- Preference, endorsement, desire or consent: \subitem The Syrian rebels
have repeatedly *requested* international *aid*. \subitem
He is *willing* to *meet* with our Pauahi Wing Queens Hospital.
\subitem Three different countries have *endorsed* the trade
*agreement*.
\end{itemize
It is worth noting that EVIDENTIAL EVENTs (such as *shows*, *reported*,
*reveals*) almost always have two separate predications.


#####  Some Tests for Semantically Light Predications

Note, as mentioned above, that copular verbs like ``to be'' or ``seems''
are not annotated, nor are predications like ``experience'', ``underwent'',
and ``occurred\textquotedbl{}:

- After undergoing extensive *transformation*, Sochi is nearly
*ready* to *host* the *Olympic Games*.

- At **that time**, he also experienced rectal *pressure*
/ *fullness* and occasionally had *hematochezia*.

- The *earthquake* occurred during the *parade*.


- We *discussed* the role for adjunctive *treatment* if
*this* is colon *cancer* as well as neoadjuvant *treatment*
if *this* is felt more consistent with a rectal *cancer* on
flexible *sigmoidoscopy*. 
\end{comment


Other verbs are not as consistent. For example, we want to treat actual
events of needing and lacking as EVENTs, while ignoring other predications
which simply add a semantic feature of necessity to the main predication.
One (admittedly slippery) test is whether you can rephrase the instance
of `need' using the less eventive `it is necessary ...' and maintain
the same meaning. If so, then it is non-eventive and should not be
annotated.

- We may need to *hold* her *diuretic* before surgery.
(can be rephrased with ``It may be necessary for us to hold her diuretic...'')

- Blood *labs* revealed an urgent *need* for more iron.
(note how hard it would be to rephrase using ``it was necessary ...'')

Another such test can be used for verbs of planning, which are also
of variable semantic weight. If `plan to' can be replaced with `will
probably' or `hopes to' without major change in meaning, then it is
too semantically light, and should not be tagged. In contrast, if
it referring to the act of formulating plans for the future, then
it is eventive.

- City officials have been *planning* for the *race* for
several months.

- No oncologic *follow* - up is *planned* at this time.

- Patient is planning to *return* to his local oncologist
who he has a good relationship with. (see rough equivalence with ``Patient
will probably return to his ...'')

- Local fire departments plan to *enact* fire *bans* if
the hot weather continues. (Again, roughly equivalent to ``fire departments
will likely enact'')


#####  EVENTs without explicit reference

When we run into EVENTs that are clearly implied by a related ENTITY,
they can be marked as ENTITY with an ``implicit event'' feature,
as discussed in section \ref{when_is_an_entity}. Yet there are situations
such as the example below, in which there is an implicit event without
such a relationship to an ENTITY:

- Her main concern is that she does not wish to have a *colonoscopy*,
which she had back in the 1970s.

Here, there are actually two colonoscopies being discussed. One is
a hypothetical, near-future one which the patient is not interested
in having, the other occurred in the 1970s. The later instance is
the kind of implied event which we will be not marking in this project,
however, and thus you'd have a single annotation with the span *colonoscopy*,
DocTimeRel AFTER, Modality HYP, Polarity NEG.

Similarly, here, two sets of raids are implied, but only one is mentioned:
```
The *raids* in Phoenix *began* at 4am, in Denver, at 5.
```

The Denver raids, thus, would not be captured in this project. This
is not covered by these guidelines but we will be investigating whether
building on PropBank annotation of gaps might be helpful.


#### Selecting Proper Spans of Annotation

Once you have decided that a given phrase or word qualifies as an
EVENT or ENTITY, you'll need to decide what `span' (section of the
text) to annotate.

For each ENTITY and EVENT annotation, you might have found a long
phrase (or even, for EVENTs, a complex string of verbs and nouns)
which designates that concept. Yet we will not be annotating that
entire string, but instead will designate the phrase with a single
word, the syntactic ``head'' of the phrase.

Please note that \textbf{the syntactic head guidelines do not specify
what qualifies as an EVENT/ENTITY or not, but instead, how to select
a span for those words or phrases which do qualify}. Deciding whether
or not a term should be one, many or no entities or events is entirely
a semantic decision; this is merely a decision about the span which
you should mark after that. A single noun phrase can have many ENTITYs
or EVENTs (every word in ``United States Olympics Organization Chairwoman''
is an ENTITY), and the fact that a word is not the head of a larger
syntactic unit \textit{in no way} disqualifies it from separate annotation.


#### Minimum Span Annotation

One might talk about ``maximum span'' annotation as being everything
encompassing what you are talking about, an approach we are \emph{not
using here}:
\begin{examples
- \label{[The-7.6-magnitude-earthquake]}*\textsubscript{MAX-SPAN}The
7.6-magnitude earthquake* *\textsubscript{MAX-SPAN} had the consequences
of * *\textsubscript{MAX-SPAN} severe damage* to *\textsubscript{MAX-SPAN
multiple buildings* *\textsubscript{MAX-SPAN} last July*
\end{examples
We will take the opposite approach, using a \textsc{minimum span
style of annotation in which we only mark the syntactic head of each
markable. This is because capturing everything about what makes an
entity an entity, or an event an event, is not only difficult, but
can lead to elaborate overlapping annotations. As such, instead of
the kinds of annotations in \ref{[The-7.6-magnitude-earthquake]},
we will annotate everything except pronoun nouns using a single word,
resulting in spans such as: 
\begin{examples
- The 7.6-magnitude *earthquake* caused severe *damage* to multiple
*buildings* last **July**.
- The *U.S.* *President* *maintained* his *stance* on
the civil *war*.
\end{examples
This does not mean we are throwing this information away, but rather
that we assume this information to be recoverable. This emphasis upon
recoverability is important; we need to capture the word that lets
us ``find'' the rest of the phrase in question, or in other words,
the \emph{syntactic head}%
\footnote{We are following modern dependency conventions, such as La MarXXXXXXXXXXXXXX,
in our assumptions about what consistutes a head, with some exceptions
to avoid annotatoin of semanticallly light verbs (such as annotating
light verbs with their nominalizations) discussed below.%
}. Consider a syntactic dependency tree of the above sentence in this
regard 
\begin{examples
- \label{ExampleDepTree}>\textcompwordmark{}> Insert Dependency tree
Here
\end{examples
``Earthquake'', one may see, has a number of dependents. Annotating
it can be thought of as pointing to everything under it. This gives
us the best of both worlds -- you get to only grab one word (and therefore
do not have to fret about what span to annotate), while underlyingly
capturing the full range of ``what is being talked about''. 

If that tree in example \ref{ExampleDepTree} is foreign to you, do
not despair; all you need to do is follow some basic rules for what
we call ``headfinding''. In general:
\begin{itemize
- The traditional notion of headedness is that there is a word in each
phrase which essentially defines and represents that phrase. The head
is not the most important part of a phrase, but instead can usually
stand in for the entire phrase and mean roughly the same thing with
roughly the same grammatical properties. 

\begin{itemize
- One casual way to test this is what lexical term would be used in
a repeated version of the same. If you constantly talk about ``John's
insatiable hunger for more donuts'', one might refer to that hunger
as ``that hunger'', but not by ``those donuts''.
\end{itemize
- For verb phrases and adjective phrases this will be simple, and there
is no need to think of things in terms of \textsc{syntactic head}s
at all. You will only be annotating the verb or adjective in the phrase,
and nothing more. Thus, look at the events in the following examples
(no other parts have been annotated):\end{itemize
\begin{examples
- The stock price is *stable*.
- \label{reportsthrowingup}Patient *reports* *throwing* up.
- She's *unable* to *lift* her arms.
- Since her last *surgery*, she has seemed *disoriented* and
*moody*.
- She feels slightly *weak* but has *resumed* most of her normal
*activities*.
- The jury *finding* was in favor of the defendant.
\end{examples
Note that we take the single verb or adjective even when when dealing
with a multiword predication such as ``throw up\textquotedbl{}. The
exception to this tendency comes from \emph{light verbs} and \emph{support
verbs, }verb-object pairs in which the verb is less informative than
the object about the event in question, as in:
\begin{examples
- John took a *\textsubscript{event}bath*.
- The patient underwent *\textsubscript{event}surgery*.
- The burglar committed a heinous *\textsubscript{event}crime*. 
\end{examples
Note that in each, there is no individuation between the verb and
object -- they collectively assert an event -- and the verb is a grammaticalized
and abstract term. For a more full definition, here is the definition
discussed in relation to Propbank:
\begin{quotation
(Light Verb Constructions) are characterized by a light verb and a
predicating complement (henceforth, true predicate) that \textquotedbl{}combine
to predicate as a single element.\textquotedbl{} (Butt 2004) In LVC,
the verb is considered semantically bleached in such a way that the
verb does not hold its full predicating power. Thus, the light verb
plus its true predicate can often be paraphrased by a verbal form
of the true predicate without loss of the core meaning of the expression.
For example, the light verb \textquotedbl{}gave\textquotedbl{} and
the predicate \textquotedbl{}lecture\textquotedbl{} in \textquotedbl{}gave
a lecture\textquotedbl{}, together form a single predicating unit
such that it can be paraphrased by \textquotedbl{}lectured\textquotedbl{}. 
\end{quotation
Remember in this that if you \textit{can} cleanly separate a verb
and its noun into two separate events, then you should treat them
as two separate things. Similarly, some verbs like ``use'' are relatively
generic, but evoke a prototypical use of the object -- rather than
evoking the object as an event in itself. Verbs such as \emph{use
}are the main event:
\begin{examples
- \textquotedbl{}Police *\textsubscript{event}used* tear gas to
*\textsubscript{event}disperse* the protesters.\textquotedbl{
\end{examples
The same rules for minimal-span annotation will also apply to nouns.
Hopefully you will have some exposure to what the head of a noun phrases
is from syntactic courses, and this will be quite familiar. Start
by examining the example for participants which you desire to annotate;
say that you found the following:
\begin{subexample
- The most recent IED attack outside the Green Zone in Baghdad
- The shooting near the word-torn city
- That recision biopsy analysis of the sigmoid colon today
\end{subexample
For each, rule out prepositional phrases and post-postitional adverbs:
\begin{subexample
- The most recent IED attack \sout{outside the Green Zone in Baghdad} 
- The shooting \sout{near the war-torn city} 
- That recision biopsy analysis \sout{of the sigmoid colon today
\end{subexample
Then for each sequence of nouns, the head is the rightmost noun%
\footnote{If the rightmost term in a noun phrase (i.e. the ``head'') is a
particle of a nominalization, such as in ``the blow out flooded the
gulf with oil'', then ignore the ``out'' particle and annotate
``blow'' itself.%
}:
\begin{subexample
- The most recent IED *\textsubscript{event}attack* \sout{outside
the Green Zone in Baghdad} 
- The *\textsubscript{event}shooting* \sout{near the war-torn
city} 
- That recision biopsy *\textsubscript{event}analysis* \sout{of
the sigmoid colon today
\end{subexample
This doesn't mean that other entities and events won't be within the
spans you considered. The same examples should result in annotations
such as
\begin{subexample
- The *\textsubscript{event}shooting* near the war-torn *\textsubscript{entity
city* 
- That recision biopsy *\textsubscript{event}analysis* of the sigmoid
*\textsubscript{entity} colon* *\textsubscript{timex} today*
\end{subexample
There will be two exceptions to this ``minimal span'' rule; proper
names and times. Proper names should be annotated with all name parts,
so that ``Bill Clinton'' is not ``Bill *Clinton*'' but rather
``*Bill Clinton*''. Do not include determine determiners in
such terms:
\begin{subexample
- The most recent IED *\textsubscript{event}attack* outside the
*\textsubscript{entity}Green Zone* in *\textsubscript{entity}Baghdad*.
\end{subexample
Sometimes this head-finding will be difficult. For example, in clinical
texts, one might find fragmentary phrases in which prepositions have
been elided, as in ``patient had CT chest pelvis''. In such cases,
do feel free to attempt various paraphrases of what the phrase means,
and to pick the word that would be the head of those more full forms. 

Such a list of rules gives us the following heads (only showing the
nominals):

- *She* had experienced no *dizziness* until the *start*
of *chemotherapy*.

- The *Zetas'* latest *attack* resulted in the *killing*
of three Mexican *officials*.

- The *CT* showed a small rectal *abcess*.

- The long-awaited but ultimately brief *battle* outside the
*city* quelled the rebel *uprising*.

- The *patient* reports *nausea* and *vomiting*.

- *She* does note *darkness* of the *stools*.

- The *fire* quickly spread throughout the *valley*, resulting
in the *destruction* of 15 *homes*.

- *Levaquin* 750 mg p.o. q. day (will restart today)

- Her *yelling* shocked *everybody* at the *conference*.

- *We* also discussed *some* of the *toxicities* of
fluoropyrimidine-based *chemotherapy*.


#### Some Exceptions and Specific Patterns


\paragraph{Measurement Phrases

Another exception to a strict headedness approach is that ``few''
is not to be annotated as the head of sentences such as 
\begin{examples
- {*} *\textsubscript{entity}I * *\textsubscript{event} ate
* a *\textsubscript{entity}few * of the plums in the *\textsubscript{entity}icebox*
\end{examples
Instead, when the head is a quantifier-type term such as ``few''
or ``some'', use the thing counted, as in:
\begin{examples
- *\textsubscript{entity}I * *\textsubscript{event} ate *
a few of the *\textsubscript{entity}plums* in the *\textsubscript{entity}icebox*
\end{examples
This is hopefully clear in such cases, but will be more complicated
when dealing with words like ``groups of ..'', ``collections of...'',
and increasingly informative units. This will end of being a question
of whether there is one entity -- in which case the quantified term
will be head -- or two entities, a SET and a MEMBER, as discussed
in section \ref{sub:SET-MEMBER}. If one could imagine replacing the
phrase with a mere count of the items in question, merely mark the
latter:
\begin{example
Within eyesight, a \textbf{gaggle of *\textsubscript{entity}geese
*} lounged in the afternoon *\textsubscript{entity}sun*

\emph{= roughly 20 geese lounged in the afternoon sun.
\end{example
In contrast, if the unit seems to be clearly a unit that is more than
an aggregate collection of its parts, feel free to mark it as a delineated
unit with SET/MEMBER:
\begin{examples
- The *\textsubscript{entity}position * was defended by a \textbf{*\textsubscript{entity
battalion* of the *\textsubscript{entity}~3rd brigade*}.
\end{examples

\paragraph{Headedness with foreign phrases

For foreign phrases -- such as latin terms -- you should feel free
to use whatever part of the term seems to be acting as head in context.
For latin phrases, these will often be left-headed phrases where one
may take the first word in the phrase, as in:

- She has *diabetes* mellitus.

- *Polymyalgia* Rheumatica is a concern here.

- We suspect *myasthenia* gravis is the cause of her continued
weakening.

Do not, however, extend this to terms that have aquired casual use
in English, even if your knowledge of the word's origin informs you
of what the ``real'' head:

- He is the attorney *\textsubscript{entity}~general* of
Florida. 


\paragraph{Multi-word Proper Nouns

As a reminder, when the head noun is a proper noun with more than
one word, take the entire appropriate span, not just one word. This
policy applies to first-middle-last name mentions, as well as consistently-used
multi-word titles or names, so long as they are all specific to the
mentioned individual:

- They are investigating the policies of *North Korea*.

- Sochi is nearly ready to host the *Olympic Games*.

- *Barack Obama* condemned the Russian aggression.

- *William Francis Styler IV* helped write these guidelines,
and has an exceedingly long full name.

- *Dr. Franklin G. Cummings, Esq.* was on safari during the
attack.

- *His Holiness the Dalai Lama* visited Nepal this week.

- *The Artist Formerly Known as Prince* played a sold-out
show.

- *Her Royal Majesty Queen Elizabeth II* was in attendance.

... but keep in mind that optional premodifying noun-phrases are not
included in the mention span, and often result in entity mentions
of their own, so:

- They visited the much-esteemed *administrator* of the facility.

- Smith introduced the *Leader* of the Free *World* and
*President* of the *United States*, *Barack Obama*.


\paragraph{Morphological vagueness involving hyphenated and possessive words

This section has insisted upon annotating ``a single word'' as if
that is a clear-cut concept. We will generally make this clear cut
in the simplest manner possible, in that a word is surrounded by spaces. 

Hyphenated words will usually be an exception to this -- if one encounters
``CT-scan'', for example, one may treat it as ``CT scan'' and
take the appropriate head ``scan''. There are, however, many hyphenated
words with a bound form -- such as ``co-exist'' -- should not be
split up. Figure \ref{fig:Affixes-which-can} lists a collection of
morphemes which should be treated as forming a single word (from Santorini
XXXXXXX).
 
| Hyphenated Words |  |  |  |  |
|-------|-------|-------|---------|------|----------|
| aorto- | ante- | anti- |  arch- | ambi- | -able |
|-ahol   | -aholic | -ation | axio- | be- | bi- | 
| bio- | broncho- | co- | counter- | cross- | centi- | 
| circum- | cis- | colo- | contra- | cortico- | cran- |
| crypto- | -centric | -cracy | -crat | de- | deca- |
| demi | dis- | -dom | eco- | electro- | ennea- |
| -esque | -ette

ex-

extra-

-er

-ery

ferro-

-ful

-fest

-fold

gastro-

-gate

-gon

giga-

hepta-

hemi-

hypo-

hexa-

-hood

in-

inter-

intra-

-ian

-ible

-ing

-isation

-ise

-ising

-ism

-ist

-itis

-ization

-ize

-izing

ideo-

idio-

infra-

iso-

-less

-logist

-logy

-ly

judeo-

macro-

micro-

mid-

mini-

mono-

musculo-

neuro-

nitro-

mm-hm

mm-mm

-most

multi-

medi-

milli-

neo-

non-

novem-

octa-

octo-

o-kay

ortho-

over-

paleo-

para-

pelvi-

pheno-

penta-

pica-

poly-

preter-

pan-

peri-

phospho-

pneumo-

pseudo-

post-

pre-

pro-

quasi-

quadri-

quinque-

-rama

re-

recto-

salpingo-

sero-

semi-

sept-

soci-

sub-

super-

supra-

sur-

tele-

tera-

tetra-

tri-

uber-

uh-huh

uh-oh

ultra-

un-

uni-

vice-

veno-

ventriculo-

-wise

x-ray

x-rays

x-rayed \end{multicols} \caption{\label{fig:Affixes-which-can}Affixes which can form larger heads
\end{figure


Furthermore, when a ``-'s'' possessive marker is present, do not
treat that term as part of the word. Unfortunately, when there is
no clear delineating apostrophe present, as in ``his'', ``its'',
or even the mere absence of an appostrophe, graph the entire word. 

- We discussed the CT results with *Miss Mullins*. The *patient*'s
scan reveals *liver* *metastasis*.

- State *legislators* report that *their* constituents
are satisfied with the compromise.

\pagebreak{


###Annotating Features on Entities and Events

When you mark each entity or event, you will need to label basic features
on the events and entities. 


#### Entity Features -- Polarity and Modality

The majority of ENTITYs will be of the polarity POS for ``positive'',
meaning that they are actual entities. This is the default value.
You will occasionally find purpose to mark an ENTITY of a NEG polarity,
indicating that the ENTITY does not exist.

- *Mr. Black*$_{POS}$ spoke with *us*$_{POS}$ about
the new *facility*$_{POS}$. 

- *Cincinnati*$_{POS}$ doesn't have an *airport*$_{NEG}$.

- *John*$_{POS}$ couldn't attend the *concert*$_{POS}$
for lack of *money*$_{NEG}$.

A related feature is Contextual Modality, which identifies whether
the entity is a specific real entity, a class of entities, etc. The
majority of ENTITYs will be ACTUAL (they refer to real, specific entities),
and this will be the default value in Anafora. However, they can refer
to general classes of entities, the idea of entites, or even hypothetical
entities. One may define ENTITY as having any of our four modalities
(which you will use far more often with EVENTS): ACTUAL, GENERIC,
HYPOTHETICAL, or UNCERTAIN/HEDGED.

The most obvious kind of GENERIC entity will be references to ``kinds''.
Such generics in English are often bare plurals, but can be indefinites
or definites too:
\begin{examples
- *Terrorists*$_{GEN}$ in the *region*$_{ACTUAL}$ often attack
office *buildings*$_{ACTUAL}$.
- *A gentleman*$_{GEN}$ opens *doors*$_{GEN}$ for *ladies*$_{GEN}$(Krifka
2012)
- *The lion*$_{GEN}$ is the proudest of *animals*$_{GEN}$
- We do not normally recommend surgery to *patients*$_{GEN}$ with
a cardiac status similar to *Ms. James*$_{ACTUAL}$.
\end{examples
One easy way to distinguish GENERIC ENTITYs from ACTUAL ENTITYs is
by `omniscient substitution'. Consider `Union Leaders' in the examples
below:
\begin{examples
- Teddy Roosevelt met with Union Leaders before writing the bill.
- Union leaders often push for tax breaks.
\end{examples
In \LLast, an omniscient person could put together a list of the
specific persons he met with and replace it with that list:
\begin{examples
- Teddy Roosevelt met with \emph{Samuel Gompers, John Lewis, Walter
Reuther, A. Philip Randolph, and Jimmy Hoffa} before writing the bill.
\end{examples
Compare this to \LLast, where there is no way that the list could
be put together; it refers to the whole class. Therefore, `Union Leaders'
in \LLast is GENERIC.

Similarly, an omniscient annotator could know specific referents for
the below ACTUAL ENTITYs:
\begin{examples
- Three unidentified *criminals*$_{ACTUAL}$ broke into my shed.
- Tomorrow's *participants*$_{ACTUAL}$ will be thrilled.
- *Vandals*$_{ACTUAL}$ have defaced a prominent prehistoric pictogram.
\end{examples
But no referents (outside of every member, past present and future,
of a generic class) could possibly be found for the below GENERIC
ENTITYs:
\begin{examples
- *Criminals*$_{GEN}$ often plead ``Not Guilty'', even if they've
committed the crime.
- *Participants*$_{GEN}$ in Triathlons generally experience significant
chafing.
- *Vandals*$_{GEN}$ should be punished severely if caught.
\end{examples
The complexity of that annotation will occur with entities which are
sets, but where the set has been defined provisionally in context:
\begin{examples
- *Young Denver voters*$_{GEN}$ turned out in high numbers for
the last election.
- *My senior class*$_{ACTUAL}$ performed quite well on *the SAT*$_{GEN}$
\end{examples
These kind of examples will be hard to measure with the above tests
-- they both are ``real'' sets of things in the world , and both
describe whole classes of objects. For these, test whether you can
paraphrase that particular noun phrase with something like 'the kind
of \_\_\_', such as ``the kind of young people who vote in Denver''.
If that paraphrase task seems hard or forced, use ACTUAL. 

Similarly, noun compounds contain another ambiguous kind of noun along
this boundary of ACTUAL and GENERIC. While a \textquotedbl{}hot dog
stand\textquotedbl{} sells actual hot dogs, its name is not due to
the 384 hot dogs it may have sold that particular day, but because
of its general purpose of being a kind of stand that sells hot dogs
in general. There are GENERIC, and one should fret over whether to
annotate them at all, using the rules defined in \ref{when_is_an_entity}.

A third kind of option for ENTITY modality is that of HYPOTHETICAL
entities. Hypothetical entities are not just entities participating
in a hypothetical situation -- all sorts of entities can be involved
in hypothetical worls -- but rather an entity that would not exist
outside of that hypothetical possible world. 
\begin{examples
- If he did have a Mustang$hypothetical$, he would wreck it.%
\footnote{For the purpose of this hypothetical definition, you can treat objects
as coming into being when purchased; don't give in to technicalities
of whether they might exist even if not purchased. %

\end{examples
As will come up later for GENERIC vs HYPOTHETICAL events, note also
that generalizations with ``if'' are still GENERIC. You should test
this by whether you can paraphrase it with a true generalization instead:
\begin{examples
- \label{couple-stacking-shelves}\textquotedbl{}I'm not saying that
if a *couple*$_{GEN}$ both work stacking shelves, they should
be getting married in a supermarket$_{GEN}$\textquotedbl{
- \label{coupe-stacking-shelves-paraphrase}I'm not saying that couples
that work stacking shelves should get married in supermarkets
\end{examples
Both examples are GENERIC here, because \ref{couple-stacking-shelves
passes that generic paraphrase test as shown in \pageref{coupe-stacking-shelves-paraphrase}. 


\paragraph{Generic You and We

\textquotedbl{}You\textquotedbl{} is to be marked as GENERIC when
it passes tests for \textquotedbl{}generic you\textquotedbl{} usage: 
\begin{itemize
- It can be paraphrased using \textquotedbl{}one\textquotedbl{}, \textquotedbl{}somebody\textquotedbl{},
\textquotedbl{}a person\textquotedbl{}, etc. 
- It would be translate into a generic pronoun in any languages you
know (such as \textquotedbl{}on\textquotedbl{} in French). 
- Restating \textquotedbl{}you\textquotedbl{} to be an apposition with
the audience's name, such as \textquotedbl{}You, John...\textquotedbl{
would change the meaning of the sentence. 
\end{itemize
For example: 
\begin{examples
- gotta love the people who insist on \textquotedbl{}helping\textquotedbl{
*you*$_{GEN}$ when it could be easier to do it *yourself*$_{GEN}$.
\end{examples
It's harder to define the delineation of \textquotedbl{}we\textquotedbl{}.
Mark \textquotedbl{}we\textquotedbl{} as GENERIC only when the set
referred to is \textquotedbl{}everybody\textquotedbl{}, i.e. the entire
human race, or is an undefined set that could be synonymous with this:

- What is this biotech revolution you are referring to that *we*$_{GEN}$
are on the verge of?

Generic \textquotedbl{}you\textquotedbl{} and \textquotedbl{}we\textquotedbl{
are subject to the \textquotedbl{}identity of very broad GENERICs\textquotedbl{
rules; see section \ref{vbroadgens}.


\paragraph{Uncertain/Hedged

As with HYPOTHETICAL, use Uncertain/Hedged only when the sheer existence
of the entity (not its role in the sentence) has been placed in doubt.


#### Event Polarity and Modality

In order to express the polarity of an EVENT, the ``polarity'' attribute
of an event is specified. Polarity in this schema is relatively straightforward,
and there are only two possible types: POS and NEG.


#### Positive Polarity (POS)

The first and most common polarity value used is POS. This is the
marker of positive polarity. This is used for an EVENT that did, in
fact, occur. Most events annotated are of this polarity, and this
is the default value. POS need not be specified in annotation.

- Three *attacks* *occurred* last week.

- Despite international *condemnation*, North Korea is now
officially a nuclear *state*.

- The patient has *hepatosplenomegaly*.

- PO *changes* right pterional *craniotomy*

- The patient will *continue* treatment.


#### Negative Polarity (NEG)

The opposite of POS, as you might guess, is NEG, which is used to
indicate when the event didn't take place, or has an otherwise negative
polarity:

- Three attacks occurred last week, but one *attack* was prevented.

- There is no *sign* of the small plane, and rescuers located
no *survivors*.

- Otherwise, he has not had any *nausea*, *vomiting*,
*diarrhea*, chest *pain*, *shortness* of breath, or *fever*.

- She is not *interested* in pursuing *chemotherapy* at
this time.

- The patient did not *report* *nausea*.

- A cystic duct lymph *node* is not *identified*.

In \LLast and \Last, there are two EVENTs being negated. The first
is a verbal EVENT of reporting, the second is a condition. In this
case, we can negate both the reporting of nausea and the identification
of the lymph node, as neither occurred. In addition, the nausea and
lymph node aren't present. So, both EVENTs in both examples are negated.

We should also highlight that NEG means ``did not happen'' or ``not
true'', rather than ``negative'' in the medical testing sense (usually
meaning ``shows no signs of cancer''). So, for something like:

- Her *colonoscopy* was negative.

The colonoscopy is still polarity POS (as it did, in fact, happen),
and ``negative'' is simply telling us that no cancer was found.
An actual polarity NEG colonoscopy would be something like:

- We were unable to perform a *colonoscopy* due to bad prep.

\vspace{0.5cm
 \fbox{ %
\begin{tabular}{p{0.6in}p{14cm}
\includegraphics[width=0.5in]{warning} \\
\textbf{Caution!}  & \raisebox{4mm}{%
\parbox[c]{14cm}{%
\vspace{2mm
\textit{ Do not worry about double-negation or phrase-level negation.
In the phrase ``She denies vomiting or nausea'', *denies* is
POS (as the denial is real) and *nausea* and *vomiting* are
both NEG because they didn't happen. Each EVENT should be considered
on its own (rather than as part of a greater denial), and if the EVENT
did not happen, it is NEG, no matter what phrasing may have preceded
it.}%
}}\ \
\tabularnewline
\end{tabular}} \vspace{0.5cm



#### \label{modality}Actual Modality (ACT)

The first is ACTUAL, which is used most of the time, and is the default
option (that need not be specifically marked). The majority of EVENTs
are ACTUAL, having already happened or been scheduled (without hedging)
to happen.

- The patient's new *tumor* is 3.5cm from the epiglottis.

- The patient did not *report* *nausea*.

- His anterior chest rash has not *reoccurred*.

Note that ACTUAL and NEG can (and usually do) co-occur -- anything
which clearly did not happen is ACTUAL+NEG. 


#### Uncertain/Hedged Modality (UNC)

EVENTS are marked as UNCertain when we can point to some explicit
lexical or phrasal trigger that indicates some degree of uncertainty
about the reality of the EVENT. Put differently, these EVENTs are
presented with a sort of tacit claim that they're \textit{probably
real (unlike hypotheticals, which are explicitly irrealis), but with
a proviso from the author that they might be not be.

This also includes EVENTs that are mentioned with any sort of hedging.
This hedging can be lexical (``seems'', ``likely'', ``suspicious'',
``possible'', ``consistent with'', ``claims''), or phrasal (``I
suspect that...'', ``It would seem likely that...'', ``In all
probability...''). These EVENTs are strongly implied, but, for safety,
liability, or due to lack of comprehensive evidence, are not stated
as fact. As such, it is very important that these uncertain EVENTs
be included in the timeline, but be marked so that they can be easily
differentiated from known facts.

- Radiation levels and seismic disturbances were measured which
are consistent with nuclear *testing*.

- Fifteen missing miners, who are now widely presumed *dead*,
are still underground.

- All evidence seems to point to *kidnapping* in the disappearance
of Dr. Charles.

Hedging is, due to the influence of malpractice law, extremely prevalent
and varied in the medical literature:

- Ultrasound findings were felt to be consistent with a T3, N1
rectal *tumor*.

- An approximately 3cm nodular region of intermediate T2 signal
involving the body of the corpus callosum is suspicious for *residual
or recurrent tumor* but appears unchanged from the patient's prior
examination.

- She has a rash not inconsistent with *measles*.

- The patient may have undergone a mild *stroke*.

Note that a doctor providing or commenting on evidence for a given
finding does not qualify as hedging, so the following EVENTs would
not be marked UNC:

- She *denies*$_{\text{ACTUAL}}$ *vomiting*$_{\text{ACTUAL, NEG}}$

- There is no *evidence*$_{\text{ACTUAL, NEG}}$ of *MS*$_{\text{ACTUAL, NEG}}$

But further active hedging can push this over into UNC:

- She *denies*$_{\text{ACTUAL}}$ *bulimia*$_{\text{UNC, POS}}$,
but all *signs*$_{\text{ACTUAL, POS}}$ point to its presence$_{\text{UNC, POS}}$

- There is no concrete *diagnosis*$_{\text{ACTUAL, NEG}}$
of *MS*$_{\text{UNC, POS}}$, but given her *symptoms*$_{\text{ACTUAL, POS}}$,
it seems extremely likely.

One final note: In order to mark something as UNCertain, there must
be evidence in the text itself. So:

- **Yesterday**, I was *abducted* by aliens and a prominent
politician who was not at all *corrupt*.

In this case, the annotator knows that both the abduction and the
negated corruption of the politician are incredibly unlikely based
on our understanding of the universe. That said, because they are
presented as fact in the text, we have no choice but to treat them
as ACTUAL. It is not our role to judge the veracity of the claims
being made in text, but instead, simply to mark the claims as accurately
as possible.

Another common use for Uncertain/Hedged is in accusation:

- She returned home after allegedly *stealing* the diamonds.

- Mr. Lucas, who allegedly *killed* eight people, will not
testify in his own defense.

Here, we don't know that there was stealing or killing (at least,
of the specific instance alleged to have happened), just that it's
being alleged. Both events should be UNCertain. Similarly:

- Frank was arrested for *resisting* arrest.

The mere fact of his arrest does not prove (nor even assert) the existence
of actual resistance, simply that this is the charge for which he
was arrested. As such, the resisting (which is asserted but not proven)
is UNC. Compare with:

- Frank was convicted of *resisting* arrest and sentenced
to probation.

Here, although there's still a chance that Frank was wrongly convicted,
we must believe our author who asserts the truth of the *resisting*.
Put differently, all crime events are UNCertain until proven ACTual
in a court of law.


#### Hypothetical Modality (HYP)

The third modality is HYP. This is useful when annotating theories,
future possibilities, or other hypothetical events. Hypothetical EVENTs
will often follow ``if'' statements (``If X happens, then we will
use Y to treat Z'') or other sorts of conditionals (``Depending
on the patient's response, we might treat A with B or with C'').

- If the Israelis *strike*, the US will surely be *dragged*
into a larger conflict.

- Any possible *attack* would *draw* widespread *condemnation*.

- I've warned the patient that this new medication may cause peripheral
*edema*.

- We suspect either *achalasia* or *pseudoachalasia* here.

- If she experiences a *fever*, we will *treat* *it*
on an outpatient basis.

It is worth noting that, in this schema, an EVENT occurring in the
future does not imply that the EVENT is HYP (although most hypothetical
EVENTs will be AFTER DOCTIME). Although it is true that there is always
a degree of uncertainty with anything happening in the future, HYP
marks explicit uncertainty in the text, and should not be used just
to indicate this future-uncertainty.

For instance:

- Any US *assault* in the region would probably *come*
from Kuwait and Saudi Arabia, with *support* from the Carrier
group in the Persian Gulf.

- We may *recommend* to *resume* the *Cipro* and *Flagyl*
and obtain a *CT* of the chest, abdomen and pelvis.

In the above, all the bracketed EVENTs are HYPOTHETICAL and have DocTimeRel
of AFTER.

- The *close* of Market Friday will *mark* the *end*
of Mr. Johnson's long career.

- The patient's *myringotomy* will take place on Friday.

In the above two examples, the marked EVENTs are expected, so DocTimeRel
is AFTER, modality is ACTUAL. Compare that to:

- If she has additional *bleeding* next week, she should *come*
back in.

In \Last, both ``additional bleeding'' and ``come back in'' would
be HYP, in addition to being AFTER the DOCTIME.

In addition, polarity and modality of EVENTs do not interact, even
though one might expect them to. It is true, at least from a real-world
point of view, that a HYP EVENT, by definition, hasn't happened. However,
polarity should not change on that basis alone. There are POS polarity
HYP EVENTs (``She might develop a rash'') as well as NEG polarity
ones (``The treaty will only hold if there are no more *attacks*'').

It is also worth noting that very often, verbs of discussion lead
to HYPOTHETICAL EVENTs (although they themselves are not hypothetical):

- We discussed the risks of adjuvant *chemotherapy* and *hemicolectomy*
with the patient.

- Discussed the potential for neoadjuvant *therapy* depending
on the findings of his MRI and studies.

But, of course, one must be careful not to overapply the rule, as
sometimes actual facts can be discussed as well, as below:

- I *discussed* the *effects* of his drinking and the
potential *progression* of his liver cirrhosis.

Note that in \Last, the *effects* are ACTUAL, but the *progression*,
at this point, is hypothetical and contingent on the patient's continued
drinking. Please see Section \ref{discussion} for additional detail
about the usage of HYPOTHETICAL with verbs of discussion.

\vspace{0.5cm
 \fbox{ %
\begin{tabular}{p{0.6in}p{14cm}
\includegraphics[width=0.5in]{warning} \\
\textbf{Caution!}  & \raisebox{4mm}{%
\parbox[c]{14cm}{%
\vspace{2mm
\textit{ Although many human languages feature such an interaction,
in our schema, modality does not interact with polarity or DocTimeRel.
Future EVENTs are assumed to be actual unless stated otherwise, and
it is possible (even common) to have an ACTUAL negated EVENT. Future
or negated do not automatically mean ``hypothetical\textquotedbl{}.}%
}}\ \
\tabularnewline
\end{tabular}} \vspace{0.5cm



#### Generic Modality (GEN)

\label{generic

GENERIC is our fourth contextual modality, and is used for EVENTs
which may be mentioned in a note, but are only mentioned in a general
sense, and do not appear on the timeline of the overall document.
These usually occur as justification of treatment (in the clinical
narrative), or to provide background or information in the general
domain.

All of the below EVENTs would be marked GENERIC under our schema:

- In the *aftermath* of most *bombings*, *trampling*
is a deadly *threat*.

- In New Zealand, bills must be *approved* three times by
Parliamentary *votes* and then *receive* Royal *Assent*
from the Governor-General.

- Adjuvant *chemotherapy* following *surgery* is generally
*recommended* in *situations* similar to this.

- I explained that BRAF *mutations* have no predictive value
with regard to cetuximab *sensitivity*.

- In other patients without significant *comorbidity* that
can *tolerate* adjuvant *chemotherapy*, there is a *benefit*
to systemic adjuvant *chemotherapy*.\textquotedbl{

Although HYPOTHETICAL and GENERIC may seem similar, remember that
most HYPOTHETICAL EVENTs still refer to the specific content of the
article, but depend on some eventuality occurring, and make reference
to specific EVENTs on the timeline, whereas GENERIC events don't require
specific reference or conditions.

This provides an excellent test for GENERIC in practice: If a sentence
would be true if copy-pasted into any contemporaneous article, note,
or text, then it is most certainly GEN:

- The terrorists *fled* Jordan via the Lebanese border.

The truth of this fleeing EVENT depends on the identity of the terrorists
and the context of the article to be true or false. Although \textit{these
terrorists fled to Lebanon, the next may flee to someplace else entirely.
Thus, it is ACTUAL. Compare with:

- Terrorists often *flee* to nation-states with crumbling
governments to avoid *interference*.

This fleeing EVENT would be equally true in any article about any
terrorists, international fugitives, or even in an article about governmental
collapse. Thus, both *flee* and *interference* are GENERIC.

Finally, remember that as discussed in \ref{dtroverlap}, \textbf{if
an EVENT is GENERIC, DocTimeRel will always be OVERLAP}.




#### Edge Cases: Counterfactuals and Past Negation

There are ambiguities involving hypotheticals and negation. Take,
for example, this sentence:

- *Had* John *gone* to the *park*, *he* would've
*seen* the cute *puppy*.

There's clearly lots going on in this sentence, but let's focus on
*seen*. There are two ways of annotating the event:
\begin{enumerate
- \textbf{*seen*}: DocTimeRel: BEFORE, Polarity: POS, Modality:
HYP 
- \textbf{*seen*}: DocTimeRel: BEFORE, Polarity: NEG, Modality:
ACT 
\end{enumerate
Both are technically correct. You can view the seeing of the puppy
as something that could have actually happened, or as something which
certainly did not.

As such, we have developed a hard-and-fast rule:

\textit{When faced with a past hypothetical which we know did not
happen, it is NEG/ACT. If you're unsure whether it happened, it's
POS/HYP. If it happened, it is POS/ACT.

So, when applied to data:

- If Will had stopped by the store, he'd have *bought* cupcakes.
But he was too lazy. \a. \textbf{*bought*}: DocTimeRel: BEFORE,
Polarity: NEG, Modality: ACT

- If Will stopped by the store, he probably *picked* up cupcakes.
He lacks the fortitude to resist frosting. \a. \textbf{*picked*}:
DocTimeRel: BEFORE, Polarity: POS, Modality: HYP

- Will stopped by the store, so, of course, he *bought* cupcakes.
Do you want one? \a. \textbf{*bought*}: DocTimeRel: BEFORE, Polarity:
POS, Modality: ACT

- If we had added this section to the guidelines earlier, our
annotator agreement would have been *better*. \a. \textbf{*better*}:
DocTimeRel: BEFORE, Polarity: NEG, Modality: ACT

Please be sure to follow this rule as you proceed with your entity
annotations.

\color{black} 


#### \label{eventfeatures}Event DocTimeRel

DocTimeRel is short for ``Document Creation Time Relation'', and
represents the temporal relation between the EVENT in question and
the time when the article, post or record in question was created
(the ``document time''). For the purposes of this schema, we are
assuming that the time of publication is functionally equivalent to
the time of writing (and that nothing substantial has changed in that
interim), and, for medical records, that the time of writing is the
same as the time of the patient's visit.

DocTimeRel allows us to avoid the linguistic ambiguities inherent
in explicitly marking the grammatical tense of the verb (like ``past'',
``present'', or ``past perfect''), instead marking the actual
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

\begin{figure*
\centerline{ \mbox{\includegraphics[width=5in]{doctimerel}} 
\caption{Schematic view of all the DocTimeRel possibilities relative to DOCTIME


\label{Tenseschematic} 
\end{figure*



#### BEFORE

BEFORE is used where the event ended before the document itself was
written. The bracketed events below would be marked as ``BEFORE''
(and all other EVENTs and TIMEX3s are unmarked):

- The *shooting* *shocked* the small city.

- He is taking in adequate nutrition and adequate fluids; consumed
3500 *calories* and drank 2-3 liters of *fluid*.

- This is unchanged and may be related to treatment *changes*.

- Today's study demonstrates a marked improvement compared to
the prior 9-16-03 *study*.

- Until last week, the patient had had no *nausea*.

- She had experienced no *dizziness* until the *start*
of chemotherapy.

- The patient had had no *fever* before the *start* of
her *surgery* last week.


#### OVERLAP

\label{dtroverlap} OVERLAP is used for events or states which are
happening or true at the time that the document was written:

- The fires *continue* to *burn* in the Mountains, despite
today's *rain*.

- Captain Smith of the Boulder County Sheriff's office is *requesting*
that anybody with information come forward.

- The patient *continues* to *do* well as an outpatient.

- The patient is *alert*, *cooperative*, and *appears*
to be in no acute *distress*.

- Moderate sized retention *cyst* or *polyp* in the right
maxillary antrum again *noted*.

- \label{twin} She is not *interested* in pursuing chemotherapy
at this time but is *interested* in continued *surveillance*.


#### AFTER

AFTER is used where the event is scheduled or planned to begin following
the document time:

- After the fires are *contained*, residents can *return*
home.

- Thursday's planned *strike* will put *pressure* on the
University to pay graduate teachers a living wage.

- *Levaquin* 750 mg p.o. q. day (will *restart* today)

- The patient will *return* tomorrow for *labs* and *exam*.

- She is not interested in pursuing chemotherapy at this time
but is interested in *continued* surveillance.

It is worth pointing out that \Last, considered alongside \ref{twin},
shows the interaction between DocTimeRel and ALINK to cover the idea
of ``already happening, and will now continue\textquotedbl{}.

There is one specific situation which must be discussed. EVENTs with
a Contextual Modality of GENERIC (discussed in \ref{generic}) will
always have a DocTimeRel of OVERLAP, as stated truths are, presumably,
true at Document Time. See \Next below.

- I explained that BRAF *mutations* have no predictive value
with regard to cetuximab *sensitivity*.


#### BEFORE-OVERLAP

\label{beforeover} BEFORE-OVERLAP is used where an event started
BEFORE the DOCTIME and continues into and through the DOCTIME (OVERLAP
with DOCTIME). Simply put, this is used where an event started before
the exam or patient visit and continues through to the present, and
often (but not always) corresponds with the use of the English present
perfect tense:

- The regime has been *arresting* suspected dissidents and
shows no sign of stopping.

- The fires have *burned* for eight days now.

- The patient has *felt* quite well and his appetite has been
*good*.

- She has not *seen* a cardiologist.

- She has had no *fever*.

- Based on last Thursday's MRI, her *swelling* is mostly gone.

Many (if not most) instances of OVERLAP entities could be inferred
as having also extended into the past. This label is \textit{only
for those events which explicitly provide evidence, in that particular
sentence, for it occurring in the past as well as the present, and
when that evidence is in the list below.


\paragraph{Admissable evidence for BEFORE/OVERLAP
\begin{itemize
- The event is in the present prefect aspect: \textquotedbl{}I have
been doing yoga for years\textquotedbl{}, \textquotedbl{}The fires
have burned for eight days\textquotedbl{}, \textquotedbl{}He has felt
good\textquotedbl{}. 
- The document contains a TIMEX3 that assigned a time or date, in the
past, where that document happened. 
- The event is modified by the discourse marker \textquotedbl{}still\textquotedbl{
and it is the \textquotedbl{}temporal\textquotedbl{} sense of still,
meaning \textquotedbl{}this has been happening and continues to happen\textquotedbl{}. 
- Aspectual verbs modify the verb, to the extent that one will probably
mark it as CONTINUES. 
\end{itemize

\paragraph{What is NOT admissable evidence for BEFORE/OVERLAP
\begin{itemize
- You cannot mark this based upon knowledge of the tense of other, coreferential
instances of the same event; mark is as OVERLAP or BEFORE based upon
the actual local context. 
- If an event is presented as OVERLAP but is mentioned as a past speech
act, as in \textquotedbl{}He said that there is no threat\textquotedbl{},
this is \textit{not} enough evidence for BEFORE/OVERLAP.
\end{itemize
\vspace{0.25cm
 \fbox{ %
\begin{tabular}{p{0.6in}p{14cm}
\includegraphics[width=0.5in]{warning} \\
\textbf{Caution!}  & \raisebox{4mm}{%
\parbox[c]{14cm}{%
\vspace{2mm
\textit{Be sure that any time you are using BEFORE-OVERLAP, it is
been explicitly stated that an EVENT started before DOCTIME and continues.
Even if you, as a human, can infer that a given EVENT must have started
before the document time, or that an earlier EVENT is likely to continue,
do not mark an EVENT as BEFORE-OVERLAP unless there is evidence in
the sentence itself. Pick BEFORE or OVERLAP -- whichever is explicitly
shown by the text -- instead.}%
}}\ \
\tabularnewline
\end{tabular}} \vspace{0.5cm



\paragraph{DocTimeRel in relation to speech

When dealing with documents involving indirect speech (as is often
the case in newswire), there can be a number of conflicting signals
about what the \textquotedbl{}time\textquotedbl{} of an event is.
A common pattern, for example, is a past tense report (\textquotedbl{}he
said ...\textquotedbl{}) that is reporting about a present tense state,
\textquotedbl{}...that there is no threat\textquotedbl{}.

When not dealing with direct quotations, you can assume that the \textquotedbl{}time\textquotedbl{
of an event is being accurately reported by the document as a whole:
for the pattern such as \ref{nothreat} below, you can mark the \textquotedbl{}threat\textquotedbl{
as OVERLAP:

- \label{nothreat} He declared that there is no threat.

- The boss said that we are working$_{\text{OVERLAP}}$ on it.

Resist the temptation to mark these as BEFORE/OVERLAP (while past
tense is often inferrable, we do not consider this to be proper \textquotedbl{}evidence\textquotedbl{
for BEFORE/OVERLAP: see section \ref{beforeover} for the allowable
BEFORE/OVERLAP criteria.

Note that this is only a constraint for indirect quotations; the time
of the speech event, in direct quotations, can be evidence of BEFORE
or BEFORE/OVERLAP conditions, as in:

- Napoleon declared$_{\text{BEFORE}}$ \textquotedbl{}I will conquer$_{\text{BEFORE}}$
Russia\textquotedbl{


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
events are usually marked with words like ``intermittently'' or
``occasionally'', and when such phrasing is used, the EVENT is marked
as INT. These indicate that, for instance, the patient has had vomiting
since a certain time, but he/she has not been vomiting 24/7 since
that point.

Please note that INT will only be used for irregular, unpredictable
periods (like the period of time between seizures or vomiting) and
not for things like medications or dialysis (which occur on a set
schedule). An event which occurs at an explicit interval can either
be treated as a constant (``the patient is taking *montelukast*
for asthma'') or the interval can be marked as a TIMEX3 (``She undergoes
dialysis *every three days*''), which is then TLINKed to the
original event.

It is important to note that we are only marking INT when there is
an explicit mention of intermittency in the sentence. Even if you
happen to know that a given EVENT or disorder often manifests intermittently,
if it is not stated explicitly as doing so, you should not mark it
as such. As with all of these annotations, we are marking the relations
mentioned in the document, not those you can infer from your own background
knowledge.

- Occasional *protests* have occurred in the last six months.

- The region is on edge after 2 years of sporadic *violence*.

- He reports occasional bright red *bleeding* from the rectum.

- Patient complains of intermittent chest *pain*.

- She has had intense *headaches* on and off since her last
visit.

If you are unsure about the contextual aspect of a given EVENT, mark
it as N/A.


#### Type of EVENTs

Some EVENTs do not actually represent real-world events, but instead,
provide aspectual information (starting, stopping, continuing) about
other EVENTs. To differentiate these EVENTs from the traditional clinical
EVENTs which occur on a timeline, we use the ``type'' marker. It
has three values: ``N/A'', ``ASP'', and ``EVI\textquotedbl{}. 


###### N/A

\textquotedbl{}N/A'' is the default value, and represents the vast
majority of EVENTs in the schema, and unless explicitly mentioned
otherwise (below or in the ALINK section), represents all EVENTs used
in examples in the Guidelines. Unless the EVENT is of the specific,
relatively closed class listed below under ASPECTUAL, or providing
evidential information (see EVIDENTIAL), it will be marked as ``N/A''
(or, as it is the default value, left blank).

One other note on the word ``recurrence'', which is often troublesome
for annotators working with the N/A/ASPECTUAL distinction. In an example
like:

- She has significant risk for tumor *recurrence*.

\textquotedbl{}recurrence'' does actually carry some aspectual information
(the tumor would have restarted). However, because the word ``recurrence''
would not be aspectual in ``she has risk of recurrence'', we have
chosen never to mark the word as an ASPECTUAL EVENT. Instead, this
will be an EVENT of type N/A, with a span of ``*recurrence*'',
as shown above. No ALINK annotations will be made here.


###### ASP - Aspectual

The next EVENT type is ASP, which is used to indicate an event whose
function is to emphasize or code the aspect of a later event, like
``continues'',\textquotedbl{}restart'', or ``terminated\textquotedbl{}.
Every EVENT of type ``aspectual'' must later participate in an ALINK.

- The community *continues* to worry about the possibility
of future strikes.

- Although there had been a period of relative peace, the desecration
of the temple *restarted* sectarian violence once again.

- The rash has not *reappeared* and we will monitor closely.

- We're going to *hold* her heparin until after her surgery.

- The patient will *continue* treatment.

- She is not interested in pursuing chemotherapy at this time
but is interested in *continued* surveillance.

These represent a relatively closed class, and you will find yourself
marking the same words as aspectual EVENTs over and over again. This
is expected, and should not be cause for concern.

A particularly good way of distinguishing between ASPECTUAL and non-aspectual
EVENTs is by substitution. A true ASPECTUAL can always be substituted
(even if losing some meaning) with similar ALINK triggers:

- We *completed* treatment today

Here, *completed* could be rephrased as ``We stopped/ended/finished/finalized/terminated
treatment today\textquotedbl{}. Compare that with:

- She *completed* the form

This *completed* cannot be replaced by ``She stopped/ended/finished/finalized
the form'' without significant coercion of meaning, and thus, is
not ASPECTUAL.

So, if you're marking an EVENT ASPECTUAL, the EVENT in question will
need to be able to be paraphrased (while retaining most of the meaning)
using words from one of the below four sets, each corresponding to
a different ALINK type (INITIATES, TERMINATES, REINITIATES, CONTINUES):
\begin{enumerate
- started/began/initiated/got going
- stopped/ended/finished/finalized/terminated/held
- restarted/started over/began again/reinitiated
- continued/persisted in/proceeded in/didn't stop
\end{enumerate
If an EVENT cannot be paraphrased using any of the words above, it
is not aspectual.


###### EVI - Evidential

The other EVENT type is EVI. EVI EVENTs are a little bit strange,
in that they are not technically relevant to the patient, but they
provide information about how doctors or journalists came to identify
and learn about other events. EVI EVENTs are a relatively closed class,
generally verbs of showing, demonstration, evidence, reporting, confirmation
or revelation, and in the clinical domain, are very commonly associated
with tests, imaging, and human observation.

In short, an EVENT should be marked EVI only if it serves as the link
between a source of knowledge or observation and a piece of knowledge
gained from it.

- Satellite photography *shows* increased troop movements
near the border.

- The Chicago newspapers *reported* the victory hours before
it was made official.

- Subsequent bloodwork *revealed* severe anemia, and the patient
was admitted.

- Dr. Green *pointed* out a patch of skin discoloration suspicious
for melanoma.

- We will plan to proceed with surgery unless her tests *indicate*
cardiac problems.

- His home health nurse *noticed* a mild increase in confusion
and fatigue during chemotherapy.

- CT scan *confirms* diverticulitis.

- She has a *confirmed* sulfa allergy.

It is worth reiterating that one does not mark the test, reporter,
or perceiver as EVI; instead, you will mark the verb of perception,
reporting, revelation, or indication as an EVI EVENT.

Finally, much like aspectual \textsc{event}s, you will be likely marking
the same verbs as EVI over and over again, and will very quickly learn
to recognize which verbs belong to this class and which do not.


#### Annotating representation of EVENTs

\label{representation

Some EVENTs that we will mark are not necessarily explicit EVENTs,
but rather, ENTITYs which are interpreted in context as representing
an EVENT.


###### Default -- Explicit

This is the default value, and corresponds to an EVENT whose span
itself represents an EVENT:

- There was an *attack* last week.


###### Implicit

The other possibility is an EVENT whose span looks like it should
only be a ENTITY, but which nonetheless represents an implicit EVENT
derived by metonymy.

- I've prescribed 15mg *Levaquin* for a UTI.

In \Last , ``Levaquin'' is an entity, but has an implicit ``taking
Levaquin'' EVENT.

- The *bomb* ended the festival three days early.

Here, ``bomb'' is metonymic for the attack itself, in addition to
representing the explosive device. The physical bomb did not end the
festival, rather, its detonation.

Because you may need to include IMPLICIT EVENTs' ENTITYs within larger
coreference chains (and thus, will need a marked ENTITY annotation),
please mark each METONYMIC EVENT both as an EVENT with the METONYMIC
type specified, and as an ENTITY.


#### Annotating degree of EVENTs

In order to express an incomplete degree of an EVENT, the ``degree''
of an event is specified.

In practice, degree is used as a companion to polarity, as a way of
allowing us to say that something is ``mostly'' or ``a little bit''
true, rather than forcing us to call every EVENT 100\% positive or
negative. Allowing something to be ``a little true'' (``She has
slight pain'') or ``largely false'' (``her scar is nearly gone'')
permits greater nuance in our representation of EVENTs than POS or
NEG generally allows.


#### N/A, MST - Most and LTL - Little

\label{little

Our three different degrees are N/A, MST, and LTL. N/A is used where
there is no need to mark either of the other two degrees on the EVENT,
and is the default value for degree. These are used when there has
been ``a little'' of an event, or a large (but not complete) change:

- She was only slightly *injured* by the blast. (LTL)

- The temple was mostly *destroyed* in the recent violence.
(MST)

- There is a small amount of bright T1 *signal*. (LTL)

- Abdominal tenderness has nearly *disappeared*. (MST)

- She feels slightly *weak* but has resumed most of her normal
activities. (LTL)


#### Marking Difficult annotations

The RED schema includes a method for you, the annotator, to highlight
annotations which are particularly difficult to make, or which they
feel fall on the border between different categories.

The ``Difficulty'' marker automatically defaults to ``None'' for
every EVENT created. However, if you feel unsure about any aspect
of the annotation, whether the identification of the EVENT itself
or the properties of it, they can change this marker to ``DIFFICULT'',
simply as an indicator of uncertainty in the annotation. This will
serve to highlight the annotation for further examination.

If you find a particular ambiguity or question leads you to mark ``DIFFICULT''
more than once or twice, you should reach out to your annotation supervisors
for clarification of the rules and policies involved.


###Temporal Expressions

Because we're looking specifically at temporal relations, the next
step of the annotation process is to find and annotate TIMEX3 objects.
These are definitive references to time, and will provide concrete
temporal references throughout the document or section. Examples of
these might be phrases like ``today'', ``tomorrow'', ``24 hours
ago'', ``at this time'' and ``early March\textquotedbl{}. In addition,
specific dates are annotated as TIMEX3 objects as well.


#### Identifying and Annotating TIMEX3s

Our approach to marking TIMEX3s is identical to that used in ISO-TimeML,
and these guidelines are heavily based on the standard established
in \cite{pustejovsky2010iso}.

Unlike with EVENTs, we will not be selecting headwords only. Instead,
syntactically speaking, all TIMEX3 annotations should correspond to
a:
\begin{itemize
- Noun phrase (``this weekend'', ``tomorrow'', ``yesterday'',
``Tuesday'', ``Last May'', ``May 16th'', ``6/9/1985''). 
- Adjective phrase (``two-hour-long'', ``half-hour\textquotedbl{}--as
in ``a half-hour trip'', ``preoperative'', ``post-partum'') 
- Adverbial phrase (``lately'', ``recently'', ``shortly'', ``hourly'',
``intraoperatively''). 
\end{itemize
Importantly, this means that any prepositions which precede (or in
some cases, follow) a temporal expression are to be left unmarked,
\textit{even when they seem to provide additional context for interpreting
the TIMEX3}. For example:

- During **the month of July**, she will come visit.

- From **May 1st** to **the 3rd**, she will refrain from eating
solid food.

- After **tomorrow**, she should be OK to walk with crutches.

- He'll come in for a follow up **two days** after his surgery,
and again **the next week**.

These prepositions (referred to as SIGNALs in ISO-TimeML), although
important in the interpretation of the meaning of the temporal expressions,
provide separate temporal information which will be automatically
extracted later.

Note that post-expression adverbs (often ``ago'') are still captured
in our spans, so:

- Patient s/p lumpectomy **2 yrs ago\

For the most part, if you have two separate temporal expressions,
they'll be two separate TIMEX3s, but two adjacent TIMEX3s which together
specify a single time can be treated as a single span. Look at the
contrast in \Next:

- \a. I'll come by to check on her at **3:30pm Tuesday** \b{.
I'll come by to check on her at **3:30pm** and on **Tuesday\

In (b), we know that the doctor is referring to two different timepoints,
so we mark two TIMEX3s, whereas in (a), the ``3:30pm'' and ``Tuesday''
combine to specify a single timepoint.

The only exception to this rule is when the two temporally connected
TIMEX3s are syntactically separated, as below:

- On **Tuesday**, I'll come by to check on her at **3:30pm**.

- She'll come in for another consult **the day** after **tomorrow**.

In these cases, mark two separate TIMEX3s, even though they combine
to specify one timepoint. The sole exception to this rule comes with
long-form times:

- Mr. Mullins arrived at **5 minutes to five**.

But in medical texts, these are extremely rare.

As one might imagine, TIMEX3s which are separated by a conjunction
are to be treated separately as well:

- She should be fine for discharge on **Tuesday** or **Wednesday**.

- He will come in on **the 1st** and **the 5th** for followups.

Finally, please include in the TIMEX3 span things like time zone identifiers,
time offsets, or other information which provides information which
is helpful in establishing the point of time being discussed.

- He posted **Jan. 5th, 2013 at 6:00pm -700 UTC**\textquotedbl{

- We'll talk at **5pm Mountain\

- She called around **2pm (MDT)\

- His email was sent at **6:59pm (-500)**.

- Our meeting **tomorrow** is at **9pm Eastern/8pm Central**.

- The collapse occurred **at 2am, plus or minus an hour or so**.


#### Annotating TIMEX3 class

Note that in the examples below, if there are multiple TIMEX3s, only
those which are of the indicated class will be marked.


#### DATE

The majority of TIMEX3 annotations you make will be of the class DATE.
DATE represents dates. These can be calendar dates (such as **January
4**) and other verbal expressions which can be mapped to calendar
dates either concretely (such as **Last week**, **This month**, **next
Friday**, or **this time**), or in a more fuzzy sense (**lately**,
**the past**).

- MRI of the brain without and with gadolinium contrast utilizing
tumor followup protocol compared with prior studies of **29, February
2005** and **28, January 2005**.

- His anterior chest rash has not reoccurred since the PCN VK
was discontinued **24-hours ago**.

- At **this time**, we see no reason to discontinue the treatment.

- The last cyclosporine level was 373 in **January**. His dose
was adjusted downward to 300-mg twice-daily. A cyclosporine level
will be repeated on **Friday morning**.

- I stated that if there is no other evidence of any disease recurrence,
in **approximately one-month's time** we would proceed with approximately
six-months worth of adjuvant therapy.

- The form was signed and scanned on **December 29, 2009**.

- I would probably restart her furosemide **tomorrow morning**.

- She came in **a couple months ago**.

- She had an appendectomy **two-to-three years ago**.

- Mr. Zegler was seen in the Hamilton University Medical Center
with Dr. Carr **the middle of December 2009**.

- Carotid artery disease, last checked **greater than two years\
prior.

- After **next week**, we will see where her pain level is.

- **June 6, 2008**, through **October 6, 2008**, treated with
FOLFOX.

As mentioned above, DATE is also used for very generic sorts of TIMEX3s,
where you may not be able to point at a specific day, week, or month
on a calendar, but can still gesture at the overall timeline. So,
for instance, expressions like ``the past'', ``lately'', ``the
future'', or even ``previously'', would be TIMEX3s of the type
DATE:

- She has experienced heavy bleeding in **the past**.

- She complains that she's felt tired **lately**.

- **Recently**, she has had several episodes of syncope.

- He wasn't sure he wanted surgery at **that point**.


#### TIME

TIME is used for specific time points within a day, for instance,
**3:00PM** or **23:45**, and once again can be relative (as in example
\NNext):

- The patient's MRI is scheduled for **5:30pm\

- Following the patient's latest seizure **20 minutes ago**, we
are re-evaluating her medications.

- At **the time of consultation** there is no operative report
or pathology available.

- Surgery will need to be completed by **2:45** to have the biopsy
to the lab sooner.

Put differently, temporal expressions which give minute-by-minute
or hour-by-hour detail are marked as TIME. Day-by-day (or larger)
detail is marked with DATE.


#### DURATION

Sometimes, you will be given a single temporal expression interpreted
as reflecting a span of time, rather than a point. These are things
like ``for **24 hours**'' or ``All of February'', and these are
marked with the class DURATION.

- The patient continuously experienced nausea for **nearly two
weeks**.

- For **the next 12 hours**, we will lower the patient's morphine
drip and then we will re-evaluate his pain.

- Since **August**, she has not had any episodes.

- Patient did well **overnight**.

- During **the last 12 months**, she's been nauseous frequently.

- Since **February 18th**, he hasn't seen his doctor.

- In **the last week**, his pain has significantly worsened.

- He has been doing this for **five years**.

- I stated that if there is no other evidence of any disease recurrence,
in approximately one-month's time we would proceed with **approximately
six-months** worth of adjuvant therapy.

- In **the time** between now and the 15th, she should attend
physical therapy whenever possible.

Note that in \Last, both **now** and **the 15th** would also be TIMEX3s,
but of type DATE.

Remember again that more abstract temporal expressions (``lately'',
``in the past'', ``in the future''), although representing loosely
defined spans of time, are considered DATE rather than DURATION, as
they are predominantly only bounded at the start or the end, not both,
as above.

Finally, remember that two dates can be used to construct a duration,
but, because each represents a single point in time (rather than duration),
both will still be labeled DATE, rather than DURATION:

- From **May 1st**$_{\text{DATE}}$ to **the 3rd**$_{\text{DATE}}$,
she will refrain from eating solid food.


#### QUANTIFIER

Although it may seem odd at first, expressions like ``Twice'', ``four
times'', and ``18 times in the month of May'' are all TIMEX3s.
These are annotated with the QUANTIFIER class.

- The patient vomited **twice** before the surgery.

- We have seen Mr. Lastname **three times** for his ulcerative
colitis.

- On **two to three incidents** she has had blood in the stools.

Note that Quantifier only applies for number of occurrences of an
EVENT, not for quantifiers like ``She has \textit{two} eyes'' or
``She lost \textit{5} units of blood\textquotedbl{}.


#### PREPOSTEXP

Similarly odd, Pre- and Post- expressions (``preoperative'', ``post-exposure'',
``post-surgery'', ``prenatal'', ``pre-prandial'') all actually
designate specific temporal spans (``The time before the surgery'',
``The time after exposure'') related to an implicit EVENT, and thus,
are TIMEX3s, marked with the class PREPOSTEXP. Usage of this TIMEX3
is discussed in more detail in Section \ref{prepostexp}.

- Patient underwent a partial hemicolectomy in July 2009. **Postoperative\
scarring noted during exam.

- The patient exhibits **post-exposure** changes.

These will not always begin with ``pre-'' or ``post-\textquotedbl{}.
Terms like ``intraoperatively'' are PREPOSTEXP as well, as in \Next:

- **Intraoperatively**, there were no difficulties securing his
airway. He received 4 liters of crystalloid, made 300 mL of urine
and estimated blood loss was 50 mL. He received a dose of DDAVP in
the OR out of concern for uremic platelet dysfunction.

And sometimes, you will have bare expressions which clearly express
the PREPOSTEXP meaning, but do not contain the whole expression.

- Pulmonary recommendations for **pre**, **peri** and **postop\
were made.


#### SET

SET is used exclusively in our schema for covering expressions which
give both a quantifier and an interval (like ``Three times weekly'',
``monthly'' or ``1/day'') and represent a frequency. This is different
from QUANTIFIER (``twice'') which only gives a quantifier, and different
from DURATION (``all week'') which only gives a timespan.

Even though most sets could be interpreted as a QUANTIFIER and a DATE/TIME
juxtaposed, we should mark them as a single span (``**twice monthly**''
rather than ``**twice** **monthly**'').

- Will administer Lariam **twice daily**.

- Patient has checked into the ER **roughly three times a month**.

- We will proceed with **weekly** consultations to monitor the
patient's condition.

- Mirtazapine REMERON 7.5-mg tablet 1 tablet by mouth **every
bedtime**.

- Simvastatin ZOCOR 20-mg tablet 1 tablet by mouth **one-time
daily**.

TIMEX3s of type SET should always be TLINKed to EVENTs using the TLINKs
of the type OVERLAP.


#### TIMEX3s vs. Temporal Manner Adverbs

Although TIMEX3s are generally uncontroversial and straightforward,
there is one ambiguity which merits further discussion. First, consider
the below examples:

- He *stopped* the polar bear's *rampage* quickly.

- He *stopped* the polar bear's *rampage* in **twenty
minutes**.

In \LLast, ``quickly'' is quite clearly not a TIMEX3. It is not
placeable on a timeline, it cannot be normalized to a date or time,
and really, it doesn't tell us much about time, but about the stopping.
Compare this to **twenty minutes**, which is clearly temporal. We
know that **twenty minutes** entirely contains the stopping, and that
it refers, on the timeline, to a period of 20 60-second intervals
beginning at the point on which he started trying to stop the rampage.

Compare these to the below sentences, where there's an ambiguity between
reading the highlighted word or words as a straightforward DURATION
TIMEX3, or as a manner adverb indicating speed of action:

- I can write that report up in <5 minutes>. \a. The report will
be ready at the time DOCTIME + 5 minutes. \b{.} When requested, I
can write it up quickly, likely within 5 minutes.

- The party leader claims that Japan ``can arm itself with nuclear
weapons <overnight>'' in response to the continued aggressions. \a.
Japan can arm itself with nuclear weapons in the period of time from
dusk on the day of DOCTIME to dawn the next day. \b{.} Japan can
arm itself, whenever it chooses to, in around 12 hours, or, in a figurative
sense, ``abruptly\textquotedbl{}.

In both \LLast and \Last, the (a) reading inteprets the marked expression
as being DURATION TIMEX3s, which CONTAIN the EVENTs (`write' and `arm'),
and which can be concretely placed on a timeline. In the (b) readings,
the marked expressions are effectively manner adverbs indicating ``quickly'',
which float above the timeline, and thus, are not TIMEX3s at all.

In situations like \LLast and \Last, where both the TIMEX3 and the
manner adverb reads are possible, \textbf{interpret ambiguous DURATION/Manner
Adverb expressions as DURATION TIMEX3s}. This way, we consistently
teach the computer to recognize sequences of text which could be DURATION
TIMEX3s, and we are able to get more temporal information than would
otherwise be possible. Humans, reading the text down the road, can
always understand and interpret as a manner adverb, if it's helpful.


#### DOCTIME and SECTIONTIME Annotation

Because all of these annotations are linking the EVENTs and TIMEX3s
to the time of patient service, it is important that we specify what
that time actually is. When there is information about the time of
writing or publication, we select that time as the DOCTIME. DOCTIME
can be considered a special sort of TIMEX3, and is annotated similarly.

It is worth noting though, that because of the complexities of medical
records or news articles, some sections might have a separate, local
time. These will always include a specific date, which will be marked
not with DOCTIME, but with SECTIONTIME. In these cases, any DocTimeRel
annotations will link to this section-specific time. \emph{If no separate
date is explicitly given for a section, assume that it shares the
overall DOCTIME.

- *head start date=\textquotedbl{}*12/13/2010*'' rev=\textquotedbl{}0002\textquotedbl{}*

Here, the *12/13/2010* would be marked as DOCTIME, as ``start
date'' is the closest thing to the ``Document Time'' that we have
for this record.

- Published *June 15th, 2013* by Jackson Teller-Morrow

Here, obviously, the Doctime is the publication time.

- \textit{UPDATE: *Saturday, February 20, 2010 at 3:34 PM*:
According to Broomfield county sheriffs, the victim of the shooting
has died at St. Joseph Hospital.

Here, *Saturday, February 20, 2010 at 3:34 PM* would be considered
SECTIONTIME, as all that follows it will be true as of this new timestamp.




#### TIMEX3 Normalization

A completely separate annotation pass, occurring after RED annotation
is completed, is TIMEX3 ``normalization'', where the natural language
phrases which constitute TIMEX3s are turned into machine-interpretable
dates and relative times. This process clarifies the referents, meaning,
and connections between TIMEX3s, and is done using a wholly different
schema and set of annotators. As a part of the TIMEX3 normalization
process, we might gain information like the following:

- We'll see her again on **April 18th, 2009** during her **2pm\
appointment \a. **April 18th, 2009** == 04/18/2009 \b{.} **2pm\
== 4/18/2009 1400 *Time Zone Unknown*

- **Next Tuesday** there will be further peace talks. \a. **Next
Tuesday** = ``The next Tuesday after *DocTime*''. \b{.} If
DocTime was 7/6/14, then **Next Tuesday** == 7/8/14

- There was another attack **three weeks after the bombing**.
\a. **three weeks after the bombing** == ``At the time exactly three
weeks after the EVENT *bombing*'' \b{.} If we know that the
bombing was on June 1st, we can then infer that the attack was on
the 22nd.

Note that this sort of normalization handles, in its entirety, the
task of determining and specifying the relative and absolute meaning
of TIMEX3s. Thus, we have no need to make TLINKs which serve only
to demonstrate TIMEX3 meanings, such as:

- I'm seeing her **today**, for the third time in **2013**. \a.
{*}**2013** CONTAINS **today\

- They fought **Friday**, and again **yesterday**. \a. {*} **Friday\
BEFORE **yesterday\

Because relations between TIMEX3s serve only to clarify these relationships
which will be clarified in normalization, we prohibit all TIMEX3 to
TIMEX3 TLINKs.

\color{black


###DUPLICATE marking for repeated spans of text 

Some documents may have significant amounts of copy/pasted or automatically
quoted text. If, as you are annotating, you come across a section
or paragaph which is identical to one previously found (and fully
annotated) in the document, you should \textbf{not} annotate EVENTs,
TIMEX3s, ENTITYs, or any relations in that section or paragraph, and
instead should select the entire paragraph or section which is repeated
and mark with DUPLICATE.


#### Guidelines for finding DUPLICATE text

As to avoid throwing out otherwise good data, DUPLICATE does have
a few hard and fast laws of usage to keep in mind:
\begin{enumerate
- Even if a section or paragraph is repeated several times in a note,
\textbf{the first instance of that section or paragraph which occurs
must be fully annotated}. DUPLICATE is only used for subsequent repetitions. 
- DUPLICATE text must stand off from novel text in some way. An inline
quote or repetition does not qualify as DUPLICATE, even if it is a
verbatim repetition. For example:


- Earlier, Will wrote ``DUPLICATE text must stand off from novel
text in some way''. This is completely accurate, and you should trust
him. He knows these things.


The quoted portion would \textit{not} be eligible for DUPLICATE annotation,
and you would want to reannotate the EVENTs, ENTITYs, and LINKs between.
Were that same sentence presented as an offset quote (as in an email
reply), though, it would be eligible.

- DUPLICATE sections must be exactly duplicate, excepting formatting
changes. Even if two paragraphs differ by only a few words, they are
no longer considered DUPLICATE. Changes to line-breaks, formatting,
or the addition of quoting characters (e.g. ``>'' or ``\textquotedbl{}'')
are not important enough to merit full re-annotation, and you're still
welcome to mark as DUPLICATE.
- DUPLICATE sections must be intentionally duplicated (automatically
or copy/pasted), rather than a part of human-generated text. In a
discussion forum post about cat ownership, many people may say ``I
have a cat.'' (although it's unlikely to be offset from the matrix
text, as discussed above). Multiple people saying the same things,
even if they use the same words, does not constitute DUPLICATE.
\end{enumerate
Remember that DUPLICATE means that a section of text will \textit{not
be annotated at all at any point in the process}, and improper use
(on text that isn't actually duplicated) will rob us of valuable data.
If you're unsure as to whether something is sufficiently similar,
offset, or automated to be DUPLICATE, err in favor of fully annotating
the text.


###Entity Coreference Relations

\label{corefannotation

While you are annotating the EVENT/ENTITY markables pass, we want
you to also annotate all \textquotedbl{}Coreference\textquotedbl{
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


#### IDENTITY and APPOSITION of ENTITIES


#### IDENTICAL 

Two entities have an IDENTICAL relation if they refer to the same
discourse referent. The IDENTICAL relation has several important semantic
characteristics%
\footnote{Following the MUC-7 specifications%
}: 
\begin{itemize
- The relation is symmetrical, i.e., non-directional: (if A is IDENT
to B, then B is IDENT to A). This is different from relations like
WHOLE/PART and SET/MEMBER, which are directional by defition. 
- It is also transitive: if A is IDENT to B and B is IDENT to C, then
A is IDENT to C. . 
\end{itemize
The canonical example of this, and perhaps the bulk of IDENT annotation
work, will be the marking of pronominal antecedents:

- Mr. *Smith*$_{N1}$ complained of a headache. *He*$_{N2}$
also had a sore throat.

Yet in many instances on will be linking together lexical nouns that
refer to the same thing. Two different ways of refering to the same
thing -- like \textquotedbl{}Michele Obama\textquotedbl{}, \textquotedbl{}she\textquotedbl{},
and \textquotedbl{}First Lady\textquotedbl{} in the example below
-- belong in the same chain.

- *Michele Obama*$_{e1}$ is a busy *lady*, *she*$_{e1}$
visits many schools around the country during the year. Just last
week, the *First Lady*$_{e1}$ was in Wisconsin teaching kids
why it is important to eat healthy and exercise \label{Mobama

Yet example \ref{Mobama} also illustrates this question of what to
do with attribution, as in the entity \textquotedbl{}is a busy *lady*\textquotedbl{}.
The fundamental rule we'll follow with this is the following: 
\begin{itemize
- If \textquotedbl{}X is Y\textquotedbl{} is actually showing the equivalence
of the identities of two mentions (such as \textquotedbl{}Clark Kent
is Superman\textquotedbl{}), then these are IDENT. 
- If \textquotedbl{}X is Y\textquotedbl{} asserts a SET/MEMBER relations,
mark it as such. The \textquotedbl{}such as\textquotedbl{} test is
a good metric in this case -- you can restatae the relationship in
\ref{Mobama} as \textquotedbl{}busy ladies such as Michele Obama\textquotedbl{},
but one can't say \textquotedbl{}Supermen like Clark Kent\textquotedbl{} 
- If \textquotedbl{}X is Y\textquotedbl{} doesn't show Y as a set, and
the two described entities are the identical, but the attribute is
a role (\textquotedbl{}Joe is the vice president\textquotedbl{}),
a defined role that is not a separate referent (\textquotedbl{}Joe
is the tallest man in the room\textquotedbl{}), then use BRIDGING. 
- If \textquotedbl{}X is Y\textquotedbl{} is very predicative (the Y
is less of a separate referent and more of an attribute of X) and
cannot be framed as a SET/MEMBER or BRIDGING relationship, then do
not mark any relation at all. 
\end{itemize

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

- My *friend* who works there, *John Smith*, makes bread.
\label{apposlong

- \Tree [.S [.NP [.NP [.NP [.DT my ] [.NN friend ] ] [.RelativeClause who works there ]] [.NP John Smith ] ] [.VP makes bread ]]

Unlike IDENT chains, which may contain many different referents in
the same relationship, this is a relationship with only two points.
The leftmost term must always be the HEAD and the right mention is
the ATTRIBUTE, except when one of the two phrases is a proper name,
in which case the proper name must be the HEAD regardless of position:

- The U.S. *President*$_{\textsc{attribute}}$, *Barack
Obama*$_{\textsc{headsc}}$

We will only consider the Head of an APPOSITIVE relation as eligible
to participate in other relations with entities outside the APPOSITIVE
relation, not the ATTRIBUTE.

There are a number of specific nominal constructions that we will
count as APPOSITION. One is any sequence of titles -- either in normal
speech, or during the description of titles as in:

- *Smith*$_{\textsc{head}}$, MD, FFF, *Pathologist*$_{\textsc{attribute}}$.

Unit conversions are also considered appositives.

- *37.00C*$_{\textsc{head}}$ (*98.60F*$_{\textsc{attribute}}$)

In some cases, APPOSITIVES may include multiple entities. In the case
that there are more than 2 markables in the apposition, we will nest
these using multiple, separate APPOS relations.

- *AUTHOR*: Company *President*, *Mr. Johnson*

We would create one APPOSITIVE in which *Mr. Johnson* would be
the Head, and *President* would be the Attribute. Then, we would
create a second APPOSITIVE with *President* as the Head, and *AUTHOR*
as the Attribute. In these cases, we still would only include the
HEAD of the first APPOSITIVE in other relations, thus, *AUTHOR*
and *President* would not be eligible for inclusion in any other
relation. You probably noticed that due to the nature of the nesting
and the specificity of the proper name *Mr. Johnson*, the nesting
worked right-to-left instead of left-to-right. We could not have had
*President* be the attribute of both APPOSITIVE relations. The
proper name takes precedent in determining APPOSITIVE phrases with
multiple ENTITYs, as it is more specific on the specificity hierarchy:
\\


\centerline{Proper noun > pronoun > definite NP > indefinite specific
NP > non-specific NP

If both ENTITYs have the same level of specificity, select the left-most
ENTITY as the head.


#### \label{bridgingsection}WHOLE/PART

Two entities exist in a WHOLE/PART relationship if one can be thought
of as part of the other, larger composite entity. These can be simple
or more abstract:

- The *hand*$_{part}$ was broken when the boulder fell on
his *arm*$_{whole}$.

Any number of PARTs may be included in a WHOLE/PART relation, although
only one Entity is allowed to fill the WHOLE slot.

- I didn't include enough *flour*$_{part}$ in this *cake*$_{whole}$,
and used too much *sugar*$_{part}$.

As with the CONTAINS-SUBEVENT TLINK, this relation can only be used
for cases of compositionality, i.e. narrow readings. In order for
an entity to be Part of another, it must be 100\% contained by the
Whole, and compositionally part of it. Thus, the following examples
do not contain any WHOLE/PART relations:

- *Mt. Everest* lies on the border between *China* and
*Nepal*.

- In the *house*, there are several *visitors*.\label{visitorsinhouse

Note that WHOLE/PART relationships are essentially \textbf{hierarchical},
in that they may theoretically have a whole chain of relationships
(a hair is part of a dog, a dog is part of a pack, spatial relations,
such as:

- We saw the *White house* while in *D.C.*.\label{dchouse

The difference between \ref{visitorsinhouse} and \ref{dchouse} reveals
a difficult boundary case that you will have to ponder -- what counts
as \textquotedbl{}compositionally part\textquotedbl{} of a thing.
This is particularly salient when the \textquotedbl{}whole\textquotedbl{
is a larger spatial entity such as a city, county or country. When
in doubt, remember this \textquotedbl{}compositionality\textquotedbl{
idea. If the removal of the potential \textquotedbl{}part\textquotedbl{
would have the potential of changing the nature of the \textquotedbl{}whole\textquotedbl{},
even a slight bit, then one might consider it compositional and use
WHOLE/PART. If, in contrast, the part is merely temporarily or arbitrarily
located in the space of the other item, do not use WHOLE/PART.

\vspace{0.25cm
 \fbox{ %
\begin{tabular}{p{0.6in}p{14cm}
\includegraphics[width=0.5in]{warning} \\
\textbf{Caution!}  & \raisebox{4mm}{%
\parbox[c]{14cm}{%
\vspace{2mm
\textit{Note that while IDENT, SET/MEMBER and BRIDGING will also be
used to mark EVENTS, WHOLE/PART is only for ENTITIES. Relationship
that you are tempted to mark as WHOLE/PART should probably be CONTAINS-SUBEVENT
or SET/MEMBER instead. }%
}}\ \
\tabularnewline
\end{tabular}} \vspace{0.25cm



#### \label{sub:SET-MEMBER}SET-MEMBER

A SET-MEMBER relationship exists when one entity or event can be thought
of as one or several members of a larger group. SET-MEMBER relations
can be between ENTITIES or between EVENTS.

- The *trustees*$_{S}$ have to sign off on the ordinance
before we proceed; however, the trustee *Mr. Gamal*$_{S}$ says
agreement has been hard to come by.

- *Patients*$_{S1}$ with *cancer*$_{S2}$ are advised
to avoid this medication. Our *patient*$_{M1}$ has kidney *cancer*$_{M2}$
and lung *cancer*$_{M2}$, so we will not prescribe it. \a. Notice
also that *Our* and *we* are in an IDENTICAL relation.

- Patient has two *arms*$_{S}$. Her left *arm*$_{M}$
is scarred.

You should note that in most examples of SET-MEMBERship, the MEMBER
will be a count noun, but in some cases, the MEMBER can itself be
a group or another set.

- *Terrorists* are among the most dangerous *criminals*,
and *Al Nuri* is perhaps the most dangerous *terrorist* alive.
\a. *Criminals* SET/MEMBER *Terrorists* \b{.} *Terrorists*
SET/MEMBER *Al Nuri*, *Terrorist*

Any number of MEMBERs may be included in a SET/MEMBER relation, although
only one Entity is allowed to fill the SET slot.


#### BRIDGING

If you are unable to use one of the previously discussed links, but
it is apparent that some sort of link exists which entails that the
events have some sort of link, then use the BRIDGING relation.

There are a few specific cases in which BRIDGING can (and should)
regularly be used:
\begin{enumerate
- Links of asserted identity, where the assertion is itself questioned
or questionable: 
\end{enumerate
- *John* was arrested last night, as authorities claim *he*
is the *killer* of a local cobbler, found Monday. \a. *John*
IDENTICAL *he* \b{.} *John* BRIDGING *killer*

- *Grigory Kuznetsov*, long thought to be *``Rosebud''*,
a key Cold War CIA asset, died Friday. \a. *Grigory Kuznetsov*
BRIDGING *``Rosebud''*

See Section \ref{judgement} for more information about this usage.

- She had a small stroke in *recovery* from her *colectomy*.
\a. *colectomy* BRIDGING *recovery*

Temporally-grounded IDENTITY links which are no longer valid. For
instance:

- *Ratzinger* was *Pope* until his retirement in 2013.
\a. *Ratzinger* BRIDGING *Pope*

- *Greg Bear*, former *Head* of the National Croquet society,
died Wednesday. \a. *Greg Bear* BRIDGING *Head*

Because BRIDGING is intended as a last resort, any contexts (beyond
those above) in which an annotator is consistently using bridging
should be passed up the chain, so that a better way to handle those
cases can be found.


#### General Guidelines for Annotating Coreference

\label{corefguidelines


#### Never link EVENTs to ENTITIES (except with BRIDGING)

In all coreference relations (IDENTICAL, APPOSITIVE, WHOLE/PART, AND
SET-MEMBER), Entities can be linked to Entities, and Events can be
link to Events, but Entities and Events will never be linked within
the same coreference relation. If you encounter an occasion where
you are tempted to do this, check that your Entity is not actually
an Event, or that your Event is not actually an Entity, as the case
may be.

Occaisionally one will encounter an ENTITY and an EVENT which are
essentially two facets of the same complex type (cf Pustjovsky XXXX).
Usually we strongly bias towards EVENTs, but this will occaisionally
occur, and the two should be linked using BRIDGING. 
\begin{example
The company says it stores your *\textsubscript{entity} texts*
on its server for thirty days after you *\textsubscript{event
text* them

texts BRIDGING text
\end{example

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

- *I*$_{M1}$ met with the *patient*$_{M2}$ today. *We*$_{S1}$
discussed treatment options for *her*$_{M2-1}$ cancer. *We*
also reviewed in *our*$_{S2}$ discussion the results of *her*$_{M2-2}$
recent CT-scan. *My*$_{M1}$ recommendation is adjuvant chemotherapy.
\a. SET *We*$_{S1}$: MEMBERs *I*$_{M1}$, *patient*$_{M2}$,
*her*$_{M2-1}$ \b{.} SET *our*$_{S2}$: MEMBERs *her*$_{M2-2}$,
*My*$_{M1}$

In this example, *I*$_{M1}$ and *My*$_{M1}$ are IDENTICAL;
*patient*$_{M2}$, *her*$_{M2-1}$, and *her*$_{M2-2}$
are IDENTICAL; and *We*$_{S1}$, *We*, and *our*$_{S2}$
are IDENTICAL.


#### Use SET/MEMBER to define groups of people

The members of groups of people (i.e. *we*, *they*, the *board*
of directors, etc.) are always annotated with SET/MEMBER relations,
as in \Last, not WHOLE/PART.


#### Don't link ACTUAL and GENERIC items

In analogy with the principle for not TLINKing HYP/GEN to ACT/UNCERTAIN
events, ACTUAL and GENERIC items can never be in an IDENTICAL, APPOSITIVE,
or WHOLE/PART relationship. They can, however, be SET/MEMBER, as in
\Next:

- *I* discussed with *Mrs. Ambry*$_{ACTUAL}$ the results
of a local clinical trial in which *patients*$_{GENERIC}$ with
*cancer*$_{GENERIC}$ recovered successfully on the *drug*
without reoccurrence. Given *her* colon *cancer*$_{ACTUAL}$
and the success of the *drug*, *I* recommend *it*. \a.
SET *patients*: MEMBER *Mrs. Ambry* \b{.} *Mrs. Ambry*
IDENTICAL *her* \c{.} SET *cancer*$_{GENERIC}$: MEMBER *cancer*$_{ACTUAL}$
\d{.} *I* IDENTICAL *I* \e. *drug* IDENTICAL *drug*,
*it*


#### Identifiers are people too

Email addresses (and other person-specific identifiers) can be linked
to their referent humans using IDENTICAL or APPOSITIVE.

- You should contact *Bill Franklin* for more information.
*He*'s *bill.franklin@hotmail.gov* \a. *Bill Franklin*
IDENTICAL *He*, *bill.franklin@hotmail.gov*

- *George Maddox* (*exampleguy6969@hotmail.gov*) should
be able to help you out. \a. *George Maddox* APPOSITIVE *exampleguy6969@hotmail.gov*

- Did you ask *Herbie* (*prairiedog1564* on here)? *He*
might know! \a. *Herbie* APPOSITIVE *prairiedog1564*, *He*

- Ms. *Jenny Tutone* (SSN: *867-53-0900*) was arrested
last week. \a. *Jenny Tutone* IDENTICAL *867-53-0900*

Phone numbers are not person-specific, and thus, are not eligible
for these relations.


#### Avoid annotating coreference links based solely on your personal
evaluation or judgement

\label{judgement} Occasionally, authors (or context) will suggest
coreference or identity, or will explicitly state the uncertainty
of coreference.

- *Hans Holbein*, a local *man*, was arrested in connection
with the murder of a local blacksmith. The *alleged killer* is
being held without bond. The *killer* reportedly had a large tattoo
of a squid on *his* face, similar to the one present in *Mr.
Holbein's* booking photo. \a. *Hans Holbein* IDENTICAL *man*,
*alleged killer*,*Mr. Holbein's* \b{.} *killer* IDENTICAL
*his*

In this example, all that we can be sure of is the two IDENTICAL chains
above. It is incredibly tempting, especially given the seemingly irrefutable
squid, to jump to conclusions and merge (a) and (b) into one massive
IDENTICAL chain. However, in our schema, all ENTITYs are different
until proven IDENTICAL, and Mr. Holbein deserves a fair trial.

However, there is irrefutably \textit{some sort of relationship} between
Mr. Holbein and the killer. Whether this relationship is of legal
identity, actual identity, or simply a mistaken prosecution by an
over-zealous district attorney, we cannot know, but we know that there
certainly is one. To mark an ambiguous relationship like this, we
use the non-specific BRIDGING link:

- *Hans Holbein*, a local *man*, was arrested in connection
with the murder of a local blacksmith. The *alleged killer* is
being held without bond. The *killer* reportedly had a large tattoo
of a squid on *his* face, similar to the one present in *Mr.
Holbein's* booking photo. \a. *Hans Holbein* IDENTICAL *man*,
*alleged killer*,*Mr. Holbein's* \b{.} *killer* IDENTICAL
*his* \b{.} *killer* BRIDGING *Mr. Holbein's*

By doing this (alongside the other necessary annotations), we've established
two clear IDENTICAL chains, and made clear that there is a link between
them, even though the nature of that link is unclear in the text.

Here's another example of a relation based purely on judgement:

- In response to the bombing, the US has dispatched agents to
*Yemen*, *Somalia*, *Norway* and *South Sudan*. An
official in a later conference stated that terrorists often seek out
*countries* with little law and order as a safe haven.

Here, it's tempting to use one's knowledge of the world to SET/MEMBER
*countries* with *Yemen*, *Somalia*, and *South Sudan*
(and to likely exclude *Norway*). However, no such relation is
given in the text, and therefore, one should not be created.

Finally, there are cases where a relation might be unclear in the
text, and recoverable only by guesswork. For instance, imagine a series
of discussion forum posts like the below (which have been adapted
from an actual document, and in no way represent the political views
of anybody associated with RED):

- *Barack Obama* was born in Nigeria, he's not American, and
his presidency is illegal. That's why *he* loves *immigrants*!
\\
 <Post by: TheyTookOurJarbs Date: 4/15/12 6:56pm> \\
 It's terrible, I hate these illegal *immigrants* taking jobs
from hard-working *Americans*. \a. *Barack Obama* IDENTICAL
*he* \b{.} *immigrants* SET/MEMBER *immigrants* (representing
the fact that illegal immigrants are a subset of immigrants)

In addition to the (uncontroversial) relations above, there are three
pitfalls, all based on external knowledge.
\begin{enumerate
- Americans SET/MEMBER Barack Obama


This is fairly uncontroversial in most circles, but is contradicted
in the text. We cannot mark it based on our understanding of the world.

- Americans SET/MEMBER immigrants, immigrants


Again, this is a matter of perspective, and should not be marked without
support in the text.

- immigrants SET/MEMBER Barack Obama


That Obama is an illegal immigrant is strongly implied by these posts.
However, it's not explicit, and therefore, we cannot mark it.

\end{enumerate
So, again, in summary, your annotations need to be sourced from the
text itself, rather than from your knowledge of the entities, people,
and places involved, and asserted IDENTITY links can be made using
BRIDGING.


#### Identity Annotation for very broadly GENERIC entities

\label{vbroadgens

Some set/member relations are so general that they define huge, all-encompassing
sets. This is most clear when considering terms such as \textquotedbl{}everything\textquotedbl{},
which may sometimes be worth marking yet which we don't want to mark
as containing all other entities.

This is different from the question of entities in which set-membership
is in doubt; instead, these are cases in which the set membership
is clear but somewhat trivial. For the sake of tractability (and your
own sanity as annotators), a small set of extremely broad GENERIC
instances will be defined as being out of the scope of our annotation.

Terms to omit from SET/MEMBER annotation: 
\begin{itemize
- \textquotedbl{}Everyone\textquotedbl{}, \textquotedbl{}people\textquotedbl{},
and generic \textquotedbl{}you\textquotedbl{}: When these are used
in the truly broad sense (so that they encompass all persons mentioned
in the text), omit them from annotation. 
- generic \textquotedbl{}we\textquotedbl{}, \textquotedbl{}everyone\textquotedbl{},
and \textquotedbl{}people\textquotedbl{}, when they do not describe
a document-specific set like \textquotedbl{}americans\textquotedbl{
but rather some broader generic set like \textquotedbl{}humanity\textquotedbl{},
does not get set/member relations. 
- \textquotedbl{}someone\textquotedbl{}, \textquotedbl{}anyone\textquotedbl{},
\textquotedbl{}one\textquotedbl{}: These do not entail set/member
relationships between themselves and the possible candidates. 
\end{itemize

\subsubsection*{IDENT over generic you, one, etc.

We do, however, want to grab identity relations with very generic
terms, and especially want identity relations with terms like \textquotedbl{}you\textquotedbl{}.
The question that arises -- especially with terms like \textquotedbl{}you\textquotedbl{},
\textquotedbl{}one\textquotedbl{}, etc. -- is whether these should
all be contained within the same IDENT chain.

Many times with GENERIC \textquotedbl{}you\textquotedbl{}, as with
\textquotedbl{}somebody\textquotedbl{}, we initiate a possible world
that would be true for any member of the set, and continue that hypothetical.
In such a hypothetical, we want an identity chain between the same
mentions. Put more concretely; given two mentions of generic \textquotedbl{}you\textquotedbl{},
you can usually replace the first with either \textquotedbl{}somebody\textquotedbl{},
\textquotedbl{}one\textquotedbl{} or \textquotedbl{}anyone\textquotedbl{
in English. In that case, the question is whether later mentions can
be replaced with pronoun such as \textquotedbl{}they\textquotedbl{},
\textquotedbl{}he\textquotedbl{} or \textquotedbl{}she\textquotedbl{
without changes in the implied meaning. If so, they deserve to be
IDENT in the same chain; otherwise they are probably different. So
for example:

- If you get out on parole, what happens then, and how long does
it last? (and, specifically, who takes you home once you get out of
jail, or do you just get turfed out and expected to check in with
your parole officer the next day?).

rephrasing attempt:

- If \textbf{someone} gets out on parole, what happens then, and
how long does it last? (and, specifically, who takes \textbf{them
home once \textbf{they} get out of jail, or do \textbf{they} just
get turfed out and expected to check in with \textbf{their} parole
officer the next day?).

In consider two other sentences, presumably from the same document.
While these both fit into the idea of GENERIC you, the second doesn't
pass this same \textquotedbl{}hypothetical somebody\textquotedbl{
test:

- If you choose not to vote, then you choose to give your opponents
all the power. This is another case of \textquotedbl{}well what did
you bloody well expect to happen\textquotedbl{}?

the rephrasal attempt seems to change the meaning in this one, and
thus these should be different IDENT chains:

- If \textbf{someone} chooses not to vote, then \textbf{they
choose to give \textbf{their} opponents all the power. This is another
case of \textquotedbl{}well what did \textbf{they} bloody well expect
to happen\textquotedbl{}?

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%



###Testing Your Understanding


#### Testing your Understanding

Since this can be a hard distinction to make, the following lists
a number of example sentences. Apply the linguistic tests above and
try to figure out what the entities and events are in the data. do
not worry for now about which words to annotate, just focus on which
referents and events deserve some sort of annotation (Answers in the
footnote \footnotemark).

- \label{test1}Mr. Stone reported that he had difficulty swallowing
and shortness of breath.

- \label{test2}The sectarian violence continued to spread in
the northern city of Tikrit.

- \label{test3}She took her car to a garage to change the oil.

\footnotetext{You should have found the following ENTITIES: Mr. Stone
\ref{test1}, he \ref{test1}, northern city of Tikrit \ref{test2},
She \ref{test3}, her \ref{test3}, car \ref{test3}, garage \ref{test3},
and oil \ref{test3}. You should also have found the following EVENTs:
reported \ref{test1}, swallowing \ref{test1}, shortness of breath\ref{test1},
sectarian violence \ref{test2}, continued \ref{test2}, spread \ref{test2},
took her car \ref{test3}, change \ref{test3}. Consult the next section
for how their headwords will be annotated.

The suspect *struck* the police officer several times before *running*
away.

- The People's army *attacked*, triggering a massive *reprisal*.
\begin{itemize
- For coordinated heads, both of the heads will be labeled as separate
elements and annotated separately. (e.g., ``They *shipped* and
*unloaded* the cargo\textquotedbl{}; ``Potential *carcinoma*
or *polyp*'', etc.)
\end{itemize
- We also discussed *some*$_{S2-M1}$ of the *toxicities*$_{S1}$
of fluoropyrimidine-based chemotherapy, including *fatigue*$_{M2}$,
*nausea*$_{M2}$, and *infection*$_{M2}$. \a. SET *toxicities*$_{S1}$:
MEMBER *some*$_{S2-M1}$ \b{.} SET *some*$_{S2-M1}$: MEMBERs
*fatigue*$_{M2}$, *nausea*$_{M2}$, *infection*$_{M2}$

- *Many*$_{M1}$ of the *aftershocks*$_{S1}$ were strong
enough to collapse already-weakened buildings. \a. SET *aftershocks*$_{S1}$:
MEMBER *Many*$_{M1}$

Occasionally, quantifying phrases indicate a WHOLE/PART relation,
as in \Next.

- a *chain*$_{S1}$ of fault *lines*$_{M1}$ and *volcanoes*$_{M2}$
known as the *Pacific* ``*ring*$_{W1}$ of *fire*$_{P1}$\textquotedbl{
\a. SET *chain*$_{S1}$: MEMBERs *lines*$_{M1}$, *volcanoes*$_{M2}$
\a. WHOLE *ring*$_{W1}$: PART *fire*$_{P1}$

Notice that the ``chain of fault lines and volcanoes'' is SET/MEMBER,
whereas ``ring of fire'' is WHOLE/PART. This is because the fault
lines and volcanoes are MEMBERs of the chain in a way in which ``fire''
is not a MEMBER of the ``ring\textquotedbl{}. Instead, ``fire''
is what the ring is physically made of, and is therefore compositionally
a part of the ``ring\textquotedbl{}.

Coreference relations such as SET/MEMBER and WHOLE/PART are discussed
in more depth in Section \ref{corefannotation}.


\paragraph{Medical Test Results, Measurements, and Labs

When discussing a test and its results, we still maintain our policy
of marking the syntactic head.

Here, the EVENT is the CT scan itself. In medical annotation, the
finding of ``normal'' is captured by comparison with other non-RED
annotations that link tests and result.

- The CT *scan* was normal.

- Her *BUN* is 9 mg/dL.

Here, the only EVENT is the test itself (*BUN*), and the finding
(9 mg/dL) is captured by a later step.

The same goes for formulaic measure sections:

- *Height*=178.60 cm,

- *Weight*=91.90 kg,

- *Systolic*=160 mm/Hg,

Here, we only capture the measure itself, and not the value.

The only exception to not capturing the test result is when the result
of a test, lab, or exam is the diagnosis (or suggestion) of another
disorder, disease, or disorder, as below:

- The CT *scan* *showed* probable *adenocarcinoma*.

- Her *CBC* *indicates* *thrombocytopenia*.

Here, the test is an EVENT, as is the revelation itself, as well as
the diagnosis, and all merit inclusion on the timeline. Put differently,
a measure isn't a separate EVENT from the test which indicated it,
but a diagnosis or disease shown by a test is. Note that *showed*
and *indicates* are both EVENTs in their own right, of TYPE EVIDENTIAL.

Outside of the medical domain, all such EVENTs are marked:

- Before the *trial*, the prosecution *argued* that the
killer's mental *status* was *normal*.

- *Readings* of tritium in seawater taken from the bay near
the crippled Fukushima nuclear plant has *shown* 4700 *becquerels*
per liter.


##Event Relations Pass: Linking Events Together

%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%


The next step of RED annotation is to take those EVENTs, ENTITYs,
and TIMEX3s annotated in EVENT annotation and mark the temporal, aspectual,
identity, and bridging relations between them.

Although these relationships may end up forming complicated structures
of meaning, each relationship is a single link which will be presented
in the form:

- *EVENT1* RELATION *EVENT2*

Where RELATION is any of a range of relation types, such as BEFORE,
CONTAINS, IDENTICAL, or PART-WHOLE. These types are described in detail
in Section \ref{tlinktypes}.

To give a realistic example, imagine the following sentence:

- The patient was to meet with oncology this month.

The EVENT *meet* is clearly related to the TIMEX3 **this month**,
because *meet* will occur during **this month**, giving you more
specificity than the followup just occurring after document time.
That is one kind of relationship -- temporal containment. So here,
you would create a TLINK annotation, insert *meet* into the ``target''
slot, **this month** into the ``source'' slot, and select CONTAINS
as the relation. By doing so, **this month** is established as a narrative
container anchor, which may contain additional EVENTs later on in
the note. So, the finished annotation would look like:

- The patient was to meet with oncology this month. \a. **this
month** CONTAINS *meet*

This is not the only kind of link, however. In this annotation task
we are attempting to get not only a sense of the timeline of events,
but to also understand which events cause other events, which events
are part of larger events, and a range of other relationships. Making
such an imposing task viable requires the use of a concept called
``narrative containers.\textquotedbl{

%%%% NARRATIVE CONTAINERS %%%%



###Narrative Containers

Our reasoning for using narrative containers is simple: Temporal relations
annotation is prone to never-ending webs of temporal links between
different EVENTs, because, simply put, every EVENT that ever happened
in the history of the universe is part of a valid temporal relation
with every other event.

As an extreme example, this (somewhat unlikely) paragraph could result
in the following temporal links:

- Napoleon was exiled to Elba in 1814. This has little to do with
Mr. Chen's rash and subsequent leg pain, which both developed after
his surgery in 2009. \a. **1814** CONTAINS *exiled* \b{.} **2009\
CONTAINS *surgery* \b{.} **2009** CONTAINS *rash* \b{.
**2009** CONTAINS *pain* \b{.} **1814** BEFORE *surgery*
\b{.} **1814** BEFORE *rash* \b{.} **1814** BEFORE *pain*
\b{.} *exiled* BEFORE *pain* \b{.} *exiled* BEFORE *rash*
\b{.} *exiled* BEFORE *surgery* \b{.} *exiled* BEFORE
**2009** \b{.} *surgery* BEFORE *rash* \b{.} *surgery*
BEFORE *pain* \b{.} *rash* BEFORE *pain*

As we can see, not only is the temporal linking of Napoleon's exile
to each modern EVENT absurd, but a number of the TLINKs described
above are accurate, but unsatisfying, simply existing ``to complete
the picture\textquotedbl{}. Moreover, one may see that as as the number
of events increased, the number of relationships you might have to
make would increase exponentially.

This is a reason for adopting the concept of the narrative container,
discussed extensively in Pustejovsky and Stubbs 2011 \cite{DBLP:conf/acllaw/PustejovskyS11
as well as in Styler et al 2014 (\cite{Styler:2014aa}). A narrative
container can be thought of as a temporal bucket into which an EVENT
or series of EVENTs may fall. These narrative containers are often
represented (or ``anchored'') by dates or other temporal expressions,
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

Using narrative containers, we can return to the example above, but
simply put all of the items into two temporal buckets, **1814** and
**2009**, and then \textit{infer from the known relation between the
containers} the relations between the items which reside within them:

- Napoleon was exiled to Elba in 1814. This has little to do with
Mr. Chen's rash and subsequent leg pain, which both developed after
his surgery in 2009. \a. **1814** CONTAINS *exiled* \b{.} **2009\
CONTAINS *surgery* \b{.} **2009** CONTAINS *rash* \b{.
**2009** CONTAINS *pain* \b{.} *surgery* BEFORE *rash*
\b{.} *rash* BEFORE *pain*

In doing so, we can cut the number of required TLINKs in half, while
still capturing all of the information of the fully-expanded version
using straightforward temporal inference.

Note that we have not made the TLINK: **1814** BEFORE **2009**. TIMEX3s
will never be linked together; this information is captured in post-processing
of your annotations.


#### Expressing Narrative Containers

You should think of all documents as starting with three implicit
narrative containers, marked by DocTimeRel. One bucket contains all
EVENTs which occur BEFORE the document time, one contains all EVENTs
which occur AFTER the document time, and one contains all EVENTs which
overlap the document time. However, there can be many more narrative
containers in a given note than just ``Before DOCTIME'', ``Overlapping
DOCTIME'', and ``After DOCTIME\textquotedbl{}. Take, for example,
this note:

\textbf{\textit{This could use a nice general-domain example. Annotators,
please keep an eye out for a good example sentence and send it along
to your supervisor!}

- \label{manycontainers} \myul[yellow]{The patient recovered
well after} \myul[red]{her first surgery on December 16th to remove
the adenocarcinoma}, although \myul[orange]{on the evening of January
3rd she was admitted with a fever and treated with antibiotics}.
\myul[blue]{Today we reviewed the pathology results and the results
of} \myul[yellow]{her follow-up CT}. She will have her \myul[green]{second
surgery in three weeks}, followed by a \myul[black]{third surgery
on April 19th which will involve both additional resection as well
as the taking of additional biopsies}.

In example \Last, one may think of it as having six narrative containers,
the contents of each marked again with differently colored underlines.
The first surgery occurred entirely within the December 16th container
(the anchor TIMEX3), the fever, admission, and antibiotics occurred
on January 3rd (and within that container), the followup CT and her
recovery occurred at an ambiguous point between the surgery and the
DOCTIME (the during-visit container), the second surgery occurs three
weeks from the DOCTIME, and the final container involves everything
occurring on April 19th (the surgery, resection, and taking of biopsies).
We also need to know that, for instance, the April 19th surgery will
happen AFTER the surgery in three weeks. These containers and their
events are shown in list format in Table 1.

\begin{table
\begin{centering
\begin{tabular}{|llllll|
\hline 
\myul[yellow]{BEFORE DocTime}  & \myul[red]{Dec 16th}  & \myul[orange]{Jan 3rd}  & \myul[blue]{OVERLAP DocTime}  & \myul[green]{In 3 Weeks}  & \myul[black]{Apr. 19th} \tabularnewline
recovered  & surgery  & admitted  & reviewed  & 2nd surgery  & 3rd surgery \tabularnewline
follow-up CT  & remove  & fever  &  &  & resection \tabularnewline
 &  & treated  &  &  & biopsies \tabularnewline
\hline 
\end{tabular}\caption{Narrative containers and EVENTs in \ref{manycontainers}

\par\end{centering

\label{180table} 
\end{table


Again, the critical function of narrative containers is that using
them conscientiously allows us to infer TLINKs, rather than forcing
annotators to explicitly mark them. Here, there is no need at all
to explicitly mark that, for instance, *fever* is before *resection*,
because we know that the fever happened on Dec 16th, the resection
happened on April 19th, and that December 16th is before April 19th.
With explicit grouping of EVENTs in this way, we can easily infer
the links between them with minimal annotator effort.

As you annotate, it is critical to keep this notion of narrative containers
in mind, as to avoid wasting effort marking temporal relations which
are already captured straightforwardly.


#### EVENTs as Containers

\label{eventcon

So far, we've been discussing temporal expressions (TIMEX3s) as providing
the boundaries of narrative containers, but EVENTs themselves can
provide boundaries too. Take this example:

- During the \myul[red]{surgery}, \myul[blue]{the patient experienced
another MI, and repeated bouts of tachycardia}.

In example \Last we can see that the surgery itself is a container,
containing an MI (myocardial infarction or ``heart attack'') as
well as tachycardia. In this case, for the temporal structure of the
note to really be captured, both the MI and tachycardia need to be
linked to the surgery.

The manner in which they are linked brings up the important distinction
between temporal containment and event-subevent containment. We invite
annotators to think of narrative containers as temporal buckets, but
it is notable that while the temporal span of ``surgery'' contains
all of the events going on in the universe during that period of time,
some events could be characterized as being subevents of that surgery
-- sharing participants, locations, and consequences with the larger
event.

We encode that distinction by expressing narrative containers using
two different relationships, CONTAINS and CONTAINS-SUBEVENT. CONTAINS
is used when the only link between two events is that of temporal
span, and CONTAINS-SUBEVENT is used when both temporal containment
and an event-subevent relationship pertain to the pair. Take, for
example, the below paragraph:

- \label{cbcexample} \myul[red]{During her surgery, Mrs. Hayes
showed some adhesions and scarring in the abdominal cavity}. \myul[blue]{She
did show some bleeding at the incision during her subsequent CT scan}.
\myul[green]{For her followup, we will take a CBC and remove her
stitches.

Here, we have three narrative containers, the surgery, the CT scan,
and the followup, with no TIMEX3s at all, all shown in Table 2, below.
The containment relations in this example are as follows:

\a. *surgery* CONTAINS *adhesions* \b{.} *surgery* CONTAINS
*scarring* \c{.} *scan* CONTAINS *bleeding* \d{.} *followup*
CONTAINS-SUBEVENT *CBC* \e. *followup* CONTAINS-SUBEVENT
*remove*

The *CBC* and the stitches being *removed* are related to
*followup* with CONTAINS-SUBEVENT, as they are compositionally
part of the larger event (*followup*) that contains them. When
one event temporally contains another, you may generally default to
CONTAINS. CONTAINS-SUBEVENT is to be treated as a special case exclusively
used for event-subevent relations (which will never be the case when
relating TIMEX3s to EVENTs).

*adhesions* and *scarring* are CONTAINed by the *surgery*,
the procedure which revealed them, according to the rule as explained
in \ref{revelation}.

Another aspect to consider, in addition to marking EVENTs that are
contained within the surgery, CT, or followup, is that we will also
need to explicitly mark the relation between those three EVENTs. So,
in addition to the containment links (e.g. *surgery* CONTAINS
*adhesions*), we will need to create two TLINKs to relate the
containers, *surgery* BEFORE *CT*, and *CT* BEFORE *followup*.

Once this is completed, inference can easily take place across the
containers, and the full benefits of our narrative container approach
can be reaped.

\begin{table
\centering{}\label{155table} %
\begin{tabular}{|lll|
\hline 
\myul[red]{During Surgery}  & \myul[blue]{During CT}  & \myul[green]{During Followup} \tabularnewline
adhesions  & bleeding  & CBC \tabularnewline
scarring  &  & remove \tabularnewline
\hline 
\end{tabular}\caption{Narrative containers and EVENTs in \ref{cbcexample}
\end{table



#### Single-bounded narrative containers

Although so far we've been discussing the idea of containment (and
thus, the CONTAINS and CONTAINS-SUBEVENT TLINKs) when discussing narrative
containers, one can still imagine and annotate narrative containers
which are bounded only on one side. Take, for instance, the below
example:

- Immediately after her *surgery*, the patient began to *vomit*
and developed a high *fever*.

In this case, the *surgery* forms one temporal boundary for the
vomiting and fever, and as such, can be thought of as anchoring a
one-sided narrative container. In this case, we would say that both
*vomit* and *high fever* have a BEGINS\_ON TLINK relation
to the *surgery*. Although somewhat conceptually different, narrative
container relationships can very easily stem from BEGINS\_ON, ENDS\_ON,
and even BEFORE, and the metaphor of the narrative container is still
useful in annotating these situations.


#### Nested Narrative Containers

\label{russiandolls

Sometimes, you will find yourself with a situation where a narrative
container seems to, itself, belong inside another narrative container.
Here's an example with three levels of nesting:

\textbf{\textit{This could use a nice general-domain example. Annotators,
please keep an eye out for a good example sentence and send it along
to your supervisor!}

- \label{nestedexampleraw} \myul[red]{December 19th: The patient
underwent an MRI and EKG as well as emergency surgery.} During the
procedure, \myul[blue]{the patient experienced mild tachycardia},
and she also \myul[green]{bled significantly during the initial incision}.

Here, we can see that in addition to the overall container of December
19th (containing surgery, an EKG and an MRI), the surgery itself is
a container, containing some mild tachycardia and an initial incision.
The incision itself forms a third narrative container, containing
the significant bleeding.

To annotate a case like this, we will think about nesting in general.
Whether you are playing with Russian nesting dolls, packing boxes-within-boxes,
or packing a car for a long trip, smaller items go in smaller containers,
which go in bigger containers, which go in bigger containers, and
so forth. Here, we will use the same principle, but with narrative
containers instead of physical objects.

The largest temporal span (actual clock duration) here is ``December
19th'', so that should be the ultimate narrative container for all
these EVENTS. First, we will put everything into it (MRI, EKG, surgery)
that belongs there using three TLINKs. The surgery is also a narrative
container, but temporally, has a smaller temporal span than December
19th (likely a few hours rather than a full day). Inside it, we will
place mild tachycardia and initial incision using two more TLINKs.
Then, finally, the initial incision, with the smallest duration of
all, CONTAINS-SUBEVENT bled significantly. Example \Next shows all
the TLINKs required to fully annotate this sentence, representing
*EVENTs* in brackets and **TIMEX3s** in curly braces:

\begin{figure*
\centerline{ \mbox{\includegraphics[width=3in]{nested}} } \caption{Schematic view of Example \ref{nestedexample} as a Venn diagram


\label{nestingschematic} 
\end{figure*


- \label{nestedexample} **December 19th**: The patient underwent
an *MRI* and *EKG* as well as emergency *surgery*. During
the *procedure*, the patient experienced mild *tachycardia*,
and she also *bled* significantly during the initial *incision*.
\a. **December 19th** CONTAINS *MRI* \b{.} **December 19th\
CONTAINS *EKG* \c{.} **December 19th** CONTAINS *surgery*
\a. *surgery* CONTAINS *tachycardia* \b{.} *surgery*
CONTAINS-SUBEVENT *incision* \a. *incision* CONTAINS-SUBEVENT
*bled*

Because of the nesting, only the TLINKs mentioned above are necessary.
One does not need to, for instance, explicitly link ``bled significantly''
to December 18th, because it is clearly contained within it by virtue
of its container being contained within it. We can visualize these
nested containers with a Venn diagram, showing these containment relationships,
and thus, why we do not need to link the contents of each container
to every other container.

So, even in this complex case, we can completely capture the temporal
relations present by first putting all EVENTs into their proper containers
using TLINKs, and then linking the containers themselves, TLINKing
the temporally smallest container to the next smallest, and so forth,
until all containers are contained.

This kind of nesting is the only way that an EVENT will ever CONTAIN
a TIMEX3, and follows once again our rule of nesting smaller temporal
spans inside larger ones. See example \Next below, showing both an
example sentence and all the TLINKs needed to annotate it:

- \label{nestedtimexes}**December 28th**: The patient experienced
a *stroke* at **approximately 9:30am**, during her *surgery*.
\a. *stroke* OVERLAP **approximately 9:30am** \b{.} **December
28th** CONTAINS *surgery* \a. *surgery* CONTAINS *stroke*
\b{.} *surgery* CONTAINS **approximately 9:30am\

Here, we have an overarching container (**December 28th**) which CONTAINS
*surgery*. The surgery then CONTAINS both *stroke* and **approximately
9:30am**. Then, to complete the annotation, we'd mark that *stroke*
OVERLAPs **approximately 9:30am**.


#### Choosing the Anchors of Narrative Containers

When creating narrative containers as discussed above, you will need
to choose either a TIMEX3 or an EVENT to be the ``anchor'' of the
container, the temporal span which all of the other EVENTs fall within
(or begin/end on). Choosing which temporal span to be the anchor of
a given narrative container can be difficult, so here are a few ground
rules to help make these decisions easier and more consistent:
\begin{enumerate
- \textbf{The majority of TIMEX3 annotations will be narrative container
anchors}. 

\begin{itemize
- Usually, when a date (or other temporal expression) is given in a
document, it is to provide temporal context for one or more other
EVENTs. As such, they are ready candidates for the narrative container
anchor. 
\end{itemize
- \textbf{If you have a choice between using an EVENT or a TIMEX3 as
the narrative container anchor, you should pick the TIMEX3}. 

\begin{itemize
- This is not to say that you will never have an EVENT within an EVENT,
but often that will be because there is no TIMEX3 or because there
is narrative container nesting going on, as in Example \ref{nestedexample}. 
\end{itemize
- \textbf{If you use an EVENT as a narrative container anchor, try to
TLINK it to a few other container anchors to avoid it being stranded}. 

\begin{itemize
- See Section \ref{eventcon} for more detail here. 
\end{itemize
- \textbf{All other things being equal, an EVENT or TIMEX3 with a larger
temporal span is more likely to be a narrative container anchor}. 

\begin{itemize
- This is per Section \ref{russiandolls}, where this principle is shown
with detailed examples (\ref{nestedexample}, \ref{nestedtimexes}). 
\end{itemize
- \textbf{EVENTs will very seldom CONTAIN TIMEX3s.} 

\begin{itemize
- Only in minute-by-minute descriptions will an EVENT serve as a narrative
container in which a TIMEX3 will be included, and even still, there
will likely be an overarching TIMEX3 which CONTAINs the EVENT. See
example \ref{nestedtimexes} above as well as the discussion in \ref{russiandolls}. 
\end{itemize
- \textbf{Sub-events will be anchored to their main event, assuming
there is actually temporal containment, using CONTAINS-SUBEVENT} 

\begin{itemize
- If the note describes three different steps (e.g. incision, tumor
removal and closing) within a single surgery, those steps will be
CONTAINed by the surgery (using CONTAINS-SUBEVENT). This is the case
in all situations where we have an event/sub-event relation (as between
``incision'' and ``surgery'' in \ref{nestedexample}). 
\end{itemize
\end{enumerate

#### Ordering within narrative containers

Because of the difficulty of capturing detail within a given narrative
container, not all relations between EVENTs will be captured. For
instance, in example \ref{nestedexample}, we do not explicitly give
the relationships between EKG and Surgery, nor between the MI and
Tachycardia. In many cases, those relationships within a narrative
container will follow a set progression (first colonoscopy, then biopsy
(which occurs during the colonoscopy), then pathological analysis,
then histology), but you as an annotator are not asked (or allowed)
to make explicit those domain-specific progressions.

So, although it may seem like some of the narrative containers that
you define may be a loose bucket of temporal EVENTs, that's not actually
a problem, as the greater timeline of the document is more important
than the fine structure within a given narrative container, and as
you will find out, there are still plenty of TLINK annotations to
be made.

Of course, as described in \ref{tlinkrules}, \textbf{if a relation
is explicitly stated, it should always be marked}.


###Temporal Relation Annotation

Temporal Links (TLINKs), as previously mentioned, are relations you
can mark between EVENTs, between TIMEX3s, or across the two categories
to show the temporal relations present within the document and to
clearly define the bounds of the narrative containers at work beyond
what DocTimeRel will naturally give us. As mentioned previously, we
will display these links in this document using the following format:

- *EVENT1* RELATION *EVENT2*

Where RELATION is BEFORE, BEFORE/CAUSES, OVERLAP/CAUSES, BEFORE/PRECONDITIONS,
CONTAINS, CONTAINS-SUBEVENT, OVERLAP, SIMULTANEOUS, BEGINS-ON, or
ENDS-ON, as determined by the type of relation being stated. Before
we talk about exactly when to use each type of TLINK, we will first
discuss two types of annotation which we have folded into Temporal
Relations: Causation and Subevent annotation.

Also of note is that we have included a ``difficulty'' marker for
all TLINKs. This is defaulted to ``None'', but if an annotator creates
a TLINK whose type is uncertain to them, they can change this value
to ``Present'', indicating that the TLINK should not be taken as
certain. Now, let's discuss the different types of TLINK available
to annotators.


#### When to TLINK

\label{tlinkrules

TLINKs themselves are relatively straightforward, and in fact, the
more difficult part of annotating TLINKs is to know when to stop.
Without any constraint, one could see making TLINKs between every
EVENT in the document, which leads to exponential growth of TLINKs
and a tangle of relations which nobody, let alone a machine, would
like to unpack.

So, to constrain this process a bit, we have developed five rules
to govern TLINKing:


#### TLINK only when it captures more information than just marking DocTimeRel.

Because the `DocTimeRel' attribute of EVENTs expresses the relation
of the event to the time the document or section was written, you
will never need to TLINK to the DOCTIME annotations. Marking an EVENT
as `after' in the DocTimeRel field gives us the same information as
making a BEFORE TLINK between the EVENT and DOCTIME, so you need not
explicitly mark that. Similarly, if one EVENT has a DocTimeRel of
OVERLAP and another has a DocTimeRel of AFTER, there is no need to
make a TLINK between those two EVENTs.


#### TLINK all EVENTs to their narrative container, if possible.

As previously discussed, most EVENTs will fall into a narrative container
of some kind. If a given EVENT is in a narrative container (like ``August
22nd'' or ``during her recovery''), you should always TLINK that
EVENT to the TIMEX3 or EVENT which represents that narrative container,
using the appropriate link. Once again, though, this should only be
done if the result will be more informative than just analyzing the
DocTimeRels. See \Next, showing an example sentence and the TLINKs
required to annotate it:

- **December 19th**: The patient underwent an *EKG* as well
as emergency *surgery*. During the *surgery*, the patient
experienced another *MI*, and repeated *tachycardia*. \a.
**December 19th** CONTAINS *EKG* \b{.} **December 19th** CONTAINS
*surgery* \b{.} *surgery* CONTAINS *MI* \b{.} *surgery*
CONTAINS *tachycardia*

When annotating, not every EVENT will be a part of a detailed narrative
container (more specific than before, after, or during DOCTIME). However,
it is vital that you, as an annotator, stop to ask yourself whether
each EVENT you examine is a part of a narrative container, and whether
the TLINKs you created are sufficient to mark that membership.

If one EVENT is TLINKed to a second EVENT which is mentioned many
times (all of which should be linked in an IDENTICAL chain), you do
not need to actually link it to all of the other EVENTs in the chain,
though such links might be technically correct. To prevent this spider-webbing,
only create a TLink to the most recently mentioned EVENT instance
in the chain. As an example:

- Patient underwent *surgery* last week for colon polyps.
The *hemicolectomy* *removed* the lesions. \a.*hemicolectomy*
CONTAINS-SUBEVENT *removed* \b{.} !*surgery* CONTAINS-SUBEVENT
*removed* (do not create this TLink!)

Note that *surgery* and *hemicolectomy* would be in an IDENTICAL
relation with each other. See \ref{corefguidelines} for more details.


#### TLINK all explicitly stated temporal relations.

If the writer goes out of his or her way to make a temporal statement,
a TLINK should be made to reflect that statement. So, if the sentence
reads:

- The patient *developed* a *rash* after *treatment*.
\a. *treatment* BEFORE *rash* \b{.} *treatment* BEFORE
*developed*

You should explicitly mark the treatment as being BEFORE both *developed*
and *rash*, using a TLINK, regardless of the fact that *developed*
and *rash* will also be ALINKed. Note, though, that if no explicit
temporal language is used, no TLINK should be created, and annotator
knowledge should not be used to fill these TLINKs in.


#### Try to only link EVENTs and TIMEX3s within the same sentence.

In a perfect world, nearly all TLINKs would occur across two EVENTs
or TIMEX3s in the same sentence. That said, often you need to link
to an EVENT or TIMEX3 in a previous sentence to put an EVENT in the
proper narrative container. In these situations, you may do so, but
you should double-check to ensure that there is no other way of going
about it, and remember that Coreference annotation will be done to
link pronouns and subsequent mentions, so linking an EVENT to a subsequent
reference to the narrative container is acceptable as well.

That said, because of the nature of the notes, \textbf{TLINKs should
never link items in sections with differing SECTIONTIME.


#### ACTUAL or UNCertain EVENTs should never be linked to HYPOTHETICAL
or GENERIC EVENTs, and vice versa.

This may seem quite specific, but HYPOTHETICAL and GENERIC EVENTs
aren't really on the same timeline as other EVENTs dealing with the
patient's actual care. Because of this, it can be quite tricky to
link them to the overall timeline, and we need to take care to avoid
having non-real EVENTs showing up on patient timelines. To avoid the
complications and potential broken relations when non-real EVENTs
are pruned from timelines, ACTUAL or UNCertain EVENTs should never
be linked to HYPOTHETICAL or GENERIC EVENTs, and vice versa. In this
way, ``real'' EVENTs are never linked to non-real ones.

- Adjuvant *chemotherapy* following her upcoming *surgery*
would generally be recommended, but given her poor *health*, this
is not an option.

Here, because the *chemotherapy* is HYPOTHETICAL, it cannot be
TLINKed to *surgery*, even given the explicit mention. Further
discussion can be found in Section \ref{discussion}.


#### You do not need to TLINK TIMEX3s to one another.

Although there is certainly a temporal relation between, say, ``January
15th, 2009'' and ``March 2013'', part of the post-processing of
these annotations is the normalization of these Temporal Expressions,
which will allow us to order these expressions on a timeline based
on the times they represent. Although you will certainly still TLINK
EVENTs and TIMEX3s, the TIMEX3s in the document can almost always
be temporally ordered without the annotator's help.

\color{blue} 


#### Avoid ``Millisecond Reasoning''

As you're annotating, there are some relations which feel ``99.9\%
true'', and you're held back only by worries that, at a very zoomed-in
level, the relation is somehow different. For example:

- She *listened* to music during her whole *drive* home.
\a. *listened* SIMULTANEOUS *drive*

Some annotators may stop themselves and ask questions like ``Well,
maybe there was a moment at the beginning where she was driving, but
the radio hadn't yet loaded the CD'', or ``Maybe she finished the
song sitting in her driveway''. These questions, although demonstrating
admirable attention to detail, are ultimately unproductive, as they
represent missing the forest for a very small tree. In this case,
the assertion of simultaneity is made, and to back down to OVERLAP
represents a major semantic loss. So, using this sort of ``millisecond
reasoning'' will serve only to rob us of information, and will result
in legally flawless annotations which miss the entire point of the
text.

Similarly, CONTAINS is vulnerable to Millisecond Reasoning:

- She had an *MRI*, *radiation*, and a course of *chemotherapy*
during her *treatment*. \a. *treatment* CONTAINS-SUBEVENT
*MRI* \b{.} *treatment* CONTAINS-SUBEVENT *radiation*
\b{.} *treatment* CONTAINS-SUBEVENT *chemotherapy*

In this situation, some annotators may be reluctant to use CONTAINS,
as presumably, the temporal bounds of ``treatment'' are the beginning
of the first sub-event, and the end of the last. Thus, at a micro-second
level, there is not containment, as there is, perhaps, no portion
of the ``treatment'' that begins prior to the first subevent in
order to contain it.

Again, though, this sort of reasoning wins us nothing. Here, a CONTAINS-SUBEVENT
relation is \textit{strongly} indicated, and no other relation is
a better fit. It is a poor choice to talk ourselves out of a 99.9\%
correct annotation (which could be, depending on one's interpretation
of treatment, 100\% correct) in favor of OVERLAP, which is much less
meaningful.

Mind you, seconds can still count, and we must always be accurate
relative to the text:

- The *headache* began moments after the *treatment* *began*,
and ended shortly after it *stopped*.

In this case, the text is quite clearly stating that *headache*
is NOT SIMULTANEOUS with *treatment*. Instead, one could use BEGINS-ON
and ENDS-ON links to *began* and *stopped* to express more
accurately what's going on.

So, although accuracy is critical, and the text should always be trusted,
if you find yourself in a situation where you feel like you're ``talking
yourself out of'' a relation on the basis of a trivial temporal difference
which is not explicitly stated, please make the relation and move
on with your life.

\color{black


#### TLINK sub-types

\label{tlinktypes

There are ten different temporal relations often used in this schema,
BEFORE, BEFORE/CAUSES, OVERLAP/CAUSES, BEFORE/PRECONDITIONS, OVERLAP,
SIMULTANEOUS, BEGINS-ON, ENDS-ON, CONTAINS, and CONTAINS-SUBEVENT.
There is no default relation type for TLINKs.


#### BEFORE

BEFORE is fairly straightforward and simply orders two events in time.

- The 8th Infantry will *arrive* before *sundown*. \a.
*arrive* BEFORE *sundown*

- She *vomited* shortly before *surgery*. \a. *vomited*
BEFORE *surgery*

- His anterior chest *rash* has not *reoccurred* since
the *PCN* VK was *discontinued* **24-hours ago**. \a. *discontinued*
BEFORE *reoccurred*$_{NEG}$ \b{.} *rash* BEFORE *reoccurred*$_{NEG}$
\c{.} (*rash* ENDS-ON *discontinued*) -- Discussed below.
\c{.} **24-hours ago** OVERLAP *discontinued*

It is worth noting that in \Last, *PCN* will be linked to *discontinued*
using an ALINK of the type TERMINATES, described in Section \ref{alinks}.

When annotating, remember that ``X occurred after Y'' can be expressed
by saying ``Y occurred before X\textquotedbl{}: - The *shooting*
came shortly after the drug dealer's *release*. \a. *release*
BEFORE *shooting*

- She was *seen* by Dr. Jones in cardiology following the
stent *placement*. \a. *placement* BEFORE *seen*

- He had a car *accident* shortly after his *visit*. \a.
*visit* BEFORE *accident*

- He had a *neckache* after *surgery*. \a. *neckache*
BEFORE *surgery*


#### CONTAINS

\label{revelation

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

- In **2007**, 15 people were *killed* outside Mumbai. \a.
**2007** CONTAINS *killed*

- During the US-led *invasion*, reporters *rode* along
with actual military units. \a. *invasion* CONTAINS *rode*

- **March 2005** - Patient underwent *appendectomy* \a. **March
2005** CONTAINS *appendectomy*

- *Levaquin* 750 mg p.o. q. day (will *restart* **today**)
\a. **today** CONTAINS *restart*

- *Comparison* is made with prior MRI head *examination*
without and with gadolinium from **10-23-03**. \a. **10-23-03** CONTAINS
*examination*

- An ENT performed the * my* during **Friday**'s *surgery*.
\a. **Friday** CONTAINS *surgery*

- *Gengraf* 300-mg p.o. b.i.d. (*decreased* in **early
June**) \a. **early June** CONTAINS *decreased*

In addition, we have made one specific regulation involving the use
of CONTAINS: All test results or observations are to be linked to
the test which generated them (their narrative container) using a
CONTAINS relation,\textit{ assuming there is actually temporal containment}.
This is not always intuitive, because as humans with some inferencing
ability, we realize that the tumor likely existed before the CT scan
which revealed it, but from a machine-learning perspective, it is
important to have that consistency. So, in a section like:

- *Colonoscopy* (**January 7, 2010**): Fair/adequate *prep.*,
Limited *Colonoscopy* to the distal sigmoid due to an obstructive
*lesion*. Diminutive *polyps* of the rectosigmoid. \a. **January
7, 2010** CONTAINS *Colonoscopy* \b{.} *Colonoscopy* CONTAINS
*lesion* \b{.} *Colonoscopy* CONTAINS *polyps*

\vspace{0.25cm
 \fbox{ %
\begin{tabular}{p{0.6in}p{14cm}
\includegraphics[width=0.5in]{warning} \\
\textbf{Caution!}  & \raisebox{4mm}{%
\parbox[c]{14cm}{%
\vspace{2mm
\textit{There are many relations which seem like a sort of semantic
containment (things like part/whole, cause/effect, disorder/symptoms).
However, the CONTAINS relation should }\textbf{\textit{only}}\textit{
be used when there exists strict temporal containment (the temporal
span of the container fully encompasses that of the contained), and
a more specific relation (CONTAINS/SUB-EVENT, for instance) is not
indicated. This rule will not be violated, and pay attention to DocTimeRel
(because a BEFORE EVENT will never CONTAIN an OVERLAP EVENT, etc).
Use a WHOLE/PART relation for instances of physical containment, etc.
Discussed below.}%
}}\ \
\tabularnewline
\end{tabular}} \vspace{0.25cm



#### CONTAINS-SUBEVENT

\label{subevent

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

- There were 5 different *skirmishes* during the marathon
*battle*. \a. *battle* CONTAINS-SUBEVENT *skirmishes*

- During **Friday's** *surgery*, the patient's heartrate *spiked*
during the initial *incision*. \a. *surgery* CONTAINS-SUBEVENT
*incision* \b{.} *surgery* CONTAINS *spiked* \c{.} **Friday\
CONTAINS *surgery*

- The *tornado* was accompanied by high *winds* and multiple
funnel *clouds*. \a. *tornado* CONTAINS-SUBEVENT *winds*
\b{.} *tornado* CONTAINS-SUBEVENT *clouds*

- *Colonoscopy* (**January 7, 2010**): Fair/adequate *prep.*,
Limited *Colonoscopy* to the distal sigmoid due to an obstructive
*lesion*. Diminutive *polyps* of the rectosigmoid. \a. *Colonoscopy*
CONTAINS-SUBEVENT *prep.*

If there is no such link of necessity, or if this event is a part
of this particular instance, but is not expected in the majority of
instances, the relationship is simply containment:

- There was a *thunderstorm* during the marathon *battle*.
\a. *battle* CONTAINS *thunderstorm*

- During **Friday's** *surgery*, the patient's heartrate *spiked*
when she *fell* off the table. \a. *surgery* CONTAINS *fell*
\b{.} *surgery* CONTAINS *spiked* \c{.} **Friday** CONTAINS
*surgery* \d{.} (*spiked* BEGINS-ON *fell*) -- Discussed
below in Section \ref{corefannotation}.

- The *earthquake* occurred during the *parade*. \a.
*parade* CONTAINS *earthquake*

- There was a large *interruption* when the colonel and his
guards *burst* into the parliament *debates*. \a. *debates*
CONTAINS *interruption* \b{.} *debates* CONTAINS *burst*
\c{.} (*interruption* BEGINS-ON *burst*) -- Discussed below.

\vspace{0.25cm
 \fbox{ %
\begin{tabular}{p{0.6in}p{14cm}
\includegraphics[width=0.5in]{warning} \\
\textbf{Caution!}  & \raisebox{4mm}{%
\parbox[c]{14cm}{%
\vspace{2mm
\textit{Remember, CONTAINS-SUBEVENT is still a CONTAINS temporal relation.
If you have two items that are event/sub-event, but where the EVENT
does not temporally CONTAIN the sub-event, use the generic BRIDGING
relation.}%
}}\ \
\tabularnewline
\end{tabular}} \vspace{0.25cm



#### OVERLAP

OVERLAP is a single temporal relation that encompasses all the different
notions of two things happening at the same time, but is less specific
than CONTAINS or SIMULTANEOUS. This can refer to two nearly simultaneous
events, an EVENT that occurs during another larger EVENT or time reference
(but where containment is not entirely sure), or any other sense in
which two events are occurring in the same time frame:

- While the mayor *spoke* to reporters about his latest anti-cartel
*initiatives*, his home was being *raided* by state officials.
\a. *spoke* OVERLAP *raided*

- The hurricane *struck* while G8 members *discussed*
climate change just a few hundred miles away. \a. *struck* OVERLAP
*discussed*

- The patient's first *MI* occurred while she was undergoing
*chemotherapy*. \a. *chemotherapy* OVERLAP *MI*

- The patient had some rectal *itching* and mild *pain*
**today**, mostly **this morning**. \a. **today** CONTAINS *itching*
\b{.} **today** CONTAINS *pain* \b{.} **this morning** OVERLAP
*itching* \b{.} **this morning** OVERLAP *pain*

- He does have a history of peri-rectal *abscess* with his
last round of *chemotherapy*. \a. *chemotherapy* OVERLAP
*abscess*

- She is not *interested* in pursuing chemotherapy at **this
time**. \a. **this time** OVERLAP *interested*$_{NEG}$

In short, OVERLAP is meant for situations where two events overlap
in some way, but where you are not sure (or do not have enough information
to tell) whether there is containment of the events' boundaries.

OVERLAP is also used for linking TIMEX3s of type SET with other EVENTs,
as in \Next:

- We will keep her on rate-control *medications* 100 mg **twice
daily** \a. **twice daily** OVERLAP *medications*

\vspace{0.25cm
 \fbox{ %
\begin{tabular}{p{0.6in}p{14cm}
\includegraphics[width=0.5in]{warning} \\
\textbf{Caution!}  & \raisebox{4mm}{%
\parbox[c]{14cm}{%
\vspace{2mm
\textit{OVERLAP provides relatively little information for the actual
processing of text compared to our other temporal relations. If you
are reasonably sure that the relation is one of containment, you should
use one of the CONTAINS relations instead, and often, one can represent
a potential OVERLAP more specifically using narrative containers and
a bit of additional thought.}%
}}\ \
\tabularnewline
\end{tabular}} \vspace{0.25cm
 \color{blue} 


#### BEFORE/CAUSES, OVERLAP/CAUSES, BEFORE/PRECONDITIONS and OVERLAP/PRECONDITIONS

Although these are included in the list of TLINKs during annotation,
and carry the same temporal information and properties as BEFORE and
OVERLAP, they carry additional causal meanings, and are fully explained
in Section \ref{causation}. \color{black} 


#### BEGINS-ON

BEGINS-ON signals that the EVENT begins on the EVENT or TIMEX3 it
is related to. This type of TLINK will only occur with EVENTs which
have a non-trivial temporal span. Relations with punctual EVENTs will
usually be marked with BEFORE instead.

Note that BEGINS-ON is to be used only where there is no causal relationship.

- **2008** marked the *start* of the rebels' brutal *campaign*
\a. *start* BEGINS-ON **2008\

- She has had Abdominal *Cramping* since **January**. \a.
*Cramping* BEGINS-ON **January\

- He reports intermittent chest *pain* since his prior *MI*.
\a. *MI* BEFORE *pain*


#### ENDS-ON

ENDS-ON signals that the EVENT ends on the EVENT or TIMEX3 it is related
to. As with BEGINS-ON, this type of TLINK will only occur with EVENTs
which have a non-trivial temporal span. Relations with punctual EVENTs
will usually be marked with BEFORE instead.

- The ``occupy'' *protests* largely *ended* when the
weather grew too *cold* for *camping*. \a. *protests*
ENDS-ON *cold*

- She has had no *bleeding* since her *stitches* were
*removed*. \a. *bleeding*$_{NEG}$ ENDS-ON *removed*

Note that ENDS-ON can be used in concert with BEGINS-ON to mark a
duration.

- She was on *chemo* from **March** through **July**. \a.
*chemo* BEGINS-ON **March** \b{.} *chemo* ENDS-ON **July\


#### SIMULTANEOUS

SIMULTANEOUS means exactly that: Two EVENTs have the same temporal
boundaries and extent.

SIMULTANEOUS is, technically speaking, a more specific type of OVERLAP
relation, and SIMULTANEOUS is to be used only when there is strict
simultaneity, that is, both the start- and endpoints of two temporal
entities are \textit{exactly} the same.

In the real world, such simultaneity does not often arise from coincidence
(and when it happens to be the case, it is widely commented on and
celebrated). Generally, true simultaneity only happens by coordination
(\textquotedbl{}So long as the president is *aboard*, the carrier
will be on high *alert*\textquotedbl{}) or by necessity (\textquotedbl{}I'll
*drink* as long as my cup is *full*\textquotedbl{}).

- She *listened* to music during her whole *drive* home.
\a. *listened* SIMULTANEOUS *drive*

In this case, she started a music-listening EVENT when she began her
ride, and ended when the ride ended. There is a functional relationship.

- Cell phones must be *turned* off while in *flight*.
\a. *turned* SIMULTANEOUS *flight*

The start and end of *flight* represent the start and end of the
prohibition, so, necessarily, SIMULTANEOUS.%
\footnote{Of course, the event is ``turned off'', but the head of this multi-word
expression is ``turned''.%


- For the duration of her *surgery*, the anesthesiologist
*monitored* her pulse at the wrist. \a. *surgery* SIMULTANEOUS
*monitored*

The anesthesiologist's monitoring would necessarily start and end
with the surgery.

In many cases of true simultaneity, there is a relationship which
borders on causality. However, these are usually not true causality
(representing strong correlation, rather than necessary causation),
and \textit{when two EVENTs are unquestionably SIMULTANEOUS and questionably
causal, we will mark the more specific SIMULTANEOUS relation, rather
than using OVERLAP-CAUSE}.

- While they *recorded*, the red light stayed *on*. \a.
*recorded* SIMULTANEOUS *on*

- The whole time that John *raced* around the track, his *frightened*
mother *clutched* her seat with white knuckles. \a. *raced*
SIMULTANEOUS *clutched* \b{.} *raced* BEFORE-CAUSE *frightened*

In this case, the clutching is likely to start and end with the racing,
but alas, the fear persists.

There are many instances of false or one-sided simultaneity to avoid:

- He was *sad* when she *visited*. \a. We're not sure
that the sadness began or ended when she arrived or left. OVERLAP.

- The bombers *shouted* while they *ran*. \a. It's unlikely
that they began shouting when they began running, persisted throughout,
and stopped when they stopped running. OVERLAP.

- The Colorado fires *burned* throughout the *summer*.
\a. Colorado did not catch fire on June 21st, and promptly extinguish
itself on September 23rd. *summer* CONTAINS *burned*

- She *talked* with her Mom while I *made* dinner. \a.
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
due to excited ``SIMULTANEOUS EVENT/EVENT TLINK!!!'' facebook posts%
}.

Unless you are sure that the start of the first EVENT \textit{is
the start of the second, and similar for the end, use CONTAINS or
OVERLAP.

\color{black

\vspace{0.25cm
 \fbox{ %
\begin{tabular}{p{0.6in}p{14cm}
\includegraphics[width=0.5in]{warning} \\
\textbf{Caution!}  & \raisebox{4mm}{%
\parbox[c]{14cm}{%
\vspace{2mm
\textit{You do not need to create SIMULTANEOUS TLINKs for EVENTs which
are in an IDENTICAL chain. Two identical EVENTs share both temporal
bounds, and thus, are SIMULTANEOUS, but we will generate those links
later. Only mark SIMULTANEOUS for non-coreferent EVENTs.}%
}}\ \
\tabularnewline
\end{tabular}} \vspace{0.25cm



#### Expressing TLINK Types in Point Algebra

A more precise (although perhaps more esoteric) way to express temporal
relations is using point algebra. In the style of Allen 1983 b\cite{Allen:1983:MKT:182.358434},
we can take the start and end of event A to be A- and A+, respectively,
and compare those points to the start and end of EVENT B, B- and B+,
using < (``less than'') and > (``greater than'') to indicate position
on the timeline.

Given this notation, our TLINK types can be expressed as below:

\begin{tabular}{|c|c|c|
\hline 
\textbf{Relation}  & \textbf{Notation}  & \textbf{Meaning}\tabularnewline
\hline 
BEFORE  & A+ < B-  & ``A is before B\textquotedbl{}\tabularnewline
CONTAINS  & (A- < B-) AND (A+ > B+)  & ``A contains B\textquotedbl{}\tabularnewline
CONTAINS-SUBEVENT  & (A- < B-) AND (A+ > B+)  & ``A contains B\textquotedbl{}\tabularnewline
OVERLAP  & (A- < B- < A+) OR (B- < A- < B+)  & ``A and B overlap'' \tabularnewline
BEGINS-ON  & A+ = B-  & ``B begins-on A\textquotedbl{}\tabularnewline
ENDS-ON  & A- = B+  & ``B ends-on A\textquotedbl{}\tabularnewline
SIMULTANEOUS  & A- = B- AND A+ = B+  & ``A is simultaneous with B\textquotedbl{}\tabularnewline
\hline 
\end{tabular

Note that our definitions of OVERLAP and SIMULTANEOUS are symmetrical,
in that ``A OVERLAP B'' and ``B OVERLAP A'' mean the same thing.
For OVERLAP, which EVENT starts first is not recoverable from the
annotation without prior knowledge of both A- and B-.


#### Annotating polarity of TLINKs

\label{TLINKPolarity} Polarity of TLINKs is identical to polarity
in EVENTs, although naturally the applications will differ slightly.
Polarity is used and applicable with TLINKs of all types.


#### POS - Positive

As with EVENTs, the default and most common polarity value used is
POS. This is the marker of positive polarity. This is used for a temporal
specification that is not negated. Most TLINKs are of this polarity,
and this is the default value. POS need not be specified in annotation.

All examples in this guideline, unless otherwise marked, represent
POS TLINKs.


#### NEG - Negative

TLINKs are marked as NEG only when they are both explicitly asserted
\textit{and} asserted to be false.

- The *bombing* did not take place on **the 18th** as expected,
but on **the 24th**. \a. **18th** CONTAINS -- NEG *bombing* \b{.
**24th** CONTAINS -- POS *bombing*

- The *earthquake* did not cause the *fire*, instead,
*it* was caused by an electrical *short* . \a. *earthquake*
BEFORE/CAUSES -- NEG *fire* \b{.} *short* BEFORE/CAUSES --
POS *it* \b{.} *earthquake* BEFORE -- POS *fire*

- The *meeting* was not on **Thursday**. \a. **Thursday\
CONTAINS -- NEG *meeting*

It is important to contrast these with the below:

- The *meeting* on **Thursday** didn't occur. \a. **Thursday\
CONTAINS -- POS *meeting*$_{\text{ACTUAL, NEG}}$

In the negated TLINKs, the EVENTs themselves are not negated, but
instead, the temporal relation \textit{itself} is negated. It is quite
possible (and in fact, far more common) to have negated EVENTs occuring
as a part of a POS TLINK. These most often occur as links between
two POS EVENTs, which are specified as NOT having a certain temporal
relation.

\vspace{0.5cm
 \fbox{ %
\begin{tabular}{p{0.6in}p{14cm}
\includegraphics[width=0.5in]{warning} \\
\textbf{Caution!}  & \raisebox{4mm}{%
\parbox[c]{14cm}{%
\vspace{2mm
\textit{TLINK negation is used only when the temporal relation itself
is negated. It is completely independent from EVENT negation, and
the negation of EVENTs in no way implies negation of the TLINK. NEG
TLINKs are far less common than NEG EVENTs, and should be pondered
carefully before creation.}%
}}\ \
\tabularnewline
\end{tabular}} \vspace{0.5cm



#### Annotating contextual modality of TLINKs

\label{linkmodality} \label{TLINKModality} TLINKs can take the same
contextual modalities as EVENTs: ACT, UNC, HYP, and GEN. These modalities,
as with EVENTs, represent claims about the reality or certainty of
the TLINKs, and are independent of the modalities or certainties of
the EVENTs they claim.

TLINKs are marked as UNC, HYP, or GEN only when the temporal relation
itself is uncertain, hypothetical or generic.


#### ACT - Actual

The first modality for TLINKs is ACTUAL, which is used most of the
time, and is the default option (that need not be specifically marked).
An overwhelming majority of TLINKs are ACTUAL, and are asserted as
true without any hedging or hypotheticality.

All examples in this guideline, unless otherwise marked, represent
ACTUAL TLINKs.


#### UNC - Uncertain/Hedged

TLINKs, like EVENTs, are marked as UNCertain when we can point to
some explicit lexical or phrasal trigger that indicates some degree
of uncertainty about the reality of the temporal relation. These TLINKs
are presented with a sort of tacit claim that they're \textit{probably
real (unlike hypotheticals, which are explicitly irrealis), but where
the author is unsure.

This also includes TLINKs that are mentioned with any sort of hedging.
This hedging can be lexical (``seems'', ``likely'', ``suspicious'',
``possible'', ``consistent with'', ``claims''), or phrasal (``I
suspect that...'', ``It would seem likely that''). These TLINKs
are strongly implied, but, for safety, liability, or due to lack of
comprehensive evidence, are not stated as fact. As with EVENTs, it
is very important that these uncertain temporal relations be included
as part of the timeline, but be marked so that they can be easily
differentiated from known facts.

- He likely *escaped* on the **18th** during a **guard change**,
although authorities cannot be sure. \a. **18th** CONTAINS *guard
change* <ACTUAL> \b{.} *guard change* CONTAINS *escaped*
<UNCERTAIN>

- The chairman will, in all likelihood, *step* down on **Monday**.
\a. **Monday** CONTAINS *step* <UNCERTAIN>

- We have every reason to expect that her incision will *heal*
before her *tournament*. \a. *heal* BEFORE *tournament*
<UNCERTAIN>

- The *fire*, very likely caused by a lightning *strike*,
is *growing* due to high *winds*. \a. *strike* BEFORE/CAUSE
*fire* <UNCERTAIN> \b{.} *winds* OVERLAP/CAUSE *growing*
<ACTUAL> \b{.} *strike* BEFORE *growing* <ACTUAL>


#### HYP - Hypothetical

The third modality for TLINKs is HYP. This is useful when annotating
theories, future possibilities, or other hypothetical temporal relations.
Again, this is unrelated to the modality of the EVENTs, and is only
when the temporal relation itself is hypothetical, theoretical, or
otherwise dependent on an external factor.

- Her *surgery* may take place on the **18th**. \a. **18th\
CONTAINS *surgery* <HYPOTHETICAL>

- If the *explosion* was caused by a natural gas *leak*,
the insurance will not *cover* the *reconstruction*. \a.
*leak* BEFORE/CAUSE *explosion* <HYPOTHETICAL> \b{.} *explosion*
BEFORE/PRECONDITIONS *reconstruction* <ACTUAL>

- Obama's *visit*, if *it* occurs on a **weekday**, is
expected to cause traffic *headaches*. \a. *it* OVERLAPS/CAUSE
*headaches* <HYPOTHETICAL> \b{.} **weekday** CONTAINS *it*
<HYPOTHETICAL>

Great caution must be exercised before marking a relation itself as
HYPOTHETICAL, as hypothetical EVENTs are not necessarily members of
hypothetical relations. See the below example:

- If the group *attacks* during the *Olympics*, Russia
has promised swift *retaliations*. \a. *Olympics*$_{\text{ACT}}$
CONTAINS *attacks*$_{\text{HYP}}$ <HYPOTHETICAL> \a. *attacks*$_{\text{HYP}}$
BEFORE/CAUSE *retaliation*$_{\text{HYP}}$ <ACTUAL>

In this example, we have a hypothetical attack, an actual Olympic
games, and a hypothetical retaliation. The timing of the attack is
hypothetical, but the causation of retaliation is certain.

As with EVENTs, polarity and modality of TLINKs do not interact.


#### GEN - Generic

GENERIC is our fourth contextual modality, and is used for TLINKs
which may be mentioned in a document, but are only mentioned in a
general sense, and do not appear on the timeline of the overall document.
These usually occur to provide background or information, or as generalized
information when no specific information is yet available.

Generic temporal information (which is true in any document) is marked
with GENERIC:

- *Attacks* in the region generally don't occur on **Holy
days** \a. **Holy days** CONTAINS *attacks*$_{\text{NEG}}$ <GENERIC>

- US Presidential *Elections* are held on the **Tuesday after
the first Monday in November** \a. **Tuesday after the first Monday
in November** CONTAINS *Elections* <GENERIC>

... but remember that specific mentions do not get <GENERIC>:

- The last US Presidential *Election* was held on **November
4th, 2008** \a. **November 4th, 2008** CONTAINS *Election* <ACTUAL>

\vspace{0.5cm
 \fbox{ %
\begin{tabular}{p{0.6in}p{14cm}
\includegraphics[width=0.5in]{warning} \\
\textbf{Caution!}  & \raisebox{4mm}{%
\parbox[c]{14cm}{%
\vspace{2mm
\textit{As with TLINK polarity, TLINK modality is seldom anything
but the default, ACTUAL. If you are considering marking a TLINK with
UNC, HYP or GEN, double-check to make sure that it is the temporal
relation itself which is uncertain, hypothetical, or generic, rather
than just the EVENTs within it.}%
}} \
\tabularnewline
\end{tabular}} \vspace{0.5cm


%%%% ANNOTATING CAUSALITY %%%%


\color{black


###Causation and Precondition Annotation

\label{causation

\color{blue} \textbf{THIS ENTIRE SECTION IS NEW, PLEASE READ AND
COMMENT} \color{black

In our schema, we want to be able to understand not just the relative
orderings of different EVENTs, but to also annotate when one event
\textit{causes} or \textit{preconditions} another event.

At first glance, it may seem like an odd choice to mark causation
and preconditioning as a subtype of temporal link rather than as a
link of its own. However, causation and preconditioning are inherently
temporal: a precondition necessarily must occur BEFORE the EVENT which
it has preconditioned. In case of causation, the cause will \textit{start
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


#### Distinguishing ``Cause'' from ``Precondition''

In our view of causality, we claim that ``X CAUSES Y'' if (and only
if), according to the writer, the particular EVENT Y was \textit{inevitable
given the particular EVENT X. Put differently, the existence of X
was not just helpful in allowing Y to happen, nor associated with
Y, but the occurrence of X triggered or immediately necessitated the
occurrence of Y:

- The *rockfall* made the *over-full* *dam* *burst*,
*flooding* the *town* below. \a. *rockfall* BEFORE/CAUSES
*burst* \b{.} *burst* BEFORE/CAUSES *flooding*

Here, the rockfall is what immediately caused the burst (although
the over-full nature of the dam may have preconditioned it), just
as the burst caused the flooding. Put differently, had the rocks not
fallen, and had the dam not burst, according to the author, there
would have been neither bursting nor flooding.

- The *sheriff* *fired* *her* *gun*, *killing*
the *injured* *deer*. \a. *fired* BEFORE/CAUSES *killing*
\b{.} *sheriff* IDENTICAL *her*

Here, although the injury may have eventually led to the deer's demise,
the killing was caused directly and immediately by the firing of the
gun.

- *Christchurch*, the first *city* *established* in
*New Zealand*, had endured a *series* of *earthquakes*
that *destroyed* *its* *infrastructure*, *homes* and
*communities*. \label{nzquake} \a. *earthquakes* OVERLAP/CAUSES
*destroyed* \c{.} Coreference relations: \a. *Christchurch*
APPOSITIVE *city* \b{.} *Christchurch* IDENTICAL *its*
\c{.} WHOLE *New Zealand*: PART *Christchurch* \d{.} WHOLE
*its*: PARTs *infrastructure*, *homes*, *communities*
\e. SET *series*: MEMBER *earthquakes*

In \Last, it is the case that the destruction would not have happened
without the earthquake, and that once the earthquake began (and through
its duration, hence OVERLAP/CAUSES), the destruction was inevitable.

- Although *it* took **many years**, the *discovery* of
*Uranium* outside *Moab* would eventually *revitalize*
the local *economy*. \label{moaburanium} \a. *discovery*
BEFORE/CAUSE *revitalize* \b{.} *it* IDENTICAL *revitalize*

\Last shows an example where, although there was significant time
lag between the cause (the discovery of Uranium and the effect: revitalization),
we are led to believe that in this case, the discovery did directly
and inevitably trigger revitalization, and therefore, the link is
causal.

So, again, causality is marked in our schema only if EVENT Y was inevitable
given this particular instance of EVENT X.

Preconditioning, in our view of the world, carries no such inevitability.
In RED, we annotate ``X PRECONDITIONS Y'' if, according to the writer,
had the particular EVENT X not happened, the particular EVENT Y would
not have been able to happen. Put differently, although a preconditioning
EVENT is not \textit{sufficient} to cause another EVENT, its occurrence
is \textit{necessary} in order for the other EVENT to have happened.

- The *rockfall* made the *over-full* *dam* *burst*,
*flooding* the *town* below. \a. *rockfall* BEFORE/CAUSES
*burst* \b{.} *burst* BEFORE/CAUSES *flooding* \b{.
\textbf{*over-full* BEFORE/PRECONDITIONS *burst*

Here, we are led to believe that the over-full nature of the dam helped
promote bursting, and thus, was a precondition of the burst itself.
However, the over-fullness of the dam alone, in this particular case,
was not enough to cause the burst, thus, is only a precondition.

- The *sheriff* *loaded* *her* *rifle*, then *fired*
at the *target*. \a. *loaded* BEFORE/PRECONDITION *fired*
\b{.} *sheriff* IDENTICAL *her*

Were the rifle not loaded, it could not have fired, and therefore,
loading is a precondition to firing (although the firing is separately
caused).

- The *strikes* came in *retaliation* for recent terrorist
*attacks*. \a. *attacks* BEFORE/PRECONDITIONS *retaliation*
\b{.} *strikes* IDENTICAL *retaliation*

In \Last, although something else (a pilot pushing a button, or a
general's orders) was the direct cause of the strikes, we are told
(via the meaning of ``retaliation'') that the strikes would not
have happened were it not for the attacks.

Similarly, note that occaisionally an ongoing state can be a motivation
or other precondition for an action; in those cases, you can use OVERLAP/PRECONDITION:

- I feel that they are *punishing* him for his *condition*
by keeping him after school, \a. *condition* OVERLAP/PRECONDITIONS
*punishing*

Remember as well that SUBEVENT, CAUSES, and PRECONDITIONS relations
are mutually exclusive, and one event pair can only have one of these
relations. Therefore, if an event pair has more than one of these
three relations, there is an order of \textquotedbl{}importance\textquotedbl{}.
If the relation is clearly some sort of outcome or causation (cause
or precondition) of an event, then default to the CAUSES or PRECONDITIONS
reading, as they are easier to consistently capture. If torn between
CAUSES and PRECONDITIONS, check the \textquotedbl{}special cases\textquotedbl{
section to see if there are special hints for your phenomenon, and
otherwise default to CAUSES.

To sum up, CAUSES implies that the occurrence of one EVENT is \textit{sufficient
to trigger another, whereas PRECONDITIONS only states one EVENT was
\textit{necessary} for another to later take place.

Once this distinction is fully understood, proper annotation is simply
a matter of understanding the temporal nature of each, and creating
the proper annotations.


#### Causality Annotation Rules and Regulations

Because causality is a difficult concept, easy to over- or under-apply,
we do have some specific guidelines below which you should use to
guide your annotation of BEFORE/CAUSES, OVERLAP/CAUSES, and BEFORE/PRECONDITIONS,
referred to collectively below as ``Causal links'' or ``Causal
annotations'':


#### Causality is specific to the instance, not to the concept

Keep in mind that we are not determining causation or preconditioning
based on our understanding of the sequence of events leading up to
an abstract instance of the particular eventuality in question. Instead,
we are examining and taking as truth what actually happened \textit{in
this case}, based on the text. For example:

- *Dropping* the *pistol* caused *it* to *fire*,
*destroying* the nearby *fan*. \a. *Dropping* BEFORE/CAUSE
*fire* \b{.} *fire* BEFORE/CAUSE *destroying* \b{.
*pistol* IDENTICAL *it*

It is rare for modern pistols to fire when dropped, and even less
the case that all pistols destroy fans when fired. However, \textit{in
this particular case}, both the firing and the destruction did happen,
and the causal relationship is quite clear.

Similarly, earthquakes do not \textit{always} cause destruction of
cities, nor does the discovery of Uranium always cause revitalization,
but that does not matter for the annotation of \ref{nzquake} or \ref{moaburanium},
as in both cases, the causal relationship is asserted.

So, do not concern yourself with probability or what \textit{usually
causes something, and remember that CAUSE and PRECONDITION annotations
are EVENT specific. A given CAUSES relation just ties together two
specific instances, and does not assert a greater relationship between
two conceptual EVENTs.


#### Focus on relations suggested in the text

\label{causessuggestedintext

You should focus on the relations that the writer suggests, instead
of over-analyzing the text, or searching for causality where it may
not otherwise exist. For example, in \ref{nzquake}, you could argue
that *established* BEFORE/PRECONDITIONS *destroyed*, meaning
that if the city had not been established, it would not have been
destroyed. This is a case where inference and world understanding
should be used with some caution. For example:

- *Smith* *complained* about being *bullied* before
*stabbing* two *people* at the *school*.

- *Smith* *complained* about being *hungry* before
*stabbing* two *people* at the *school*.

In \LLast, we would not want to infer that bullying caused (or even
preconditioned) the stabbings, for the same reasons that we would
not infer that *hungry* caused or preconditined the stabbings.
Remember that although the difference between ``hungry'' and ``bullied''
in this context is clear to humans, that understanding does not extend
to machines.

We must be particularly cautious when we search for new causal relations.
After all, anything that happened in the past can precondition a later
EVENT, and there are a great many logically true preconditions which
do not warrant annotation (``All murders are predicated on the birth
of the victim, because one cannot kill a person who never existed'').
So, if although a relation may be logically or inferably true, if
the writer is not suggesting such preconditioning or causation, and
there is nothing \textit{in the text} to suggest the relation, it
should not be marked. Please focus on the relations that the writer
suggests, as they will be the most relevant, useful, and learnable.


#### Look for causal language to guide causal annotations

You should consider creating a CAUSES link when you see words and
phrases such as ``cause,'' ``because of,'', ``due to,'' ``incite,''
``trigger,'' etc. Similarly, PRECONDITIONS links are indicated by
words like ``let'', ``enable,'' ``allowed'', ``lead to'',
etc.

- An *ambush* in the rural Kunar province triggered a day-long
*battle* between Coalition forces and Taliban soldiers. \a. *ambush*
BEFORE/CAUSES *battle* \b{.} Do not annotate as *ambush*
BEFORE/CAUSES *trigger*.

As seen in \Last, these relational words themselves, however, should
not be included in the CAUSES/PRECONDITIONS links, and in fact should
not be marked as EVENTs at all, as they share the temporality of the
causing event (e.g. of *ambush* in \Last).


#### Causal annotations can only link EVENTs to one another

TIMEX3s cannot be in CAUSES or PRECONDITIONS links:

- The vault will be *opened* on **June 24th**. \a. **June
24th** CONTAINS *opened*

Even if the humans (or mechanisms) controlling the vault's opening
will not allow it to happen until the 24th, ultimately, it is not
the change in calendar date which causes (or even preconditions) the
opening. The date, however ardently awaited, is arbitrary.

Similarly, as with all TLINKs, CAUSES and PRECONDITIONS links cannot
include ENTITYs. Animate objects, or groups of them (e.g., officers,
John, the government, Army) should not be included in a CAUSES/PRECONDITIONS
link, because they should not be annotated as events to begin with:

- The <ENTITY officers> <EVENT arrested> the drug traffickers.

There is no causality here, as at best, you would be stating that
the existence of the officers caused the arrest. This is logically
true, but ultimately silly.


#### Objects described as causes, effects, or preconditions must be METONYMIC

If an inanimate object is described as a cause/effect/precondition,
mark it as a IMPLICIT EVENT, so that it can be linked:

- The *drug* *raised* *her* *blood* *pressure*.
\a. *drug* OVERLAPS/CAUSES *raised*

Here, the administration or the chemical effects of the the drug are
causing the raise, rather than the drug itself. Thus, we can mark
the drug as METONYMIC.

- The balance *sheets* caused them to *favor* the *spin*
off. \a. *sheets* OVERLAPS/CAUSES *favored*

Here, the ``balance sheets'' refer to the analysis of the financial
state of the company, rather than to the sheets of paper themselves.
It is this analysis, captured through IMPLICIT marking, which caused
the favoring. Compare \Last with \Next:

- The balance *sheets* clearly *show* why they *favored*
the *spin* off.

Although almost identical with \LLast, \Last isn't showing any temporal
or causal information. The favoring could have happened before the
balance sheets were ever analyzed or created. The fact that the the
balance sheets show why the spin-off was favored does not mean that
the balance sheets caused the favoring to happen.


#### Do not create causal links between verbs and their arguments

Every verb has expected actors or ``semantic roles'', as annotated
in PropBank or AMR. These expected arguments, for instance, the hitter,
thing hit, and instrument used in a hitting event, are linked by the
verb's semantics, and a causal link is not needed to capture this
meaning. Similarly, it is not useful to emphasize the relationship
between a creation EVENT and its product.

No causal links would be made below:

- *Salt Lake City* *hosted* the 2002 *Olympics*. \a.
*hosted* OVERLAP *Olympics*

- *Stringer Bell* *called* a *summit*. \a. *called*
BEFORE *summit*

- *Kevin* *cooked* Thanksgiving *Dinner*. \a. *cooked*
BEFORE *dinner*

- The *general* *ordered* *strikes* in *retaliation*
for recent terrorist *attacks*. \a. *attacks* BEFORE/PRECONDITIONS
*retaliation* \b{.} *strikes* IDENTICAL *retaliation*

In all of these cases, the verb semantics will reveal the link in
a clearer and more nuanced way than causal annotations.


#### EVIDENTIAL EVENTs should not be causally linked to those things which
they demonstrate

Do not create a CAUSES/PRECONDITIONS link between things that show
(*scans*), the showing events (*showed*), and things that
are shown (*lymphomas*). The same goes with other evidential events
(seeing, saying, etc.):

- *Scans* through the lower neck and upper chest *showed*
malignant *lymphomas*. \a. *scans* OVERLAP *lymphomas*
\b{.} *scans* OVERLAP *showed*

Although it is logically true that without scanning, nothing could
be shown, and that the showing creates the understanding of the presence
of lymphomas, no CAUSES or PRECONDITIONS links should be made here.
Similarly:

- *Obama's* *statement* *revealed* the *extent*
of the *drone* *program*.

Here, the statement does not CAUSE revelation, nor does the revelation
CAUSE the extent.


#### Assume the writer of the text is reliable

For quoted speech or reporting, assume that the narrator or writer
is reliable, unless otherwise indicated:

- On **Sunday**, he *said*, *one* of the *bombs* *wrecked*
the family's home. \a. *one* OVERLAPS/CAUSES *wrecked* \b{.
**Sunday** CONTAINS *wrecked* \b{.} *bombs* SET/MEMBER *one*

- *Frank* *claims* that an *alien* mind-control *beam*
made *him* *rob* the *bank*. \a. *beam* OVERLAP/CAUSES
*rob* \b{.} *Frank* IDENTICAL *him* \c{.} *claims*
REPORTING *beam*

Remember, you are not a jury, and it is not your role to determine
the accuracy of asserted causal claims, but to simply annotate them.


#### Each EVENT can participate in multiple CAUSES or PRECONDITIONS links

There can be multiple causes and preconditions for a single event:

- After *loading* *his* *pistol* and *chambering*
a *round*, the *instructor* *pulled* the *trigger*
and *fired* a *shot* as a *demonstration*. \a. *loading*
BEFORE/PRECONDITION *fired* \b{.} *chambering* BEFORE/PRECONDITION
*fired* \b{.} *pulled* BEFORE/CAUSE *fired*

Similarly, a single EVENT can cause or precondition several other
EVENTs:

- *He* has *seen* *people* *decapitated* by barrel
*bombs* and *others* who *lost* *their* *limbs*.
\a. *bombs* OVERLAPS/CAUSES *decapitated* \b{.} *bombs*
OVERLAPS/CAUSES *lost* \c{.} *others* IDENTICAL *their*


#### Causal links can cross sentence boundaries

As with other forms of TLINK, CAUSES/PRECONDITIONS links can cross
sentence boundaries, where necessary:

- She *said* the *bombs* *rained* down on them for
two days. The children are *terrified* as a result, she *said*.
\a. *rained* BEFORE/CAUSES *terrified*

However, EVENTs that are too far apart (crossing multiple sentence
boundaries) should not be linked to each other, as there is likely
no way to determine causation besides human inference:

- A terrorist group has *claimed* responsibility for the suspect
packages. (...) The group *formed* just before the London *Olympics*
in 2012. \a. *formed* BEFORE *Olympics* \b{.} Do not annotate
as *formed* BEFORE/PRECONDITIONS *claimed*


#### Causal links should be chained where possible

Causality, as a phenomenon, tends towards the formation of complex
chains. One event may cause another, which in turn preconditions a
third, and that may cause several others, and so forth.

Although this leads to complexity, we can leverage these chains in
annotation, to allow us to communicate the foundational role of earlier
causation in the eventual outcome:

- *He* was *jailed* after *pleading* guilty in *court*
following a series of *burglaries* and *muggings* in **November
2013**. \a. *burglaries* BEFORE/PRECONDITIONS *pleading*
\b{.} *muggings* BEFORE/PRECONDITIONS *pleading* \b{.} *pleading*
BEFORE/CAUSES *jailed*

Rather than stating explicitly that the burglaries and muggings precondition
his jailing, we can state (rightfully) that they preconditioned his
plea, and that the plea caused his jailing. The chain can then be
followed through basic logic. Similarly:

- The death toll from a *bombing* in Bangkok *rose* to
three on Monday after a doctor *confirmed* that a six-year-old
girl had *died* from her *injuries*. \a. *bombing* OVERLAP/CAUSES
*injuries* \b{.} *injuries* BEFORE/CAUSES *died* \c{.
*confirmed* REPORTS *died* \d{.} *died* BEFORE/CAUSE
*rose*%
\footnote{The word ``after'' indicates a BEFORE link instead of an OVERLAP
link, even though in reality, the death toll rises simultaneously
with the confirmation of death.%
} \e. *confirmed* BEFORE/CAUSES *rose*

Here, again, we can infer the broadest link (\textquotedbl{}the bombing
caused the death toll to rise\textquotedbl{}) by a series of small
logical jumps through CAUSES annotations.

These chained annotations, much like narrative containers, allow us
to leave easily inferable links unspecified. In this way, we can fully
capture the causal nature of the situation without specifying every
small step.


#### ALINK annotations should not be interpreted causally

Do not create CAUSES/PRECONDITIONS links between the source (e.g.
\textit{started}) and the target (e.g. \textit{attacking}) of ALINKs:

- The *terrorists* *started* *attacking*. \a. ALINK:
*started* INITIATES *attacking*

Although it is tempting to claim that the start of the attack causes
the attack, it's somewhat tautological, and completely useless to
us. Similarly:

- *We* will *restart* the *investigation* after the
*holiday*. \a. ALINK: *restart* REINITIATES *investigation*

The investigation has already been caused by something else, and its
reinitiation is in no way causal.

Note that ASPECTUAL events can CAUSE or PRECONDITION other EVENTs
which are not the target of the associated ALINK:

- Several months after *quitting* *smoking*, his *singing*
got so much *better*. \a. *quitting* BEFORE/CAUSES *better*
\b{.} ALINK: *quitting* TERMINATES *smoking*


#### When in doubt, leave it out!

If the situation is not clear with respect to causality or preconditioning,
do not create a CAUSES/PRECONDITIONS link, and use a plain temporal
relation instead:

- *Politicians* *condemned* the *attacks*, *saying*
*they* were a deliberate *effort* to *incite* sectarian
*strife* and *undermine* the *country*'s fragile *democracy*.
\a. *effort* OVERLAPS *strife* \b{.} *strife* OVERLAPS
*undermine* \b{.} ALINK: *incite* INITIATES *strife*

Do not mark *effort* OVERLAPS/CAUSES *strife* nor *strife*
OVERLAPS/CAUSES *undermine*, as both would rely on inference,
and on pessimism (that the attacks would be successful).

Similarly:

- *She* *drank* *Diet Mountain Dew* like *water*,
and **now** *she* has *cancer*. \a. (Because DocTimeRel differs,
no TLINK between *drank* and *cancer* is needed) \b{.} *She*
IDENTICAL *she*

As with some of the examples in Section \ref{causessuggestedintext},
the juxtaposition of the two EVENTs pragmatically implies a causal
link, but no causality is asserted firmly (nor easily inferable).
Thus, the link should not be created.


#### Causation and Precondition TLINK Use

If, even after evaluating the EVENTs in light of the regulations above,
you belive there to be a markable causal relationship, you must choose
among the three causal annotation types.


#### BEFORE/PRECONDITIONS

As such, if you understand two EVENTs to have a relationship of preconditioning,
your sole choice is to create a BEFORE/PRECONDITIONS link.

- *She* *unlocked* the *vault*, *disabled* the
*cameras*, and *distracted* the *guard* so that *he*
could *steal* the *gold*. \a. *unlocked* BEFORE/PRECONDITIONS
*steal* \b{.} *disabled* BEFORE/PRECONDITIONS *steal*
\b{.} *distracted* BEFORE/PRECONDITIONS *steal*

Because preconditions are defined as EVENTs which must have happened
in order for a later EVENT to happen, temporally speaking, all PRECONDITIONS
must start BEFORE the EVENT which they precondition.


#### BEFORE/CAUSES

If the relation between two EVENTs is causal, that is, that one EVENT
\textit{necessarily} causes the other, you must evaluate its temporality.

In many cases, the causing EVENT will have ended before the effect
fully takes place. In these cases, BEFORE/CAUSE is the only prudent
annotation.

- The *bear's* *visit* forced the *city* to *adopt*
a new *trash-can* *design*. \a. *visit* BEFORE/CAUSE
*adopt*

It is clearly the case that the adoption did not happen while the
bear was still in town, so the cause is BEFORE the effect, and BEFORE/CAUSE
is prudent.

- *France's* *declaration* caused *tension* with *Russia*.
\a. *declaration* BEFORE/CAUSE *tension*

The declaration did not, itself, cause tension with Russia in the
same way that an earthquake causes damage. Instead, its interpretation
and analysis by the Russians caused the tension. This means that there
was a non-trivial lag between cause and effect, and that BEFORE/CAUSE
is prudent.

- *Switching* *textbooks* led to *improvements* in
*scores*. \a. *switching* BEFORE/CAUSE *improvements*

Again, it is not the case that the improvement occurred \textit{during
the switch, so BEFORE/CAUSE is prudent.

- *He* *shot* and *killed* the *attacking* *soldier*.
\a. *shot* BEFORE/CAUSE *killed*

*shot* here refers to the act of discharging a firearm. Even assuming
an immediate and painless death for the attacker, there is a (very
small) lag between the discharge and the death. Put differently, it
is not the case that at any point, this specific shot and killing
were occuring at the same moment. So, BEFORE/CAUSE.

- The *bus* *kneeled* to allow *access* to the elderly
*man*. \a. *kneeled* BEFORE/CAUSE *access*

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

- The *earthquake* *destroyed* the *palace*. \a.
*earthquake* OVERLAP/CAUSES *destroyed*

At some point in time, the destruction had begun while the earth was
still quaking, and thus, the two EVENTs are in an OVERLAP/CAUSES relationship.

- *His* *coldness* made *Kerri* *uncomfortable*.
\a. *coldness* OVERLAP/CAUSES *uncomfortable*

Her discomfort and his coldness are both durative EVENTs, and it is
extremely likely that she began feeling discomfort before his coldness
had ended. Thus, OVERLAP/CAUSES.

- The *attacks* resulted in 89 *deaths*. \a. *attacks*
OVERLAP/CAUSES *deaths*

It's likely that deaths occurred during each individual attack, and
when taken as a plural sum, it is certain that the span of the ``attacks''
contains at least one death.

Note that the semantics of participating EVENTs have a strong role
in the choice of BEFORE/CAUSES vs. OVERLAP/CAUSES. For instance:

- The *explosion* caused mass *hysteria*. \a. *explosion*
BEFORE/CAUSE *hysteria*

Here, it's fairly clear that the hysteria began after the explosion,
rather than the physical blast causing the hysteria as it propagated.
Compare to:

- The *explosion* caused many *injuries*. \a. *explosion*
OVERLAP/CAUSE *injuries*

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

\vspace{0.25cm
 \fbox{ %
\begin{tabular}{p{0.6in}p{14cm}
\includegraphics[width=0.5in]{warning} \\
\textbf{Caution!}  & \raisebox{4mm}{%
\parbox[c]{14cm}{%
\vspace{2mm
\textit{Avoid ``millisecond reasoning''. If you find yourself attempting
to justify OVERLAP/CAUSES by saying ``Well, there was probably a
few milliseconds of hysteria which started before the end of the bomb's
explosion...'' or ``Maybe he was injured slightly by the shockwave
ahead of the sub-sonic bullet which hadn't yet left the barrel, thus,
during the *shot*...'', stop. OVERLAP/CAUSES is intended for
those causal EVENTs which are durative and causing an effect throughout
their duration, rather than for those with coincidental or miniscule
overlap between cause and effect. These annotations will be difficult
enough without adding this additional agony.}%
}}\ \
\tabularnewline
\end{tabular}} \vspace{0.25cm



#### Causal TLINK Properties

Polarity and Modality apply to causal TLINKs in the same way that
they apply to other TLINKs. See Sections \ref{TLINKPolarity} and
\ref{TLINKModality} for a full description.

\color{black

%%%% ANNOTATING ALINK %%%%



###Event Coreference

\label{corefannotation-1

While linking up events in terms of their temporal, causal and subevent
structure, you will also be marking them for event coreference. These
guidelines for coreference annotation have been adapted from the OntoNotes
v. 7.0 (\cite{pradhan2007ontonotes}) and ODIE (2010) guidelines as
needed to accommodate the objectives of the RED schema. Additional
concepts and information were synthesized from Poesio et al. 2004
(\cite{poesio2004centering}), Poesio 1997 (\cite{poesio1997conversational}),
and Savova et al. 2011 (\cite{savova2011anaphoric}).


#### IDENTITY

Two events have an IDENTICAL relation if they refer to the same event
in space and time. The IDENTICAL relation has several important semantic
characteristics%
\footnote{Following the MUC-7 specifications%
}: 
\begin{itemize
- The relation is symmetrical, i.e., non-directional: (if A is IDENT
to B, then B is IDENT to A). This is different from relations like
WHOLE/PART and SET/MEMBER, which are directional by defition. 
- It is also transitive: if A is IDENT to B and B is IDENT to C, then
A is IDENT to C. . 
\end{itemize

#### \label{sub:SET-MEMBER-1}SET-MEMBER

A SET-MEMBER relationship exists when one event can be thought of
as being an instane of a larger set of events. In annotating this
over events, you are to decide between SET-MEMBER and CONTAINS-SUBEVENT.
You should remember to use CONTAINS-SUBEVENT for all cases in which
an event is temporally within, and part of the script of, a larger
event. 

SET-MEMBER can occur between multiple ACTUAL events when the SET is
an actual agglomeration of instances that are not a temporally continguous
unit, as in \Next 

- A series of *earthquakes*$_{S}$ struck the province of
Manokwari last Tuesday. The largest *earthquake*$_{M}$ alone
caused \$73 million in damage.

Other SET/MEMBER relations will be between generalizations and their
instances
\begin{examples
- Presidents usually *\textsubscript{SET} pardon* a turkey for
Thanksgiving, and today the lucky convict he *\textsubscript{MEMBER
pardoned* was named Ginny Fawell. 
\end{examples

#### BRIDGING

As with entities, if you are unable to use one of the previously discussed
links, but it is apparent that some sort of coreference link exists
which entails that the events have some sort of link, then use the
BRIDGING relation. For dealing with EVENT coreference, an important
option that this opens up is when a text alledges that doing one event
is analogous to doing another, either directly or in an attempt at
metaphor:
\begin{examples
- John *\textsubscript{head} voted* to make waffles the state food,
which *\textsubscript{attribute} amounts* to betraying all his
campagin promises.
\end{examples
Because we define CONTAINS-SUBEVENT as involving temporal containment,
you may also use BRIDGING for any subevent which seemed to be ``part
of'', yet temporally outside of, another event.

- After a week of attempted repairs, the palace *collapsed*
Friday, the most disheartening part of the already-terrible *earthquake*.
\a. *earthquake* BEFORE-CAUSE *collapsed* \b{.} *earthquake*
BRIDGING *collapsed*


#### General Guidelines for Annotating Coreference

\label{corefguidelines-1


#### Never link EVENTs to ENTITIES

In all coreference relations (IDENTICAL, APPOSITIVE, WHOLE/PART, AND
SET-MEMBER), Entities can be linked to Entities, and Events can be
link to Events, but Entities and Events will never be linked within
the same coreference relation. If you encounter an occasion where
you are tempted to do this, check that your Entity is not actually
an Event, or that your Event is not actually an Entity, as the case
may be.


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

- *I*$_{M1}$ met with the *patient*$_{M2}$ today. *We*$_{S1}$
discussed treatment options for *her*$_{M2-1}$ cancer. *We*
also reviewed in *our*$_{S2}$ discussion the results of *her*$_{M2-2}$
recent CT-scan. *My*$_{M1}$ recommendation is adjuvant chemotherapy.
\a. SET *We*$_{S1}$: MEMBERs *I*$_{M1}$, *patient*$_{M2}$,
*her*$_{M2-1}$ \b{.} SET *our*$_{S2}$: MEMBERs *her*$_{M2-2}$,
*My*$_{M1}$

In this example, *I*$_{M1}$ and *My*$_{M1}$ are IDENTICAL;
*patient*$_{M2}$, *her*$_{M2-1}$, and *her*$_{M2-2}$
are IDENTICAL; and *We*$_{S1}$, *We*, and *our*$_{S2}$
are IDENTICAL.


#### Don't link ACTUAL and GENERIC items

In analogy with the principle for not TLINKing HYP/GEN to ACT/UNCERTAIN
events, ACTUAL and GENERIC items can never be in an IDENTICAL, APPOSITIVE,
or WHOLE/PART relationship. They can, however, be SET/MEMBER, as in
\Next:

- *I* discussed with *Mrs. Ambry*$_{ACTUAL}$ the results
of a local clinical trial in which *patients*$_{GENERIC}$ with
*cancer*$_{GENERIC}$ recovered successfully on the *drug*
without reoccurrence. Given *her* colon *cancer*$_{ACTUAL}$
and the success of the *drug*, *I* recommend *it*. \a.
SET *patients*: MEMBER *Mrs. Ambry* \b{.} *Mrs. Ambry*
IDENTICAL *her* \c{.} SET *cancer*$_{GENERIC}$: MEMBER *cancer*$_{ACTUAL}$
\d{.} *I* IDENTICAL *I* \e. *drug* IDENTICAL *drug*,
*it*


###Aspectual Link Annotation

\label{alinks

The next annotation performed on the data is the ALINK (or ``aspectual
link'') annotation. ALINKs are created between an aspectual EVENT
and a non-aspectual EVENT. Any EVENT previously marked with the class
ASPECTUAL will be ALINKed to another, non-aspectual event, and you
will never make an ALINK which includes a TIMEX3 or two non-aspectual
EVENTS. ALINKs only occur when you have an aspectual EVENT, and are
much less common in the text than TLINK annotations. Relatively few
EVENTs will have an associated ALINK.

As with TLINKs, they are created interactively, and have the basic
form:

- EVENT1 *aspectual relation* EVENT2

But unlike TLINKs, no matter the circumstance, an ALINK should never
cross a sentence boundary.


#### ALINK sub-types

There are four different aspectual relations used in the schema, CONTINUES,
INITIATES, REINITIATES, and TERMINATES.


#### CONTINUES

CONTINUES is used when an aspectual event shows the continuation of
another event:

- We *continue* to *fight* tyranny in all its forms. \a.
*continue* CONTINUES *fight*

- The rebels have announced that they will *keep* *pressing*
towards Damascus. \a. *keep* CONTINUES *pressing*

- The patient will *remain* on *dialysis* until her condition
*changes*. \a. *remain* CONTINUES *dialysis* \b{.} *remain*
ENDS-ON *changes*

- She is not interested in pursuing chemotherapy at this time
but is interested in *continued* *surveillance*. \a. *continued*
CONTINUES *surveillance*

- We will *continue* to *monitor* heart rate and rhythm
along with serial cardiac markers and electrocardiograms to rule her
out for any cardiac involvement. \a. *continue* CONTINUES *monitor*


#### INITIATES

INITIATES is used when an aspectual event indicates the start or initiation
of another event:

- **2008** marked the *start* of the rebels' brutal *campaign*.
\a. *start* BEGINS-ON **2008** \b{.} *start* INITIATES *campaign*

- Patient will *begin* a high-fiber *diet* upon *release*.
\a. *begin* INITIATES *diet* \b{.} *begin* BEGINS-ON
*release*

- We will *start* Ms. Miller on a normal saline *infusion*
at 75 an hour for a total of 1 L. \a. *start* INITIATES *infusion*

Note that INITIATES carries an implied sort of causality (beginning
something, by definition, causes it to start). This causality need
not be marked, so long as the ALINK is present.


#### REINITIATES

REINITIATES is used when an aspectual event indicates that another
event will be restarted or reinitiated:

- The latest *bombing* broke the treaty, *resurrecting*
*violence* throughout the city. \a. *resurrecting* REINITIATES
*violence*

- *Levaquin* 750 mg p.o. q. day (will *restart* **today**)
\a. *restart* REINITIATES *Levaquin* \b{.} **today** CONTAINS
*restart*

- His anterior chest *rash* has not *reoccurred* since
the *PCN* VK was *discontinued* **24-hours ago**. \a. *discontinued*
TERMINATES *PCN* \b{.} *discontinued* BEFORE *reoccurred*$_{NEG}$
\b{.} *discontinued* OVERLAP **24-hours ago\

As with INITIATES, reinitiates carries an implied sort of causality.
This causality need not be marked, so long as the ALINK is present.


#### TERMINATES

TERMINATES is used when an aspectual event indicates the ending of
another event:

- The latest *treaty* should finally *end* the *bloodshed*.
\a. *end* TERMINATES *bloodshed*

- Because of this *reaction*, *Allegra* will be *discontinued*.
\a. *discontinued* TERMINATES *Allegra*

- We will *hold* her *heparin* until after the *surgery*.
\a. *hold* TERMINATES *heparin* \b{.} *hold* ENDS-ON
*surgery*

- Patient *nausea* was successfully *stopped* by 1-mg
*Ativan* p.r.n. \a. *stopped* TERMINATES *nausea*

\vspace{0.25cm
 \fbox{ %
\begin{tabular}{p{0.6in}p{14cm}
\includegraphics[width=0.5in]{warning} \\
\textbf{Caution!}  & \raisebox{4mm}{%
\parbox[c]{14cm}{%
\vspace{2mm
\textit{ALINKs are much less common than TLINKs, usually only a few
per document, but they are no less important and easy to overlook.
Remember that any time you have an EVENT which has the type ASPECTUAL,
you will need to create at least one ALINK.}%
}}\ \
\tabularnewline
\end{tabular}} \vspace{0.25cm



###REP - Reporting Annotation

Reporting Annotations link EVIDENTIAL EVENTs to those EVENTs that
they report. For instance:

- A Kurdish newspaper *said*$_{R}$ Wednesday that Iraqi members
of an Al Qaeda- linked group, a Kurd and an Arab, *blew*$_{E}$
themselves up in northern Iraq on February 1, *killing*$_{E}$
at least 105 people.

- The newspaper *added*$_{R}$ that bin Mahmud is the brother
of a man whose alias is Abdullah Al-Shami, an Ansar al-Islam leader
who was *killed*$_{E}$ last year while *fighting*$_{E}$
a US-backed *onslaught*$_{E}$ by the PUK that *forced*$_{E}$
the group out of its enclave near the Iranian border at the end of
March last year.

Here, we are linking the Report itself with the Event that was reported.
The EVENTs that can serve as a Report appear to be a restricted class,
mostly the verbs ``say'', ``tell'', and ``report'', and will
always be an EVENT of the type EVI. The events serving as Event, what
was being reported, are restricted to only the EVENTs in the remainder
of the sentence, unless we have some explicit rationale we can point
to that the report does not cover an in-sentence event, or that the
report continues outside the sentence boundary. In the latter case,
it should only be for cases of direct quotations including multiple
sentences.

- Mr. Jones *said*$_{R}$, ``I'm not *sure*$_{E}$ when
our company will go *public*$_{E}$. It will not be before we
*acquire*$_{E}$ Vandelay Industries.\textquotedbl{

If there are multiple EVENTs reported by the same EVI event, as in
the examples above, only one REPORTING link will be created, with
all of the reported events linked to the same EVI event in the same
relation.


###Special Cases, Constructions and Edge Cases


#### Metaphorical and Figurative Language

You may be asked to annotate some particularly natural natural language
speech. In such discourse, you'll find metaphorical expressions, figures
of speech, and idioms which are not straightforwardly representing
the sequence of EVENTs and the ENTITYs which live in the text.

When you find such expressions and phrases, we encourage you take
them at face value, and annotate them naively, as would a non-native
speaker who doesn't fully understand what's going on. Take, for instance:

- *John* *kicked* the *bucket* **last week**.

- *She*'s *off* *her* *rocker*.

- That *accountant* is a *snake* in the *grass*.

- *My* *head* *exploded* when *I* *found*
out.

- *That* *flew* right over *his* *head*.

In all of these cases, even though we know better, we must treat the
EVENTs as literal EVENTs (e.g. John quite literally kicked something,
his head exploded into fragments, and ``that'' was briefly airborne).
Similarly, although they're likely to be singletons (barring exceptionally
cute wordplay), we need to grab entities like the kicked bucket, the
grass inhabited by the snake, and the rocker she was recently separated
from.

Even though this may seem unsatisfying, a surprising amount of this
information can be recovered by verb sense disambiguation (``Kick''
has a `the bucket' sense which is specified as meaning ``death''),
and by work being done in other contexts. Because we are working directly
with the text (rather than at some abstract level), we must mark the
text as it stands and allow humans to parse as we do best.

\color{blue


#### Exclamations, Interjections, and Emphatics!

Natural language data, especially chats, emails, and discussion forum
data, is full of emphatics, interjections, and exclamations which
are not propositions per se, but simple statements of emotion or empathy.

We distinguish two types of exclamations/emphatics/interjections:
Emotional vs. Evaluative interjections.

Emotional interjections are short, off-the-cuff emotional statements,
which are generally formulaic, often are not complete statements,
and make no assertion, serving only to signal an emotional reaction.
Although the surrounding sentence can and should be annotated, these
statements (in <angle brackets> below) are not annotated.

- <Holy crap!> Cher actually showed up!

- <OMG> I can't believe you met Justin Bieber.

- \$300,000?! <Goodness Gracious Great Balls of Fire!>

- Me? Watch a Michael Bay movie? <Hell no!>

- The Computer Science department's softball team asked me to
play for them. <As if!!>

- <F{*}{*}{*} yes> I'll take a free cupcake!

These contrast with evaluative exclamations which actually provide
a subject and predication, generally elided (although identity is
perhaps pragmatically determined, and are just regular statements,
forcefully put). These should still be annotated, along with their
nearby context.

- *You* *hurt* *yourself* *playing* *softball*?
*Poor* *you*! \a. *You* IDENTICAL *yourself*, *you*
\b{.} *Poor* is an EVENT (OVERLAP, POS, ACT)

- *He* *posed* as a *lawyer* and *stole* *her*
*savings*? What a *scumbag*! \a. *He* IDENTICAL *scumbag*
\b{.} *He* BRIDGING *lawyer*

- *He* *hooked* up with *Mark*? *I* can't *believe*
*it*! \a. *hooked* IDENTICAL *it*

- *Your* *leg* is *broken*? *That* *sucks*!
\a. *broken* IDENTICAL *That*

- *You* *got* the *job*? *You* are sooooooo *lucky*!!!1!
\a. *You* IDENTICAL *You*

Put differently, you are welcome to annotate those exclamations to
which our schema applies, where statements are being made about ENTITYs
and EVENTs through well-formed topic-predication style sentences,
but those exclamations or interjections which don't fit the linguistic
mold can safely be discarded.


#### Annotating Sarcasm

Detection of sarcasm is not among RED's goals at the moment, but the
detection of EVENTs, ENTITYs and TIMEX3s within sarcastic speech is.
So, even though the intent of the speech may be sarcastic, the speech
itself should still be taken literally and annotated accordingly.

- Yeah, 40-year-old me *loves* going to Chuck E. Cheeses.
The food is so *good*. \a. *love* and *good* would be
ACT, POS, despite the implications otherwise.

- Uh-huh, Laura's going to *cook* me dinner. As if! \a. *cook*
would be ACT, POS, with a DocTimeRel of AFTER.

Another way to think about this is that even though the illocutionary
force and meaning of the statement can be interpreted differently,
linguistically, the speaker is simply stating a fact. To mark the
force rather than the literal interprtation would be confusing to
the computer, and without annotating sarcasm explicitly, it would
hurt our models more than the data would help. \color{black

\begin{comment
\color{blue


#### Metaphorical and Figurative Language (MkII)

You may be asked to annotate some particularly natural natural language
speech. In such discourse, you'll find metaphorical expressions, figures
of speech, and idioms which are not straightforwardly representing
the sequence of EVENTs and the ENTITYs which live in the text.

When you find such expressions and phrases, we encourage you take
them at face value, and annotate them naively, as would a non-native
speaker who doesn't fully understand what's going on. In all of these
cases, even though we know better, we must treat the EVENTs as literal
EVENTs (e.g. John quite literally kicked something, his head exploded
into fragments, and ``that'' was briefly airborne).

However, when annotating idiomatic speech, ENTITYs or EVENTs which
have no conversational referent should not be annotated. Put differently,
if an ENTITY or EVENT is used in an idiom which cannot be paraphrased
by replacing it with another ENTITY or EVENT from the remainder of
the note, it should not be marked.

Take, for instance:

- *John* *kicked* the bucket **last week**.

- *She*'s *off* *her* rocker.

- That *accountant* is a *snake* in the grass.

- *He* left officer *school* because he couldn't *cut*
the mustard.

In these examples, ``bucket'', ``rocker'', ``grass'' and ``mustard''
are not referential within the conversation, and cannot be mapped
to anything else outside of that figurative meaning. The *snake*
is referent, though, as the speaker has stated that the accountant
is IDENTICAL to the snake.

Please try to avoid coercing elements of idioms into reference:

- *Stop* *beating* around the bush and just *sell*
the *car*.

- *Mary* *rode* shotgun, and the falling *rocks* *missed*
the passenger *seat* by inches.

- *She* got a *taste* of *her* own medicine when *Sarah*
*cheated* on *her*.

- *Matt* *stole* *my* thunder by *announcing*
the product.

Do not, for example, attempt to interpret ``bush'' as IDENTICAL
to the sale, attempt to corefer ``shotgun'' to the physical passenger
seat, equate ``cheating'' with her medicine, or claim that ``thunder''
\textit{is} the announcement. To make any of these links would require
us to ignore some part of the larger meaning of the word or idiom
(e.g. there's more to ``thunder'' than the act of announcing), and
thus, do not constitute true coreference.

However, there are sometimes true referents within idiomatic expressions:

- *My* *head* *exploded* when *I* *found*
out.

- *That* *flew* right over *my* *head*, better
*rephrase*.

- *I* *trained* for **two hours** **today**. *Practice*
makes perfect!

- *He*'s *rolling* in the *dough*. He *made* *\$50k*
**last week**!

In the first two idioms, ``head'' does have a concrete referent
(the speaker's physical head), although it is not literally exploding
or being overflown. Similarly, *practice* clearly refers to the
training, and *dough* is just another term for `money', allowing
a WHOLE/PART relationship with \$50k.

Even though this may seem unsatisfying, a surprising amount of this
information can be recovered by verb sense disambiguation (``Kick''
has a `the bucket' sense which is specified as meaning ``death''),
and by work being done in other contexts. Because we are working directly
with the text (rather than at some abstract level), we must mark the
text as it stands and allow humans to parse as we do best.
\end{comment



#### Intent and Purpose

\label{desiderative

Sometimes you may find an event like \textquotedbl{}want\textquotedbl{},
\textquotedbl{}need\textquotedbl{}, \textquotedbl{}decide\textquotedbl{},
or a purpose phrase like \textquotedbl{}I bought it to play softball\textquotedbl{}.
These all share a weird characteristic: they mark an intent to make
something happen.

Often, wanting is ACTUAL and the wanted action is HYPOTHETICAL or
GENERIC (and therefore they shouldn't be TLINKed together), but otherwise,
this often entails precondition.


\subsubsection*{How does intent relate to causation?

There are occaisional moments in which the intent cannot possibly
have an effect upon the final event; those, naturally, should have
neither cause nor PRECONDITION labels:

- he-' I really *want* Clinton to *succeed*.

The lack of desire/intent also don't show causation:

- I don't *want* to *give* the wrong impression

But if the intent and its events are of the same modality, and some
sort of causation may be going on, default to PRECONDITION:

- I've *decided* I'm not *going* to fight it.

- Before that, I *wanted* to *come* back

- and caregivers are *needed* to *provide* guidance


\subsubsection*{Are these OVERLAP? BEFORE?

It's often similarly vague what the temporal relationship there is
between \textquotedbl{}want\textquotedbl{} and the wanted event, \textquotedbl{}need\textquotedbl{
and the needed event, etc. Whenever it's unclear, default to OVERLAP
(so mostly use OVERLAP/PRECONDITION):

- Before that, I *wanted* to *come* back


#### Requesting, Asking, Promising

As with wanting, and needing, requests usually aren't direct causation.
Even if it seems unlikely that someone will decline the request, we
don't want you start guessing social hierarchies: if there is some
form of causation, treat is as PRECONDITION (this should almost always
be BEFORE/PRECONDITION).


#### Restatement, reframing, equating

Sometimes, events will be followed by another event, that can be interpreted
as a restatement of the last mention:

- Her mother had recently *died* , effectively *rendering*
her an orphan.

- The cartels were deeply *rooted* in Mexico, effectively
*controlling* municipalities across the country and even entire
states.

If the two events are very clearly identical, feel free to use IDENT.
If they are similar but not identical (as the above examples), you
can related them with BRIDGING. Either way, the important think is
to be consistent with later events; all TLINK and other relations,
if at all possible, should be linked to the first of the two elements.


#### Avoiding Inference in Temporal Relations

One thing to keep in mind when annotating is that you, being human
with even basic understanding of the world and of the way that medicine
works, will easily be able to infer relations that are simply not
present in the text. Take, for example, the below sentence:

- We *diagnosed* her *cancer* {last week}.

Here, it is very tempting to want to assign the cancer and the diagnosis
different temporal realities, to claim that the cancer preceded the
diagnosis (as well as last week), and that the diagnosis was simply
one point in a longer history of cancer.

However, we do not really know that the cancer preceded the diagnosis,
and it is really human inference that gives us that information. It
is possible, however remotely, that the cancer could have existed
since birth, or perhaps cropped up 5-10 minutes before the biopsy.
Regardless, we know that the diagnosis and cancer OVERLAP, but we
do not know much else.

Similarly:

- A terrorist *cell* was *discovered* in March.

Again, we assume that the cell existed previously, but cannot confirm
such.

EVENT mentions are a flashbulb in a dark room. We can infer that what
we see during the flash was there before and persists after, but that's
not a level of surety at which we can annotate, unless the document
is more explicit (``We diagnosed her with carcinoma in Fall 2007,
but it was there for many years prior.'').

Compare this to the below:

- We *observed* her *seizure* {last week}.

In this case, we again have an EVIDENTIAL EVENT alongside a regular
one, but here, it would be silly to infer that the seizure has a different
temporal time frame than then observation. But note that nothing has
changed syntactically or linguistically to indicate that difference,
so this would be a very difficult point to teach a non-human. As such,
although we assume there is a different time frame for the diagnosis
and the cancer itself, we should not annotate based on that assumption.

Similarly, you will see sentences like:

- On the {12th}, she underwent an *EKG* and emergency *bypass*
following an *MI*.

As humans, we understand that the test (the EKG) likely occurred before
the invasive procedure (the bypass). But when we compare:

- On the {12th}, she underwent an *MRI* and *CT* following
a car *accident*.

We see that there is no easily understood order between *MRI*
and *CT*, and because there is no linguistic difference, just
human understanding, we should not annotate the inferred relation
between *EKG* and *bypass*.

Finally, be cautious of your intuitions when ordering EVENTs where
you have information not in the text. For instance:

- Both Pearl *Harbor* and *9/11* were huge blows to the
national psyche.

The verb tense allows us to understand that both EVENTs happened BEFORE
DocTime, and most Americans will be aware of their temporal ordering.
However, there is no evidence in the document to support the TLINK:

\a. *Harbor* BEFORE *9/11*

The TLINK would be justified, however, in:

- The national psyche suffered a huge blow with Pearl *Harbor*
and later, *9/11*.

Although this is a fairly straightforward example, check yourself
when creating TLINKs to ensure that the document supports the assertions
you're making.

This may seem like a silly point to belabor, but recall that the eventual
goal is to use this data to train software, and that software will
have no understanding of this distinction. As such, even when it seems
like you are throwing away easily recoverable information, you should
always know your audience and annotate based on the text, rather than
based on your understanding of the world.

\color{blue} 


#### Inference and Coreference

Unlike with Temporal Relations, Coreference is largely dependent on
human inference, as there are fewer grammatical cues to identity,
especially with easily-human-inferrable coreference like that between
``Will Styler'', ``William Styler'', and ``Mr. Styler''. Thus,
although we should avoid guesswork and evaluation of unclear evidence
to make IDENTICAL links, and use BRIDGING judiciously to mark coreference
situations where `it's complicated' (as discussed in Section \ref{judgement}),
the bar for ``too inferential'' is far higher for coreference than
it is for temporal relations.

\color{black


#### Discussions, Generalizations, and other EVENTs which aren't on the
timeline

\label{discussion

One of the biggest sources of difficulty for annotators is the presence
of EVENTs which do not really belong in the timeline per se, but are
present in the document. Let's use the below examples to discuss.

- \label{1stcase} We're going ahead with adjuvant *chemotherapy*
for Mrs. Parks, starting next week.

- I briefly discussed the *risks* of adjuvant *chemotherapy*
with Mr. Peloquin, along with those of several other treatment options.

- Adjuvant *chemotherapy* following *surgery* is generally
recommended in situations similar to this.

In all cases, clearly, *chemotherapy* represents an EVENT, namely,
the administration of chemotherapy as a secondary measure following
a primary treatment. However, only in \ref{1stcase} is the chemotherapy
actually on the patient's timeline, something which is presumed to
occur. In \LLast, the chemotherapy will not necessarily occur for
the patient, and in \Last, we have a generalization about patient
care, rather than a specific discussion of that patient's treatment
plan. These EVENTs are clearly not a part of the patient's actual
course of treatment, and thus should not show up on his or her timeline.
If the note reads ``We discussed her upcoming surgery as well as
the possibility for future recurrence'', we certainly do not want
``recurrence'' showing up on a factual timeline, but we certainly
would want ``surgery'' to show up.

In order to properly train our systems to find EVENTs, all EVENTs
must be marked; however, we must make sure that we can reconstruct
the reality (and the applicability to the timeline) of all EVENTs.
Our primary means for handling this is the Contextual Modality property
of EVENTs. As discussed in Section \ref{modality}, we use HYPOTHETICAL
and GENERIC to mark EVENTs which, although certainly events, do not
belong on the timeline. As you may have already guessed, in \LLast,
``adjuvant chemotherapy'' is a HYPOTHETICAL EVENT, and in \Last,
it is a GENERIC EVENT.

Using these two modalities, you should be able to annotate all of
the cases where EVENTs are discussed which do not belong on the timeline
(or belong on a hypothetical fork of the timeline).


#### Ground Rules for annotating HYP/GEN events and discussion events

As discussed previously, these EVENTs, by virtue of their modality,
aren't really on the same timeline as other EVENTs dealing with the
patient's actual care. Because of this, it can be quite tricky to
link them to the overall timeline. As such, we have a few rules, all
previously discussed, which you will find particularly useful:
\begin{enumerate
- If an EVENT is HYP, mark DocTimeRel as best you can using the same
guidelines you would for all other EVENTs, as if they were actual
EVENTs. 
- If an EVENT is GEN, and thus, a statement of fact, DocTimeRel will
always be OVERLAP. 
- Because these EVENTs are on timelines of their own, you should never
TLINK an EVENT marked HYPOTHETICAL or GENERIC to an ACTUAL or UNCertain
EVENT. 
- In situations with an EVENT of discussion or talk, no matter the modality
of what was discussed, the *discussion*/*discussed* itself
will have a modality of ACTUAL, as the discussion really did take
place. 
\end{enumerate

#### Examples of discussion

- We *discussed* that Adjuvant *chemotherapy* following
*surgery* is generally recommended in situations similar to this.
\a. *surgery* BEFORE *chemotherapy*

Here, we have a straightforward discussion of GENERIC EVENTs. So,
the EVENTs are as marked above, with all three having an OVERLAP DocTimeRel.
In addition, we'd TLINK *surgery* BEFORE *chemotherapy*, both
GENERIC EVENTs. *discussed* is ACTUAL, as the discussion actually
occurred.

- I briefly *mentioned* the *risks* of adjuvant *chemotherapy*
with Mr. Peloquin, along with *those* of several other treatment
*options*.

Here, the risks of a generic course of chemotherapy are mentioned.
*mentioned* would be ACTUAL, with a DocTimeRel of OVERLAP. *risks*
and adjuvant *chemotherapy* would be GENERIC with a DocTimeRel
of OVERLAP.

- We also *discussed* the risk of wound *infections*,
urinary tract *infections*, and *pneumonia*.

Again, ACTUAL discussion, with three HYPOTHETICAL EVENTs.

- The *risk* of the *anastomosis* was the primary *risk*
*discussed* including the possibility of an anastomotic *leak*,
need for *intervention*, possibly even *surgery* and a temporary
*stoma*.

Do not let the rearrangement of the sentence fool you--this is just
like the prior examples. *discussed* would be ACTUAL, and all
the other EVENTs would be HYPOTHETICAL. Although there are temporal
relations among the EVENTs here, they are not explicitly stated in
the document, so they should not be marked.

- I am *concerned* about use of adjuvant *chemotherapy*
such as *FOLFOX* in this elderly man.

Although there is no explicit discussion here, the doctor is still
making a statement. Here, you'd have an ACTUAL *concerned*, HYPOTHETICAL
*chemotherapy* and *FOLFOX*, and an SET-MEMBER relation between
*chemotherapy* and *FOLFOX*, both HYPOTHETICAL.


#### Pre- and Post- expressions (preoperative, post-treatment, intraoperatively,
etc.)

\label{prepostexp

The adjectives ``preoperative'' and ``postoperative'' (as well
as related terms like ``post-surgical'', ``post-injury'', ``pre-treatment'',
``post-partum'', ``intraoperatively'', ``post-prandial'') present
a particular difficulty for our schema when used without explicit
mention of their referents, as they simultaneously express two inseparable
temporal meanings: first, they introduce an EVENT (like an operation
or an injury), and second, they tell us that the noun they modify
occurred either before, after, or sometimes during this operation
(in the case of intra-).

Because ``preoperative'' and ``post-treatment'' (and their ilk)
actually denote temporal spans (``everything until the surgery'',
``any time after the treatment''), they are actually a sort of TIMEX3.
So, all of these pre- and post- expressions will be marked as being
TIMEX3 of the type PREPOSTEXP (``Pre- Post- Expression''), which
function much like other narrative container anchors.

First, an easy example:

- Patient underwent a partial *hemicolectomy* in **July 2009**.
**Postoperative** *scarring* *noted* during *exam*. \a.
**July 2009** CONTAINS *hemicolectomy* \b{.} *hemicolectomy*
BEFORE *exam* \b{.} *exam* CONTAINS *noted* \b{.} *hemicolectomy*
BEFORE **Postoperative** \b{.} **Postoperative** CONTAINS *scarring*
\b{.} **Postoperative** BEGINS-ON *surgery*

Here, you can see that there is a large amount of temporal information
expressed here, but most important is the **postoperative** TIMEX3
and the two associated TLINKs. The scarring is TLINKed to postoperative
with CONTAINS because the scarring occurs during the span of time
which ``postoperative'' designates. Then, we mark that postoperative
BEGINS-ON the surgery, because the surgery's end represents the start
of the postoperative period.

This is relatively straightforward, but there is not always an explicit
reference to the surgery in the note:

- Patient is in *recovery*, no **post-operative** *changes*.
\a. **post-operative**$_{prepostexp}$ CONTAINS *changes*$_{\text{NEG}}$
\b{.} **post-operative**$_{prepostexp}$ CONTAINS *recovery*

Here, we have no EVENT for the operation which we can TLINK the *changes*
to. In this situation, **postoperative** would still be a TIMEX3,
and it would CONTAIN the *changes*. Post-operative here stands
in for the span of time following the surgery, allowing us to capture
that the lack of changes occurred following the unmentioned procedure.
Let's look at another example:

- The patient's **preoperative** *health* is *good*, and
**next week**'s *tonsillectomy* should proceed without *difficulty*$_{NEG,HYP}$.
\a. **preoperative** CONTAINS *health* \b{.} **preoperative\
CONTAINS *good* \b{.} **preoperative** ENDS-ON *tonsillectomy*
\b{.} **next week** CONTAINS *tonsillectomy*

The surgery introduced by **preoperative** will presumably occur in
the future (given the tenses in the sentence). The *health* and
*good* EVENTs are occurring at the document time, so they have
a DocTimeRel of OVERLAP, and then finally the TLINK shows us that
the preoperative period CONTAINS the good health. Note that *difficulty*$_{NEG,HYP}$
is not linked to *tonsillectomy*$_{ACTUAL}$, because we cannot
link HYP Events to ACTUAL Events.


#### Annotating the word ``plan'' or ``plans\textquotedbl{}

\textquotedbl{}Plan'' is a temporally difficult word. In some cases,
it is clearly temporally relevant:

- I'd discussed that she'll need to come in for the EGD with biopsies,
followed by a CT scan. We're hoping to implement this plan in the
next few weeks.

In this case, it is clearly an EVENT, as it needs to be implemented
at a specific time and TLINKed with **next few weeks**. But in some
cases, its status as an EVENT is more ambiguous.

- I have explained this plan to both Miss Mullins and the primary
team.

Here, there is no strong TLINK, and the plan itself isn't necessarily
temporally bound.

To avoid this ambiguity and improve annotator agreement, we've decided
that \textbf{in all cases, ``plan'' will be considered an EVENT}.
Do your best to annotate DocTimeRel and all other EVENT properties,
making TLINKs which may be necessary, but no matter the usage, we
should always be marking `plan' (or `plans') as an EVENT. This rule
applies to both verbs and nouns, where relevant.


#### Annotating ``prior'' and ``at the same time\textquotedbl{}

\textquotedbl{}Prior'', ``at the same time'', and other related
temporal indicator words or phrases are often complicated in their
role within the schema, and as such, merit special discussions.


#### Annotating ``Prior\textquotedbl{}

The most common mistake made by new annotators is to consider ``prior''
itself to be a TIMEX3. It is, of course, a word carrying considerable
temporal information, but it is not a TIMEX3. Prior is a marker of
a temporal relationship, like the words ``before'' or ``during'',
rather than an explicit reference to a time or date (like **Yesterday**,
**Last weekend** or **2pm**). As such, the word ``prior'' itself
will never be a TIMEX3, although, as shown below, it will occasionally
show up as part of a longer temporal expression.

The best way to illustrate the varied uses of ``prior'' in the data
is to discuss a series of examples:

- Healthy prior to admission and only co-morbid conditions. \a.
*healthy* BEFORE *admission*

Here (as in many cases), ``prior'' is marking a temporal relationship,
here stating that the *healthy* comes BEFORE *admission*.
This is the case with most usages, where ``prior'' simply indicates
a temporal link (``She should meet with me prior to discharge'',
``The electrolyte panel should be reviewed prior to the consult'').
This link is usually of type BEFORE, but occasionally marks ENDS-ON
(``She had no symptoms prior to her coughing''). Note that in this
example (as with most), the word ``prior'' itself is left unmarked.

- Prior to her *MI*, she experienced no *signs* of cardiovascular
illness. \a. *signs*$_{NEG}$ ENDS-ON *MI*

Example \Last is identical to \LLast, except for a syntactic change
pulling the ``prior to her MI'' to the front of the sentence. Once
again, prior indicates the given TLINK.

- *Omeprazole* should be taken **1 hour** prior to *meals*.
\a. **1 hour** OVERLAP *Omeprazole* \b{.} **1 hour** BEFORE
*meals*

Note that here, ``1 hour prior to meals'' is itself a temporal expression
(which happens to include the term ``prior''), to which Omeprazole
is linked, although ``prior'' is not included in this TIMEX. No
further links are possible in this schema.

- Prior *treatment* with Prilosec was not felt to be *effective*.

Here, all that ``prior'' is giving us is that the treatment with
Prilosec has a DocTimeRel of ``before\textquotedbl{}. No explicit
TLINK is given or indicated. This is usually the case when ``prior''
is being used as a modifier (``Her prior illness'', ``the prior
surgery'', etc).


#### Annotating ``at the same time\textquotedbl{}

Similarly to ``prior'', ``at the same time'' (and derivative expressions)
is not a TIMEX3, but a marker of a temporal relationship. For example:

- We will order the *EGD* as a complex procedure so that Botox
*injection* can be done at the discretion of the endoscopist at
that same time. \a. *EGD* OVERLAP *injection*

Here, ``at that same time'' is indicating that *EGD* OVERLAPs
*injection*, and is itself unmarked. This is the most common usage,
marking OVERLAP or CONTAINS TLINK relations.

- She had a *hysterectomy* with scar ovaries *removed*
and appendix *removed* at the same time. \a. *hysterectomy*
OVERLAP *removed* \a. *hysterectomy* OVERLAP *removed*

In \Last, again, ``at the same time'' is left unmarked.

- I met with the patient at 2pm today, and told her I'd *check*
in at **the same time tomorrow**. \a. **the same time tomorrow\
CONTAINS *check*

\Last shows one of the relatively rare uses of ``at the same time''
as a TIMEX3. Here, **the same time tomorrow** is a TIMEX3, which CONTAINS
*check*.

- There is good evidence that this procedure will improve her
condition, but at the same time, it could easily lead to additional
complications.

This usage is a red herring, as this ``at the same time'' is simply
a turn of phrase used to separate opposing statements, rather than
indicating a worthwhile temporal link.


#### Negation and Causation

There is often an issue with negative counterfactuals, where the causation
is essentially what would happen if the event happened. As the second
event in such links must be HYPOTHETICAL, you only need to link these
if both events are HYPOTHETICAL.

If that is the case, then mark the TLINK as if it actually were happening:

- DA Hurlbert won't *press* felony charges against hit-and-run
driver because it might *affect* his job. \a. *press* BEFORE/CAUSE
*affect*


#### Discerning OVERLAP/CAUSE vs OVERLAP/PRECONDITIONS

If you are pondering this boundary, then the causing event is probably
some sort of state or condition leading to another event. If causation
defines an intent or desire to do something, then assume that this
is a PRECONDITION. Consult section \ref{desiderative} for more on
these.

If having state X means that one has the skills, resources, etc. to
do event Y, then that is PRECONDITION.

If the two events are in an \textquotedbl{}X amounts to doing Y\textquotedbl{},
then you should do it using CAUSE, unless they are coreferential enough
to accept IDENT or BRIDING:

- If you do *take* him back though, you *send* the signal
that you're prepared to accept things continuing as they \a. *take*
OVERLAP/CAUSE *send*

\pagebreak{


##Appendix


###Schema Description

In an effort to clarify the schema at a glance, here's a quick summary
of the Richer Event Description Annotation Schema, using the structure
described below. Default values, where applicable, are in \textbf{\textit{bold
italics}}: \begin{multicols}{2} \begin{itemize*} 

- \textbf{Entity/Relation Type} \begin{itemize*} 

- Property of that entity/relation type \begin{itemize*} 

- Choice 1 for that property 

- Choice 2 for that property 

- ... \end{itemize*} \end{itemize*} \end{itemize*
\begin{itemize
- \textbf{ENTITY} \begin{itemize*} 
- Polarity \begin{itemize*} 
- \textbf{\textit{POS}} 
- NEG \end{itemize*} \end{itemize*} \begin{itemize*} 
- Contextual Modality \begin{itemize*} 
- \textbf{\textit{ACTUAL}} 
- GENERIC \end{itemize*} \end{itemize*
- \textbf{EVENT} \begin{itemize*} 
- DocTimeRel \begin{itemize*} 
- BEFORE 
- OVERLAP 
- AFTER 
- BEFORE/OVERLAP \end{itemize*} 
- Type \begin{itemize*} 
- \textbf{\textit{N/A}} 
- ASPECTUAL 
- EVIDENTIAL \end{itemize*} 
- Representation \begin{itemize*} 
- \textbf{\textit{EXPLICIT}} 
- IMPLICIT \end{itemize*} 
- Polarity \begin{itemize*} 
- \textbf{\textit{POS}} 
- NEG \end{itemize*} 
- Degree \begin{itemize*} 
- \textbf{\textit{N/A}} 
- MOST 
- LITTLE \end{itemize*} 
- Contextual Modality \begin{itemize*} 
- \textbf{\textit{ACTUAL}} 
- HYPOTHETICAL 
- UNC 
- GENERIC \end{itemize*} 
- Contextual Aspect \begin{itemize*} 
- \textbf{\textit{N/A}} 
- INTERMITTENT \end{itemize*} \end{itemize*} 
- \textbf{DOCTIME} 
- \textbf{SECTIONTIME} 
- \textbf{TIMEX3} \begin{itemize*} 
- Class \begin{itemize*} 
- DATE 
- TIME 
- DURATION 
- QUANTIFIER 
- PREPOSTEXP 
- SET \end{itemize*} \end{itemize*
- \textbf{TLINK} \begin{itemize*} 
- Event \begin{itemize*} 
- (This is a slot, designed to be filled with the EVENT being TLINKed)
\end{itemize*} 
- Related to \begin{itemize*} 
- (This is a slot, designed to be filled another EVENT or TIMEX3 to
which the first EVENT is being temporally linked) \end{itemize*} 
- Type \begin{itemize*} 
- BEFORE 
- BEFORE-CAUSE 
- BEFORE-PRECONDITION 
- OVERLAP-CAUSE 
- OVERLAP 
- CONTAINS 
- CONTAINS-SUBEVENT 
- BEGINS-ON 
- ENDS-ON 
- SIMULTANEOUS \end{itemize*} \end{itemize*
- \textbf{ALINK} \begin{itemize*} 
- Event \begin{itemize*} 
- (This is a slot, designed to be filled with the EVENT (of type ``ASPECTUAL'')
being ALINKed) \end{itemize*} 
- Related to \begin{itemize*} 
- (This is a slot, designed to be filled another EVENT to which the
first EVENT is aspectually linked) \end{itemize*} 
- Type \begin{itemize*} 
- CONTINUES 
- INITIATES 
- REINITIATES 
- TERMINATES \end{itemize*} \end{itemize*
- \textbf{COREFERENCE} 

\begin{itemize
- IDENTICAL 
- APPOSITIVE 
- WHOLE/PART 
- SET/MEMBER 
- REPORTING 
- BRIDGING 
\end{itemize
\end{itemize
\end{multicols} \pagebreak{


#### Default Values

Some of the attributes of EVENTs, TLINKs, TIMEX3s and ALINKs have
default values, which will automatically be entered by the annotation
tool. This is a list of those default values:


\subsubsection*{Default Values for EVENT

\begin{center
\begin{tabular}{|l|r|
\hline 
\textbf{Property}  & \textbf{Default Value} \tabularnewline
\hline 
EVENT.type  & (N/A) \tabularnewline
EVENT.representation  & EXPLICIT \tabularnewline
EVENT.DocTimeRel  & Must be specified \tabularnewline
EVENT.polarity  & POS \tabularnewline
EVENT.degree  & (N/A) \tabularnewline
EVENT.contextualaspect  & (N/A) \tabularnewline
EVENT.contextualmodality  & ACTUAL \tabularnewline
\hline 
\end{tabular
\par\end{center


\subsubsection*{Default Values for TIMEX3

All values for TIMEX3 annotations must be specified for each instance.


\subsubsection*{Default Values for TLINK

All values for TLINK annotations must be specified for each instance.


\subsubsection*{Default Values for ALINK

All values for ALINK annotations must be specified for each instance.


###References

\bibliographystyle{amsplain
\bibliography{bibtex
 \pagebreak{


###Document Revision History
\begin{itemize
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
discussions and quantifying phrases. Elimination of ``risk of X\textquotedbl{}-type
guidelines. General revision. - Mariah 
- 7/5/14 -- Accepted all prior tweaks, and began v.1.5, a clarification
for completing the pilot. 
- 7/6/14 -- Implemented Mariah's suggestion for emotive vs. assertive
emphatics. 
- 7/27/14 -- Added `Avoid millisecond reasoning', `hypotheticals, negation
and the past', and a made a few other repairs. - Will\end{itemize

\end{document}
