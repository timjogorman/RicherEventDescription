#### Ground Rules for annotating HYP/GEN events and discussion events

As discussed previously, these EVENTs, by virtue of their modality,
aren't really on the same timeline as other EVENTs dealing with the
patient's actual care. Because of this, it can be quite tricky to
link them to the overall timeline. As such, we have a few rules, all
previously discussed, which you will find particularly useful:

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


#### Deontic Modality is an edge case.


We want to treat actual events of needing and lacking as EVENTs, while ignoring instances like "need to" or "got to" which merely add a feature like "necessity" to other predications.  If you can rephrase something with "must" or "it is necessary ...", is it NOT an event:

- We may ~~need~~ to **hold** her **diuretic** before surgery.
(can be rephrased with "It may be necessary for us to hold her diuretic...")

In contrast, if the term means something like "lacks and needs more of", then you should make it an event:
- Blood **labs** revealed an urgent **[<sub>event</sub> need]** for more iron.
*(note how hard it would be to rephrase this using "it was necessary ...")*


Another such test can be used for verbs of planning, which are also
of variable semantic weight. If `plan to' can be replaced with `will
probably' or `hopes to' without major change in meaning, then it is
too semantically light, and should not be tagged. In contrast, if
it referring to the act of formulating plans for the future, then
it is eventive.

- City officials have been **planning** for the **race** for
several months.

- No oncologic **follow** - up is **planned** at this time.

- Patient is planning to **return** to his local oncologist
who he has a good relationship with. (see rough equivalence with "Patient
will probably return to his ...")

- Local fire departments plan to **enact** fire **bans** if
the hot weather continues. (Again, roughly equivalent to "fire departments
will likely enact")


