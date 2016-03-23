## Using Anafora for AMR document  annotation
##### Step 1: Load the document

1. I've sent out "username" and "password"  emails to a bunch of you (if anyone reading this wants one and didn't get it, email me).  
* When you have that, go to verbs.colorado.edu/anafora-event and log in. 
 * From "Schema" select "DAMR"
 * From "Mode" select "Coreference"
 * From "Select Project" select "DocumentAMR"
 * From "Select Corpus" select "Training"
 * Select "attack-example", which should be "in-progress" for everyone.
 * Click "open" in the bottom right-hand corner

##### Sidebar on the color scheme
* The concepts are in categories, but those categories are NOT relevant to final output; they are for easy of understanding.
* Green means that something is likely to be an entity (light green = less likely to be relevant)
* Orange means that something is likely to be an event (light orange = less likely to be relevant)
* Brown means it has a good :wiki link
* light blue means that something is an implicit argument not in the current AMR.
 
##### Step 2: Make an Entity coreference chain

* In the menu, go to Schema->EntityChains, and select "UniqueEntity". 
 * Press "mentions" in the right-hand panel (**edit:** specifically, the empty box to the right of the box that says "mentions"), which will grey out that box.  You are now in a mode where any concept you click on gets added to the identity chain. as in:
![This example](https://www.dropbox.com/s/6n9kk0kfwa6x5s1/amrexampleMS.png?dl=1)
 * Click on "m2 / man" in the first AMR
 * Then click on "p / person" in the second sentence (this is a multi-sentence AMR). 
* In the menu, go to Schema->EntityChains, and select "AggregateEntity", and again select "mentions".  
 * Click on "y / yob" in the first AMR. 
* These have hotkeys: "u" gets you a unique entity chain, "s" gets you an Aggregate entity chain, and "1" selects that box to the right of "mentions". 

##### Step 3: Make an Event coreference chain
* In the menu, go to Schema->EventChains, and select "Event".  Again, press "1" to get into the mentions mode.
 * Select the "a / attack" in the first AMR. 
 * All of these annotations default to the modality of "actual", but you can change the modality of an event or entity by clicking on the box to the right of "modality", which currently says "actual", and picking from menu it provides.
 * *The options of "NegatedEvent", "HypotheticalEvent", etc are just shortcuts for specific modalities; you can otherwise treat them like a normal "event" chain*

##### Step 4: Link to a previously mentioned entity chain.
* Go to AMR sentence 2 and find ```(p / person :wiki - :name (n / name :op1 "Mr." :op2 "Goodman"))```.  We've already made an entity chain for this guy, and we want to add this mention to it. 
 * Press "ESC" to leave the coreference mode of whatever you are currently annotating.
 * Click on a previous mention of Mr Goodman (like ```(m2 / man)``` in the first sentence).
 * It will show every relation that mention participates in, including the UniqueEntity chain.  Click on it. 
 * Now just select the "mentions" box again and add our new mention to the list. 
* (Alternatively, one can just scroll through the list of identity chains in the bottom window and find what you're looking for there)

##### Step 5: Mark a bridging / partial-coreference link
* There are a number of relations that are similar to identity, and so you may want them available now.  In AMR language, these correspond to have-part-91, include-91, and the :consist relation, as well as "bridging" (for debatable, speculative or metaphorical coreference, roughly ```have-mod-91 :arg1-of possible-01```)
* In the first sentence, ```l / lung``` and ```r2 / rib``` are not linked to the man.  In the menu, go to Schema -> Partial -> Whole part. 
 * click on "whole" and select a mention of the victim, such as ```p / person```.  
 * click on "part" and add any number of part mentions that are relevant. 
* We don't need to mark these if the AMRs somewhere capture the relevant link. 


