
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
his head exploded into fragments, and "that" was briefly airborne).
Similarly, although they're likely to be singletons (barring exceptionally
cute wordplay), we need to grab entities like the kicked bucket, the
grass inhabited by the snake, and the rocker she was recently separated
from.

Even though this may seem unsatisfying, a surprising amount of this
information can be recovered by verb sense disambiguation ("Kick"
has a `the bucket' sense which is specified as meaning "death"),
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
into fragments, and "that" was briefly airborne).

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

In these examples, "bucket", "rocker", "grass" and "mustard"
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

Do not, for example, attempt to interpret "bush" as IDENTICAL
to the sale, attempt to corefer "shotgun" to the physical passenger
seat, equate "cheating" with her medicine, or claim that "thunder"
\textit{is} the announcement. To make any of these links would require
us to ignore some part of the larger meaning of the word or idiom
(e.g. there's more to "thunder" than the act of announcing), and
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

In the first two idioms, "head" does have a concrete referent
(the speaker's physical head), although it is not literally exploding
or being overflown. Similarly, *practice* clearly refers to the
training, and *dough* is just another term for `money', allowing
a WHOLE/PART relationship with \$50k.

Even though this may seem unsatisfying, a surprising amount of this
information can be recovered by verb sense disambiguation ("Kick"
has a `the bucket' sense which is specified as meaning "death"),
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

#### Annotating the word "plan" or "plans"

\textquotedbl{}Plan" is a temporally difficult word. In some cases,
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
that **in all cases, "plan" will be considered an EVENT}.
Do your best to annotate DocTimeRel and all other EVENT properties,
making TLINKs which may be necessary, but no matter the usage, we
should always be marking `plan' (or `plans') as an EVENT. This rule
applies to both verbs and nouns, where relevant.


#### Annotating "prior" and "at the same time\textquotedbl{}

\textquotedbl{}Prior", "at the same time", and other related
temporal indicator words or phrases are often complicated in their
role within the schema, and as such, merit special discussions.


#### Annotating "Prior\textquotedbl{}

The most common mistake made by new annotators is to consider "prior"
itself to be a TIMEX3. It is, of course, a word carrying considerable
temporal information, but it is not a TIMEX3. Prior is a marker of
a temporal relationship, like the words "before" or "during",
rather than an explicit reference to a time or date (like **Yesterday**,
**Last weekend** or **2pm**). As such, the word "prior" itself
will never be a TIMEX3, although, as shown below, it will occasionally
show up as part of a longer temporal expression.

The best way to illustrate the varied uses of "prior" in the data
is to discuss a series of examples:

- Healthy prior to admission and only co-morbid conditions. \a.
*healthy* BEFORE *admission*

Here (as in many cases), "prior" is marking a temporal relationship,
here stating that the *healthy* comes BEFORE *admission*.
This is the case with most usages, where "prior" simply indicates
a temporal link ("She should meet with me prior to discharge",
"The electrolyte panel should be reviewed prior to the consult").
This link is usually of type BEFORE, but occasionally marks ENDS-ON
("She had no symptoms prior to her coughing"). Note that in this
example (as with most), the word "prior" itself is left unmarked.

- Prior to her *MI*, she experienced no *signs* of cardiovascular
illness. \a. *signs*$_{NEG}$ ENDS-ON *MI*

Example \Last is identical to \LLast, except for a syntactic change
pulling the "prior to her MI" to the front of the sentence. Once
again, prior indicates the given TLINK.

- *Omeprazole* should be taken **1 hour** prior to *meals*.
\a. **1 hour** OVERLAP *Omeprazole* \b{.} **1 hour** BEFORE
*meals*

Note that here, "1 hour prior to meals" is itself a temporal expression
(which happens to include the term "prior"), to which Omeprazole
is linked, although "prior" is not included in this TIMEX. No
further links are possible in this schema.

- Prior *treatment* with Prilosec was not felt to be *effective*.

Here, all that "prior" is giving us is that the treatment with
Prilosec has a DocTimeRel of "before\textquotedbl{}. No explicit
TLINK is given or indicated. This is usually the case when "prior"
is being used as a modifier ("Her prior illness", "the prior
surgery", etc).


#### Annotating "at the same time\textquotedbl{}

Similarly to "prior", "at the same time" (and derivative expressions)
is not a TIMEX3, but a marker of a temporal relationship. For example:

- We will order the *EGD* as a complex procedure so that Botox
*injection* can be done at the discretion of the endoscopist at
that same time. \a. *EGD* OVERLAP *injection*

Here, "at that same time" is indicating that *EGD* OVERLAPs
*injection*, and is itself unmarked. This is the most common usage,
marking OVERLAP or CONTAINS TLINK relations.

- She had a *hysterectomy* with scar ovaries *removed*
and appendix *removed* at the same time. \a. *hysterectomy*
OVERLAP *removed* \a. *hysterectomy* OVERLAP *removed*

In \Last, again, "at the same time" is left unmarked.

- I met with the patient at 2pm today, and told her I'd *check*
in at **the same time tomorrow**. \a. **the same time tomorrow\
CONTAINS *check*

\Last shows one of the relatively rare uses of "at the same time"
as a TIMEX3. Here, **the same time tomorrow** is a TIMEX3, which CONTAINS
*check*.

- There is good evidence that this procedure will improve her
condition, but at the same time, it could easily lead to additional
complications.

This usage is a red herring, as this "at the same time" is simply
a turn of phrase used to separate opposing statements, rather than
indicating a worthwhile temporal link.


#### Discussions, Generalizations, and other EVENTs which aren't on the
timeline


One of the biggest sources of difficulty for annotators is the presence
of EVENTs which do not really belong in the timeline per se, but are
present in the document. Let's use the below examples to discuss.

- We're going ahead with adjuvant *chemotherapy*
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
If the note reads "We discussed her upcoming surgery as well as
the possibility for future recurrence", we certainly do not want
"recurrence" showing up on a factual timeline, but we certainly
would want "surgery" to show up.

In order to properly train our systems to find EVENTs, all EVENTs
must be marked; however, we must make sure that we can reconstruct
the reality (and the applicability to the timeline) of all EVENTs.
Our primary means for handling this is the Contextual Modality property
of EVENTs. As discussed in Section \ref{modality}, we use HYPOTHETICAL
and GENERIC to mark EVENTs which, although certainly events, do not
belong on the timeline. As you may have already guessed, in \LLast,
"adjuvant chemotherapy" is a HYPOTHETICAL EVENT, and in \Last,
it is a GENERIC EVENT.

Using these two modalities, you should be able to annotate all of
the cases where EVENTs are discussed which do not belong on the timeline
(or belong on a hypothetical fork of the timeline).



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


#### Some Exceptions and Specific Patterns


##### Measurement Phrases

Another exception to a strict headedness approach is that "few"
is not to be annotated as the head of sentences such as 
\begin{examples
- {**} **\textsubscript{entity}I ** **\textsubscript{event} ate
** a **\textsubscript{entity}few ** of the plums in the **\textsubscript{entity}icebox**
\end{examples
Instead, when the head is a quantifier-type term such as "few"
or "some", use the thing counted, as in:
\begin{examples
- **\textsubscript{entity}I ** **\textsubscript{event} ate **
a few of the **\textsubscript{entity}plums** in the **\textsubscript{entity}icebox**
\end{examples
This is hopefully clear in such cases, but will be more complicated
when dealing with words like "groups of ..", "collections of...",
and increasingly informative units. This will end of being a question
of whether there is one entity -- in which case the quantified term
will be head -- or two entities, a SET and a MEMBER, as discussed
in section \ref{sub:SET-MEMBER}. If one could imagine replacing the
phrase with a mere count of the items in question, merely mark the
latter:
\begin{example
Within eyesight, a *gaggle of **\textsubscript{entity}geese
**} lounged in the afternoon **\textsubscript{entity}sun**

\emph{= roughly 20 geese lounged in the afternoon sun.
\end{example
In contrast, if the unit seems to be clearly a unit that is more than
an aggregate collection of its parts, feel free to mark it as a delineated
unit with SET/MEMBER:
\begin{examples
- The **\textsubscript{entity}position ** was defended by a ***\textsubscript{entity
battalion** of the **\textsubscript{entity}~3rd brigade**}.
\end{examples

\paragraph{Headedness with foreign phrases

For foreign phrases -- such as latin terms -- you should feel free
to use whatever part of the term seems to be acting as head in context.
For latin phrases, these will often be left-headed phrases where one
may take the first word in the phrase, as in:

- She has **diabetes** mellitus.

- **Polymyalgia** Rheumatica is a concern here.

- We suspect **myasthenia** gravis is the cause of her continued
weakening.

Do not, however, extend this to terms that have aquired casual use
in English, even if your knowledge of the word's origin informs you
of what the "real" head:

- He is the attorney **\textsubscript{entity}~general** of
Florida. 


\paragraph{Multi-word Proper Nouns

As a reminder, when the head noun is a proper noun with more than
one word, take the entire appropriate span, not just one word. This
policy applies to first-middle-last name mentions, as well as consistently-used
multi-word titles or names, so long as they are all specific to the
mentioned individual:

- They are investigating the policies of **North Korea**.

- Sochi is nearly ready to host the **Olympic Games**.

- **Barack Obama** condemned the Russian aggression.

- **William Francis Styler IV** helped write these guidelines,
and has an exceedingly long full name.

- **Dr. Franklin G. Cummings, Esq.** was on safari during the
attack.

- **His Holiness the Dalai Lama** visited Nepal this week.

- **The Artist Formerly Known as Prince** played a sold-out
show.

- **Her Royal Majesty Queen Elizabeth II** was in attendance.

... but keep in mind that optional premodifying noun-phrases are not
included in the mention span, and often result in entity mentions
of their own, so:

- They visited the much-esteemed **administrator** of the facility.

- Smith introduced the **Leader** of the Free **World** and
**President** of the **United States**, **Barack Obama**.


\paragraph{Morphological vagueness involving hyphenated and possessive words

This section has insisted upon annotating "a single word" as if
that is a clear-cut concept. We will generally make this clear cut
in the simplest manner possible, in that a word is surrounded by spaces. 

Hyphenated words will usually be an exception to this -- if one encounters
"CT-scan", for example, one may treat it as "CT scan" and
take the appropriate head "scan". There are, however, many hyphenated
words with a bound form -- such as "co-exist" -- should not be
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


Furthermore, when a "-'s" possessive marker is present, do not
treat that term as part of the word. Unfortunately, when there is
no clear delineating apostrophe present, as in "his", "its",
or even the mere absence of an appostrophe, graph the entire word. 

- We discussed the CT results with **Miss Mullins**. The **patient**'s
scan reveals **liver** **metastasis**.

- State **legislators** report that **their** constituents
are satisfied with the compromise.

\pagebreak{


