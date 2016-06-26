:author: Michael D. Pacer
:email: mpacer@berkeley.edu
:institution: University of California, Berkeley

:author: Jordan W. Suchow
:email: suchow@berkeley.edu
:institution: University of California, Berkeley

:video: http://www.youtube.com/
:bibliography: mybib

------------------------------------------------
Proselint
------------------------------------------------

.. class:: abstract

   Writing is notoriously hard, even for the best writers, and it's not for lack of good advice — a tremendous amount of knowledge about the craft is strewn across usage guides, dictionaries, technical manuals, essays, pamphlets, websites, and the hearts and minds of great authors and editors. But this knowledge is trapped, waiting to be extracted and transformed.

   We built Proselint, a Python-based linter for prose. Proselint identifies violations of expert style and usage guidelines. Proselint is open-source software released under the BSD license and is compatible with Python 2 and 3. It runs as a command-line utility or editor plugin (e.g., Sublime Text, Atom, Vim, Emacs) and outputs advice in standard formats (e.g., JSON). Proselint includes modules that address redundancy, jargon, illogic, clichés, unidiomatic vocabulary, sexism, misspelling, inconsistency, misuse of symbols, malapropisms, oxymorons, security gaffes, hedging, apologizing, and pretension.

   Proselint can be seen as both a language tool for scientists and a tool for language science. On the one hand, it includes modules that promote clear and consistent prose in science writing. On the other, it measures language usage and explores the factors relevant to creating a useful linter.

.. class:: keywords

   linters, writing tools, copyediting

The problem
===========

Writing is notoriously hard, even for the best writers, and it's not for lack of good advice — a tremendous amount of knowledge about the craft is strewn across usage guides, dictionaries, technical manuals, essays, pamphlets, websites, and the hearts and minds of great authors and editors. Consider for example *Garner's Modern English Usage*, an authoritative usage guide with 11,000 entries covering a broad range of topics that, when followed, help writers produce clean and idiomatic prose. Or consider the *Federal Plain Language Guidelines*, a 2011 guide created by employees of the U.S. federal government to promote writing that is clear, consise, and well-organized. Professional conferences, such as the annual meeting of the American Copy Editors Society, are dedicated to sharing knowledge about editing prose. And within the academy, organizations such as the American Psychological Association publish manuals whose guidance on style has been adopted as a standard. Advice on writing abounds.

Advice on writing touches upon everything from superficial conventions to the deepest reflections of our society and its attitudes. Take for example advice concerning the preferred forms of words such as "" (vs. ""), which may help to prune needless variants in spelling, but are unlikely to effect the reader's understanding of the text and its author. Compare this to advice concerning needlessly gendered language ("woman scientist", "policeman"), which by being commonplace in language may perpetuate social inequality.

Having amassed a pile of useful advice is not enough to make writing better. Advice, though it may be principled, thoughtful, and worth following, is hard to apply in new settings once it has been learned. Thus, even if one could absorb all the knowledge contained in these sources, there would still be the problem of recalling and systematically it. And even when its applicability is recognized, developing a new habit is still slow, costly, and difficult. Errors will appear and mistakes will be made.

.. linter advantage: Instant feedback? e.g.,

Today, an author wishing to improve a piece of writing by applying the collective wisdom of experts must use indirect means. The most common approach, used extensively in publishing, is a division of labor whereby dedicated staff with deep knowledge of best practices in writing copyedit a piece to their satisfaction. This is the approach used, for example, by *The New Yorker*, whose editing team includes fact checkers, editors, grammarians, and more. A second approach, used extensively in desktop publishing, is a reliance on software-based tools such as spellcheckers and grammar checkers that mark unrecognized words and purported violations of grammatical rules.

Neither of these approaches — expert staff and extant software-based tools — fully solve the problem. Few people have the resources to outsource editing of everything they write to expert staff, and getting the advice inevitably takes time because copyeditors do not look over one's shoulder and whisper advice during the act of writing —  by the time you receive their notes, you have already missed out on the best opportunity to strengthen your craft. And software-based tools, though they are inexpensive and fast, are typically incomplete, imprecise, or inaccessible.

Our collective knowledge about best practices in writing is trapped, waiting to be extracted and transformed into a new medium that makes the knowledge immediately accessible to all authors.

The solution
============

To solve this, we built Proselint, a Python-based linter for prose. A linter is a computer program that, like a spell checker, scans through a document and analyzes it and identified where it violates. Our goal with Proselint is to aggregate knowledge about best practices in writing and to make that knowledge immediately accessible to all authors in the form of a linter for prose. Proselint thus identifies violations of expert style and usage guidelines.

Proselint is open-source software released under the BSD license and works with Python 2 and 3. It runs efficiently as a command-line utility or editor plugin for SublimeText, vim, &c. It outputs advice in standard formats (e.g., JSON), integrating with Sublime Text, Atom, Vim, Emacs, and other editors and services. Though in its infancy – perhaps 2% of what it could be – Proselint already includes modules on a variety of usage problems: redundancy, jargon, illogic, clichés, sexism, misspelling, inconsistency, misuse of symbols, malapropisms, oxymorons, security gaffes, hedging, apologizing, pretension, and more. 

Two views on proselint
======================

Proselint can be seen as both a language tool for scientists and a tool for language science. On the one hand, it can be used to improve writing, and it includes modules that promote clear and consistent prose in science writing. On the other, it can measure language usage and help to explore the factors relevant to creating a useful linter.


As a language tool for scientists
----------------------------------

Science and writing are fast friends; science as we know it would not be possible without the written word. But cutting-edge scientific research is, by necessity,  difficult to understand by all but those most acquainted with it. Even expressing those ideas challenges the greatest of minds, leaving little time for eradicating opacity from prose. Nonetheless, opacity is the enemy of the proliferation of any idea.

Proselint can aid specifically improve scientists' writings across a number of dimensions:

* consistent terminology
* cleaner prose
* less redundancy
* typographic niceties
* 

Even greater improvement can be found along each of these dimensions (especially consistent terminology) if the scientist in question were to build custom extensions to proselint for their field/subfield/topic/&c.. However, even out-of-the-box proselint can be useful, as demonstrated by the following graph of the errors identified by proselint in this year's scipy submissions from initial to final submission dates [insert graph of the number of errors identified by proselint over time across all of the papers submitted to scipy 2016].

As a tool for language science
------------------------------

In the course of developing the tool, we have identified several features implicit to the problem of error-detection and correction in general, as well as language linting specifically.

Additionally, the normative content inherent in proselint right now is unnecessary. We could use this merely to detect whether people use various words. By doing that proselint  acts as a stylometric feature extractor unlike any other. This opens the door to a variety of possibilities for future applications and generalisations of this kind of a platform.

E.g.,

* Stylometrics.
* Author identification.
* Encoding messages (in the case of multiple acceptable options)
* 


Our general approach
====================

Various ways to divide up the kinds of problems

#.  Divide up problem types into levels of difficulty. (how hard is it to identify that a rule should be fired)

    #. Replacement rules
    #. Regex
    #. Basic syntax processing
    #. NLP, state-of-the-art
    #. NLP, beyond state-of-the-art
    #. AI-complete

#.  Divide up by content (What sorts of rules say similar things to this one?)

    #. This is the basis for our module structure.

#. Divide up by response type (recommendation vs. prohibition)(what should you do when this rule fires)

Desiderata for a linter
-----------------------

Desiderata are a set of criteria that are looked 

Ideal linters need to 

*   scale to many rules
*   respond needs to be in real time

    * This limits how much processing can occur per rule.

*   responses should be relatively monotonic (i.e., we should minimise the number of lints that are due to sentences that have not yet been completed)
*   it needs to be able to be installed easily by the end-user
*   it should be modifiable fairly easily (i.e., if a user does not like a particular rule set it should be able to be turned off)
*   it needs to explain why it raising the flags it raises


Large scale problems require scalable resources
-----------------------------------------------

Open source license allows the community of users to become a community of builders. 
Many of the rules' implementations are particularly well-suited to small-scale coding projects or assignments.






.. the principles we've identified
.. -------------------------------

.. Low false positive rates

.. how our tool address or uses each of those principles
.. -----------------------------------------------------

Installing proselint


Using proselint
===============

Command-line utility
--------------------

At its core, proselint is a command-line utility.

.. code-block:: bash

   proselint text.md

Running this command prints a list of suggestions to stdout, one per line. Each suggestion will have the form:

.. code-block:: bash

   text.md:<line>:<column>: <check_name> <message>

For example,

.. code-block:: bash

  text.md:0:10: wallace.uncomparables Comparison of an 
  uncomparable: 'unique' can not be compared.

The command line utility can also print the list of suggestions in JSON using the <tt>&#45;&#45;json</tt> flag. In this case, the output is considerably richer and matches the output of the <a href="/api">web API</a>.

.. code-block:: javascript

  {
      // Type of check that output this suggestion.
      "check": "wallace.uncomparables",

      // Message to describe the suggestion.
      "message": "Comparison of an uncomparable: 'unique' can not be compared.",

      // The person or organization giving the suggestion.
      "source": "David Foster Wallace"

      // URL pointing to the source material.
      "source_url": "http://www.telegraph.co.uk/a/9715551"

      // Line where the error starts.
      "line": 0,

      // Column where the error starts.
      "column": 10,

      // Index in the text where the error starts.
      "start": 10,

      // Index in the text where the error ends.
      "end": 21,

      // start - end
      "extent": 11,

      // How important is this? Can be "suggestion", "warning", or "error".
      "severity": "warning",

      // Possible replacements.
      "replacements": [
          {
              "value": "unique"
          }
      ]
  }

Text editor plugins
-------------------

Web-editor
----------




Advice: sources and examples
============================

Proselint is built around advice[#]_ derived from works by Bryan Garner, David Foster Wallace, Chuck Palahniuk, Steve Pinker, Mary Norris, Mark Twain, Elmore Leonard, George Orwell, Matthew Butterick, William Strunk, E.B. White, Philip Corbett, Ernest Gowers, and the editorial staff of the world’s finest literary magazines and newspapers, among others. Our goal is to aggregate knowledge about best practices in writing and to make that knowledge immediately accessible to all authors in the form of a linter for prose.

.. [#] Proselint has not been officially endorsed by any of these individuals. We have merely taken their words and implemented them in code. 


examples of some rules
----------------------

Issues are on github repo. 

Any new rules need to be accompanied by an expert source meriting the inclusion of the rule. 

Final decision of whether to include it in the default set of rules is up to us.

We have not included rule modules that are by default left off but can be turned on. 
Though we are not opposed to this in principle, it is difficult to see why we should do so. 
If someone wants to include rules that are not properly attributed, they are welcome to add the module to their own linter. 
We want to make that process simple. 
If someone wants to include rules that are properly attributed it is unclear why we would ever want to turn them off by default.
Furthermore, doing so would weaken our emphasis on encouraging contributions while leaving open the door for extensive customisation to adapt to your personal "style".


Internal structure
------------------

Rule modules
^^^^^^^^^^^^

Proselint rules are organized into modules that reflect the structure on language advice found in usage guides. For example, Proselint includes a module `terms` that encourages idiomatic usage of vocabulary. It has as submodules specific kinds of terms that can be found as entries in usage guides. For example, one such submodule, `terms.venery`,pertains to *venery terms*, which arose from hunting tradition and are used to describe groups of particular animals --- e.g., a "pride" of lions, or a "murmuration" of starlings. Another such submodule, `terms.denizen_labels`, pertains to *demonyms*, which are used to describe people from a particular place --- e.g., *New Yorkers* (New York), *Mancunians* (Manchester), or *Novocastrians* (Newcastle).

Organizing rules into modules is useful both because it allows for a logical separation of similar rules, which often require similar computational machinery to implement, and also because it allows users to include and exclude rules at a higher level of abstraction than an individual word or phrase. One open challenge is how to allow customization at a level more finely grained than a submodule.

Rule templates
^^^^^^^^^^^^^^

Memoization
^^^^^^^^^^^

One of our goals is for Proselint to be efficient, able to run over a document in realtime as an author writes it. To achieve this goal, it is helpful to avoid redundant computation by storing the results of expensive function calls from one run of the linter to the next, a technique called memoization. For example, consider that many of Proselint's checks can operate at the level of a paragraph, and most paragraphs do not change when a sizable document is being edited --- at the extreme, where the linter is run after each keystroke, this is true by definition. By running checks over paragraphs, and recomputing only when the paragraph has changed, otherwise returning the memoized result, it is possible to reduce the total amount of computation and thus improve the linter's running time.

Future
------

Prosewash
^^^^^^^^^
Next steps: more intense processing with riskier rules
False positive checking with crowd sourcing
Feedsback to improve proselint

One reason to have rules off by default but included might be because of their effect on the false positive rate.


Concerns around normativity in prose styling
--------------------------------------------

One of the most common critiques of proselint is a concern that introducing any kind of linter-like process to the act of writing prose would in some way diminish the ability for authors to express themselves creatively.
These arguments suggest that authors will find themselves limited in the set of things that are consistent with the linter's rules, and as a result that this will have a homogenising effect on prose.
There are many nuances around how exactly this is stated, but that general gist covers the core of the critique. 

To this critique there are several possible responses.
The first few apply in general, the latter apply in the case of scientific and technical writing.

Proselint is a massive undertaking, one that will require the ethos of an open source community to complete. Garner’s book alone has 11,000 entries. Half are easy, assignable as a homework problem (e.g., that “very unique” compares an uncomparable adjective, or that people from Michigan prefer to be called “Michiganders”, not “Michiganians”). Thirty percent are moderately challenging, requiring custom tooling. Fifteen percent are hard — projects that require advances in AI and NLP. Everything else, around five percent (the best five percent), is AI-complete.

We will discuss where Proselint is and where it is heading. We will show its installation and application, demonstrating its use on the repository of papers submitted to SciPy2016.

Proselint is fertile ground for growing an open-source community. It has trivial subproblems and lofty goals, an immediate impact and a long future.

Existing modules
----------------

Here is a list of what `proselint` checks.

.. table:: What Proselint checks. :label:`checks`

   +---------------------------------+---------------------------------------------+
   | ID                              | Description                                 |
   +=================================+=============================================+
   |``airlinese.misc``               | Avoiding jargon of the airline industry     |
   +---------------------------------+---------------------------------------------+
   |``annotations.misc``             | Catching annotations left in the text       |
   +---------------------------------+---------------------------------------------+
   |``archaism.misc``                | Avoiding archaic forms                      |
   +---------------------------------+---------------------------------------------+
   |``cliches.hell``                 | Avoiding a common cliché                    |
   +---------------------------------+---------------------------------------------+
   |``cliches.misc``                 | Avoiding clichés                            |
   +---------------------------------+---------------------------------------------+
   |``consistency.spacing``          | Consistent sentence spacing                 |
   +---------------------------------+---------------------------------------------+
   |``consistency.spelling``         | Consistent spelling                         |
   +---------------------------------+---------------------------------------------+
   |``corporate_speak.misc``         | Avoiding corporate buzzwords`               |
   +---------------------------------+---------------------------------------------+
   |``cursing.filth``                | Words to avoid                              |
   +---------------------------------+---------------------------------------------+
   |``cursing.nfl``                  | Avoiding words banned by the NFL            |
   +---------------------------------+---------------------------------------------+
   |``dates_times.am_pm``            | Using the right form for the time of day    |
   +---------------------------------+---------------------------------------------+
   |``dates_times.dates``            | Stylish formatting of dates                 |
   +---------------------------------+---------------------------------------------+
   |``hedging.misc``                 | Not hedging                                 |
   +---------------------------------+---------------------------------------------+
   |``hyperbole.misc``               | Not being hyperbolic                        |
   +---------------------------------+---------------------------------------------+
   |``jargon.misc``                  | Avoiding miscellaneous jargon               |
   +---------------------------------+---------------------------------------------+
   |``lexical_illusions.misc``       | Avoiding lexical illusions                  |
   +---------------------------------+---------------------------------------------+
   |``links.broken``                 | Linking only to existing sites              |
   +---------------------------------+---------------------------------------------+
   |``malapropisms.misc``            | Avoiding common malapropisms                |
   +---------------------------------+---------------------------------------------+
   |``misc.apologizing``             | Being confident                             |
   +---------------------------------+---------------------------------------------+
   |``misc.back_formations``         | Avoiding needless backformations            |
   +---------------------------------+---------------------------------------------+
   |``misc.bureaucratese``           | Avoiding bureaucratese                      |
   +---------------------------------+---------------------------------------------+
   |``misc.but``                     | Avoid starting a paragraph with "But..."    |
   +---------------------------------+---------------------------------------------+
   |``misc.capitalization``          | Capitalizing correctly                      |
   +---------------------------------+---------------------------------------------+
   |``misc.chatspeak``               | Avoiding lolling and other chatspeak        |
   +---------------------------------+---------------------------------------------+
   |``misc.commercialese``           | Avoiding jargon of the commercial world     |
   +---------------------------------+---------------------------------------------+
   |``misc.currency``                | Avoiding redundant currency symbols         |
   +---------------------------------+---------------------------------------------+
   |``misc.debased``                 | Avoiding debased language                   |
   +---------------------------------+---------------------------------------------+
   |``misc.false_plurals``           | Avoiding false plurals                      |
   +---------------------------------+---------------------------------------------+
   |``misc.illogic``                 | Avoiding illogical forms                    |
   +---------------------------------+---------------------------------------------+
   |``misc.inferior_superior``       | Superior to, not than                       |
   +---------------------------------+---------------------------------------------+
   |``misc.latin``                   | Avoiding overuse of Latin phrases           |
   +---------------------------------+---------------------------------------------+
   |``misc.many_a``                  | Many a singular                             |
   +---------------------------------+---------------------------------------------+
   |``misc.metaconcepts``            | Avoiding overuse of metaconcepts            |
   +---------------------------------+---------------------------------------------+
   |``misc.narcisissm``              | Talking about the subject, not its study    |
   +---------------------------------+---------------------------------------------+
   |``misc.phrasal_adjectives``      | Hyphenating phrasal adjectives              |
   +---------------------------------+---------------------------------------------+
   |``misc.preferred_forms``         | Miscellaneous preferred forms               |
   +---------------------------------+---------------------------------------------+
   |``misc.pretension``              | Avoiding being pretentious                  |
   +---------------------------------+---------------------------------------------+
   |``misc.professions``             | Calling jobs by the right name              |
   +---------------------------------+---------------------------------------------+
   |``misc.punctuation``             | Using punctuation assiduously               |
   +---------------------------------+---------------------------------------------+
   |``misc.scare_quotes``            | Using scare quotes only when needed         |
   +---------------------------------+---------------------------------------------+
   |``misc.suddenly``                | Avoiding the word suddenly                  |
   +---------------------------------+---------------------------------------------+
   |``misc.tense_present``           | Advice from Tense Present                   |
   +---------------------------------+---------------------------------------------+
   |``misc.waxed``                   | Waxing poetic                               |
   +---------------------------------+---------------------------------------------+
   |``misc.whence``                  | Using "whence"                              |
   +---------------------------------+---------------------------------------------+

.. table:: What Proselint checks(cont.). :label:`checkscont`

   +---------------------------------+---------------------------------------------+
   | ID                              | Description                                 |
   +=================================+=============================================+
   |``mixed_metaphors.misc``         | Not mixing metaphors                        |
   +---------------------------------+---------------------------------------------+
   |``mondegreens.misc``             | Avoiding mondegreen                         |
   +---------------------------------+---------------------------------------------+
   |``needless_variants.misc``       | Using the preferred form                    |
   +---------------------------------+---------------------------------------------+
   |``nonwords.misc``                | Avoid using nonwords                        |
   +---------------------------------+---------------------------------------------+
   |``oxymorons.misc``               | Avoiding oxymorons                          |
   +---------------------------------+---------------------------------------------+
   |``psychology.misc``              | Avoiding misused psychological terms        |
   +---------------------------------+---------------------------------------------+
   |``redundancy.misc``              | Avoid redundancy & saying things twice      |
   +---------------------------------+---------------------------------------------+
   |``redundancy.ras_syndrome``      | Avoiding RAS syndrome                       |
   +---------------------------------+---------------------------------------------+
   |``skunked_terms.misc``           | Avoid using skunked terms                   |
   +---------------------------------+---------------------------------------------+
   |``spelling.able_atable``         | -able vs. -atable                           |
   +---------------------------------+---------------------------------------------+
   |``spelling.able_ible``           | -able vs. -ible                             |
   +---------------------------------+---------------------------------------------+
   |``spelling.athletes``            | Spelling of athlete names                   |
   +---------------------------------+---------------------------------------------+
   |``spelling.em_im_en_in``         | -em vs. -im and -en vs. -in                 |
   +---------------------------------+---------------------------------------------+
   |``spelling.er_or``               | -er vs. -or                                 |
   +---------------------------------+---------------------------------------------+
   |``spelling.in_un``               | in- vs. un-                                 |
   +---------------------------------+---------------------------------------------+
   |``spelling.misc``                | Spelling words corectly                     |
   +---------------------------------+---------------------------------------------+
   |``security.credit_card``         | Keeping credit card numbers secret          |
   +---------------------------------+---------------------------------------------+
   |``security.password``            | Keeping passwords secret                    |
   +---------------------------------+---------------------------------------------+
   |``sexism.misc``                  | Avoiding sexist language                    |
   +---------------------------------+---------------------------------------------+
   |``terms.animal_adjectives``      | Animal adjectives                           |
   +---------------------------------+---------------------------------------------+
   |``terms.denizen_labels``         | Calling denizens by the right name          |
   +---------------------------------+---------------------------------------------+
   |``terms.eponymous_adjectives``   | Calling people by the right name            |
   +---------------------------------+---------------------------------------------+
   |``terms.venery``                 | Call groups of animals by the right name    |
   +---------------------------------+---------------------------------------------+
   |``typography.diacritical_marks`` | Using dïacríticâl marks                     |
   +---------------------------------+---------------------------------------------+
   |``typography.exclamation``       | Avoiding overuse of exclamation             |
   +---------------------------------+---------------------------------------------+
   |``typography.symbols``           | Using the right symbols                     |
   +---------------------------------+---------------------------------------------+
   |``uncomparables.misc``           | Not comparing uncomparables                 |
   +---------------------------------+---------------------------------------------+
   |``weasel_words.misc``            | Avoiding weasel words                       |
   +---------------------------------+---------------------------------------------+
   |``weasel_words.very``            | Avoiding the word "very"                    |
   +---------------------------------+---------------------------------------------+


Theoretical background to our approach
======================================

Check usage, not grammar
------------------------

Proselint does not focus on grammar, which is at once too easy and too hard. 
Grammar is "too easy" because, for most native speakers, grammatical errors are easily identified (if not easily fixed).
The errors that would leave the greatest negative impression will often appear to be glaring from the perspective of native speakers. 
That would reduce a linter's job to catching mistakes in execution rather than in intent, obviating any chance of helping a writer improve in the course of her writing. 
On the other hand, more subtle errors like long range plurality noun-verb agreement requires[#]_  can evade even native speakers.
But it is precisely *because* these errors can pass by unnoticed that they can be safely ignored.

More pressingly, grammar is "too hard" because, in its most general form, detecting grammatical errors is AI-complete.
That is, it requires human-level intelligence and native speaker expertise to get things right(and even then it might not be enough). Furthermore, even if we did have the tools to identify grammatical rules, using those tools (by )

Instead, we consider errors of usage and style: redundancy, jargon, illogic, clichés, sexism, misspelling, inconsistency, misuse of symbols, malapropisms, oxymorons, security gaffes, hedging, apologizing, pretension, and more.

.. [#] Note that this was a purposefully placed noun-verb plurality agreement error. While potentially detectable, it is not as obviously problematic to the average speaker, meaning that rules like this are less crucial. 

Levels of difficulty
--------------------

In a loose analogy to the Chomskian hierarchy of formal grammars, we have identified levels of difficulty in problems faced by any language linter.

#. Replacement rules
#. Regex
#. Basic syntax processing
#. NLP, state-of-the-art
#. NLP, beyond state-of-the-art
#. AI-complete

One of the biggest differences between these levels of difficulty is how hard it is to successfully identify problems without introducing many false positives into the mix. 

Wield a rapier not a cudgel
---------------------------

Existing tools for improving prose raise so many false alarms that their advice can not be trusted. The writer must carefully consider whether to accept or reject each change.

We aim for a tool so precise that it becomes possible to unquestioningly adopt its recommendations and still come out ahead — with stronger, tighter prose. 
Better to be quiet and authoritative than loud and unreliable. 

To do this we limit the number of false positives, by measuring the performance performance of proselint by tracking its lintscore.

The lintscore is defined as 

.. math::
    \frac{T^{k+1}}{(T+F)^k}

where k is a free parameter that allows you to determine the degree to which the false positive rate is sensitive to the absolute number of true corrections versus the proportion of errors identified that are true positives. If instead we used the raw, scaled false positive rate :math:`\frac{T^{k}}{(T+F)^k}`, *k* becomes a temperature paramter that merely adjusts the implicit scale penalising false negatives in terms of how far it makes the value from 1.0 (or 100%).

This score does not take into account false negatives or true negatives, and the reason it does not is worth mentioning as it illustrates one of the core problems with prose linting.

False negatives can be understood in terms of cases where a rule should have activated and flagged the text, but failed to do so. True negatives can be understood as those opportunities where a rule was applied and successfully did not raise an error. Both of these ideas are problematic when analysing prose in a way that may not in other signal detection problems. Thus a full recall-precision curve analysis seems inappropriate in this domain.


Problem 0: Building off of a default
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In a tautological sense, every editor has a version of proselint (and any other automated writing aid) already installed, it is merely installed with the null rule-set.
That is, the set of rules that claim no substrings anywhere have any faults whatsoever; literally, anything goes.
Any time one will attempt to convince someone to adopt a tool, that tool needs to demonstrate itself as better than this default.

If people's prose was littered with errors to an egregious degree this default would not suffice.
But people are competent writers.
Proselint and other writing aids aim to polish what is already fairly good prose.
Thus, we can expect that any appropriate rule-set can expect to be invoked sparingly. 

Sparse use of the ruleset means that the positive statements are distinguished from the background of the null rule-set.
Because positives are what distinguish a writing aid, focusing on the false positive and true positive ratio
Negative statements are the remnants of the null rule-set, meaning they are less indicative of the quality of the linter.

In short, all linters and all language tools will be missing most errors by virtue of the problem they are trying to solve. Given this, avoiding the pitfalls of a high false-positive rate will be the comparison that matters most for determining their value.

Problem 1: Magnitude of "potential activations"
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It is not clear how many chances there are for a rule to be activated when one considers analysing prose. It could be at the sentence level or it could be at the word level, or it could be at the pairs of words level. If we are maximally generous, any subset of words could comprise a potential activation instance for a rule, meaning that the number of rule opportunities in the most liberal terms is the Bell number of the number of words in any document being analysed.

That means that without further specification, the number will grow extremely rapidly. If this occurs and the rule set is sparsely activated(it has specifically tailored rules in the manner of proselint), this means that the true negative score will be near 1, because there were so many opportunities for rules to be applied and they were not. If this occurs and the rule set is densely activated, the recommendations in aggregate will be incomprehensible as they will be so densely packed as to be unable to represent a coherent claim about the totality of the text.


Problem 2: Arbitrariness of "potential activations"
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If on the other hand you were to come up with a criterion that limits the number of potential activations, you now have an arbitrary criterion (likely defined by your language theory itself) that determines what counts as a potential activation. If different language theories postulate a set of potential activations that is neither a subset nor a superset of your rules, those language theories would then be incommeasurable [#]_.


.. [#] Note that this is not a problem for false positives because any rule that is not present in another theory can be treated as either a null result or a false positive by the theory lacking the rule. This stems from the fact that by default, all documents are already being analysed by the "null language theory" which states that there are no errors in any text. This gives a ground from which errors can be built up (since defining them in terms of the set of potential activations is so difficult) rather than winnowed down.

*Problem 3*: Infinitude/nonuniqueness of "potential activations"
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The same string (a sentence, for instance) can be analysed as being an error by two different theories for entirely different reasons. It is unclear whether two rules that identify the same text as problematic but differ in their justifications are in agreement or disagreement.

There are an infinite number of possible rule sets (in general), in the same way that there are an infinite number of possible strings.
So, if we consider all possible rule sets for evaluating any finite bit of prose, there will always be an infinite number of potential interpretations. Because those interpretations could conflict with one another while agreeing in a set theoretic sense on which substrings are to be flagged, you cannot count on any agreement that is characterised only in terms of the strings to be uniquely identifiable and associated with any particular set of potential activations.

*Problem 4*: False negatives are undefined without a positive model
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Finally, false negatives lack meaning without some particular positive model to be contrasted against the model under consideration.
A false negative states that a violation occurred that was not identified.
But one cannot say that a violation occurred without specifying what violation was that occurred, meaning that a positive model for identifying which violations were possible in the first place is neeeded.

Our implicit comparison is to the null model.
And the defining feature of the null-model is that it makes no positive statements at all.
Given that, there are no potential positive statements that proselint could miss. 
All negative statements are true negatives by fiat. 
For the least interesting reason possible, proselint has a perfect false-negative rate. 


.. proselint is precise. 

Assessing false positive rates
------------------------------

Unfortunately despite their cruciality, false positive rates pose quite a challenge as an assessment criterion.

Notably, a false positive is difficult (if not impossible) to identify without some kind of human intervention. 
Any automated system for determining whether some string of text is or is not an error is itself a normative theory of prose style as embodied in those determinations.
While it may not be a *linter* per se – for example, because of the speed or manner with which it is providing the statements – it is nonetheless equivalent to the normative role proselint plays.
Thus, while we would be able to provide comparisons between the recommendations offered for the same text by different normative language theories, that would not give us a good measure of false positives as it matters in terms of establishing trust with users.

To build the kind of trust we are aiming at, we need to be precisely attuned to the linguistic intuitions of human writers themselves. 
There is no way of knowing that a linting rule activation was successful or unsuccessful without direct feedback.
This is why we have developed a corpus of writings from well-established publications and manually coded them to identify false and true positives. 
It is this corpus that we use to measure proselint's lintscore. 

One of the biggest hindrances for adding new rules (at all) and more complicated and nuanced rules (in particular) stems from the difficulty of efficiently measuring how they affect our lintscore.
A key feature in growing proselint's capabilities will be establishing some mechanism for more efficiently inferring false positives.


Published expertise as primary source
-------------------------------------

This is one part of the motivation for using only expert language guides — they are human prose crafters who have honed their skills at identifying well and poorly styled prose.

proselint defers to the world’s greatest writers and editors. We didn’t make up this advice on our own. Instead, we aggregated their expertise, giving you direct access to humanity’s collective understanding about the craft of writing.


existing tools
==============

* 1Checker (http://www.1checker.com/)
* AbiWord's grammar checker (http://www.abisource.com/)
* After the Deadline (https://openatd.wordpress.com/)
* Alex (http://alexjs.com/)
* Autocrit (https://www.autocrit.com/editor/)
* ClearEdits (http://www.clearwriter.com/clearedits.html)
* CorrectEnglish (http://www.correctenglish.com/)
* CKEditor (http://www.webspellchecker.net/)
* Editor (http://www.serenity-software.com/)
* The Editorium (http://www.editorium.com/ETKPlus2014.htm)
* EditorSoftware (http://www.editorsoftware.com/)
* Edminton (http://editminion.com/)
* Expresso (http://expresso-app.org/)
* Ghotit (http://www.ghotit.com/)
* Ginger (http://www.gingersoftware.com/)
* GNU Diction (https://www.gnu.org/software/diction/)
* GNU Style (http://archive09.linux.com/feature/56833)
* Grac (http://grac.sourceforge.net/)
* GrammarBase (http://www.grammarbase.com/)
* GrammarCheck (http://www.grammarcheck.net/)
* Grammar Check Anywhere (https://www.spellcheckanywhere.com/grammar_check/)
* Grammar Expert Plus (http://www.wintertree-software.com/app/gramxp/)
* GrammarianPro (http://linguisoft.com/gramerrorfeatures.html)
* Grammark (https://github.com/markfullmer/grammark)
* Grammarly (https://www.grammarly.com/)
* Grammar Slammer (http://englishplus.com/grammar/)
* Grammatica (http://grammatica-english.soft32.com/)
* Grammatik (https://en.wikipedia.org/wiki/Grammatik)
* Graviax (http://graviax-grammar-checker.soft112.com/)
* Hemmingway (http://www.hemingwayapp.com/desktop.html)
* ivanistheone's scripts (https://github.com/ivanistheone/writing_scripts)
* Language Tool (https://www.languagetool.org/)
* Matt Might's shell scripts (http://matt.might.net/articles/shell-scripts-for-passive-voice-weasel-words-duplicates/)
* Microsoft Word's grammar check (https://support.office.com/en-us/article/Check-spelling-and-grammar-cab319e8-17df-4b08-8c6b-b868dd2228d1)
* OnlineCorrection.com (http://www.onlinecorrection.com/)
* PaperRater (https://www.paperrater.com/)
* PerfectIt (http://www.intelligentediting.com/)
* ProWritingAid (https://prowritingaid.com/)
* Reverso (http://www.reverso.net/)
* RightWriter (http://www.right-writer.com/)
* Rousseau (https://github.com/GitbookIO/rousseau)
* SpellCheckPlus (http://spellcheckplus.com/)
* Stilus (http://www.mystilus.com/Main)
* Textanz (http://www.textanz.com/)
* Virtual Writing Tutor (http://virtualwritingtutor.com/)
* Wave (https://en.wikipedia.org/wiki/Apache_Wave)
* WhiteSmoke (http://www.whitesmoke.com/)
* WordPerfect (http://www.wordperfect.com/us/)
* WinProof (http://www.franklinhu.com/winproof.htm)
* WordRake (http://www.wordrake.com/)
* write-good (https://github.com/btford/write-good)
* Writer's Workbench (http://www.emo.com/)

Infrastructural details
=======================

Contribution infrastructure
---------------------------

Issues are on github repo. 

Any new rules need to be accompanied by an expert source meriting the inclusion of the rule. 

Final decision of whether to include it in the default set of rules is up to us.

We have not included rule modules that are by default left off but can be turned on. 
Though we are not opposed to this in principle, it is difficult to see why we should do so. 
If someone wants to include rules that are not properly attributed, they are welcome to add the module to their own linter. 
We want to make that process simple. 
If someone wants to include rules that are properly attributed it is unclear why we would ever want to turn them off by default.
Furthermore, doing so would weaken our emphasis on encouraging contributions while leaving open the door for extensive customisation to adapt to your personal "style".


Code infrastructure
-------------------

Rule modules
^^^^^^^^^^^^

Proselint rules are organized into modules that reflect the structure on language advice found in usage guides. For example, Proselint includes a module ``terms`` that encourages idiomatic usage of vocabulary. It has as submodules specific kinds of terms that can be found as entries in usage guides. For example, one such submodule, ``terms.venery``,pertains to *venery terms*, which arose from hunting tradition and are used to describe groups of particular animals --- e.g., a "pride" of lions, or a "murmuration" of starlings. Another such submodule, ``terms.denizen_labels``, pertains to *demonyms*, which are used to describe people from a particular place --- e.g., *New Yorkers* (New York), *Mancunians* (Manchester), or *Novocastrians* (Newcastle).

Organizing rules into modules is useful both because it allows for a logical separation of similar rules, which often require similar computational machinery to implement, and also because it allows users to include and exclude rules at a higher level of abstraction than an individual word or phrase. One open challenge is how to allow customization at a level more finely grained than a submodule.

Rule templates
^^^^^^^^^^^^^^

Memoization
^^^^^^^^^^^

One of our goals is for Proselint to be efficient, able to run over a document in realtime as an author writes it. To achieve this goal, it is helpful to avoid redundant computation by storing the results of expensive function calls from one run of the linter to the next, a technique called memoization. For example, consider that many of Proselint's checks can operate at the level of a paragraph, and most paragraphs do not change when a sizable document is being edited --- at the extreme, where the linter is run after each keystroke, this is true by definition. By running checks over paragraphs, and recomputing only when the paragraph has changed, otherwise returning the memoized result, it is possible to reduce the total amount of computation and thus improve the linter's running time.

Concerns around normativity in prose styling
============================================

One of the most common critiques of proselint is a concern that introducing any kind of linter-like process to the act of writing prose would in some way diminish the ability for authors to express themselves creatively.
These arguments suggest that authors will find themselves limited in the set of things that are consistent with the linter's rules, and as a result that this will have a shaping or homogenising effect on prose.
There are many nuances around how exactly this is stated, but that general gist covers the core of the critique. 

To this critique there are several possible responses.
The first few apply in general, the latter apply in the case of scientific and technical writing.

A good deal of the advice in proselint points out that certain word sequences are problematic without suggesting any particular replacement text. There are a few reasons for this (including the computational natures of error-detection vs. solution-recommendation problems). The reason most relevant to this concern is that solution-recommendations are more likely to produce a homogenizing effect because they have a driving effect, wherein using a particular set of words is deemed superior to another set of words. Much in the way that the diversity of life-forms has arisen because of selective pressures, by eliminating the least fit combinations of words, the native variation in writing can flourish all the more readily.

The goal is not to homogenize text for the sake of uniformity, but rather to identify those cases that have been identified by respected authors and usage guides as being specifically problematic. Any text that is sufficiently artful and compelling to have not been specifically addressed by these sources should not be able to be caught by the linter.
Novelty will continue to introduce new usages, and some of them will be poor. 
Authors identified as trustworthy may point these out, but this will only be in retrospect. 
If one does not trust a guide's point of view, our strongest recommendation would be to turn off the modules associated with that guide.

Scientific writing is characterised by consistent 

And, as a final point, we can do little better than to give a modified quote from the Foreword[#]_ in Robert Bringhurst's The Elements of Typographic Style (version 3.2, 2004)
    
    [Language usage] thrives as a shared concern — and there are no paths at all where there are no shared desires and directions. A [language user] determined to forge new routes must move, like other solitary travellers, through uninhabited country and against the grain of the land, crossing common thoroughfares in the silence before dawn. The subject [of proselint] is not [stylistic] solitude, but the old, well-travelled roads at the core of the tradition: paths that each of us is free to follow or not, and to enter and leave when we choose — if only we know the paths are there and have a sense of where the lead. That freedom is denied us if the tradition is concealed or left for dead. Originality is everywhere, but much originality is blocked if the way back to earlier discoveries is cut or overgrown.

    -- Robert Bringhurst :cite:`bringhurst2004elements`

.. [#] Only because we are on the topic of historical traditions and stylistic guides, it should be mentioned that a foreword – according to book design tradition – would be written by an individual other than the author about the author, the book, and usually the relation between them. In this case, the section in Bringhurst's masterpiece labeled "Foreword" would likely be better described as "Preface" or "Introduction". Given his knowledge of book design, I shall assume that this was a conscious departure from the road of tradition, even if I cannot appreciate the new view that it offers.




Future
======
stuff will occur
.. Prosewash
.. ---------
.. Next steps: more intense processing with riskier rules
.. False positive checking with crowd sourcing
.. Feeds back to improve proselint

.. Including rules set to be off by default. One reason to have rules off by default but included might be because of their effect on the false positive rate.

Acknowledgements
================
Work on proselint was supported in part by the `Berkeley Center for Technology, Society and Policy`__ through the CTSP Fellows program, specifically as regards applying proselint to the problem of improving governmental communications as required the by `Federal Plain Language Guidelines`__.

.. __: https://ctsp.berkeley.edu/

.. __: http://www.plainlanguage.gov/howto/guidelines/FederalPLGuidelines

.. Bibliographies, citations and block quotes
.. ------------------------------------------

.. If you want to include a ``.bib`` file, do so above by placing  :code:`:bibliography: yourFilenameWithoutExtension` as above (replacing ``mybib``) for a file named :code:`yourFilenameWithoutExtension.bib` after removing the ``.bib`` extension. 

.. **Do not include any special characters that need to be escaped or any spaces in the bib-file's name**. Doing so makes bibTeX cranky, & the rst to LaTeX+bibTeX transform won't work. 

.. To reference citations contained in that bibliography use the :code:`:cite:`citation-key`` role, as in :cite:`hume48` (which literally is :code:`:cite:`hume48`` in accordance with the ``hume48`` cite-key in the associated ``mybib.bib`` file).

.. However, if you use a bibtex file, this will overwrite any manually written references. 

.. So what would previously have registered as a in text reference ``[Atr03]_`` for 

.. .. :: 

.. ..      [Atr03] P. Atreides. *How to catch a sandworm*,
..            Transactions on Terraforming, 21(3):261-300, August 2003.

.. what you actually see will be an empty reference rendered as **[?]**.

.. E.g., [Atr03]_.


.. If you wish to have a block quote, you can just indent the text, as in 

..     When it is asked, What is the nature of all our reasonings concerning matter of fact? the proper answer seems to be, that they are founded on the relation of cause and effect. When again it is asked, What is the foundation of all our reasonings and conclusions concerning that relation? it may be replied in one word, experience. But if we still carry on our sifting humor, and ask, What is the foundation of all conclusions from experience? this implies a new question, which may be of more difficult solution and explication. :cite:`hume48`


.. Source code examples
.. --------------------

.. Of course, no paper would be complete without some source code.  Without
.. highlighting, it would look like this::

..    def sum(a, b):
..        """Sum two numbers."""

..        return a + b

.. With code-highlighting:

.. .. code-block:: python

..    def sum(a, b):
..        """Sum two numbers."""

..        return a + b

.. Maybe also in another language, and with line numbers:

.. .. code-block:: c
..    :linenos:

..    int main() {
..        for (int i = 0; i < 10; i++) {
..            /* do something */
..        }
..        return 0;
..    }

.. Or a snippet from the above code, starting at the correct line number:

.. .. code-block:: c
..    :linenos:
..    :linenostart: 2

..    for (int i = 0; i < 10; i++) {
..        /* do something */
..    }
 
.. Important Part
.. --------------

.. It is well known [Atr03]_ that Spice grows on the planet Dune.  Test
.. some maths, for example :math:`e^{\pi i} + 3 \delta`.  Or maybe an
.. equation on a separate line:

.. .. math::

..    g(x) = \int_0^\infty f(x) dx

.. or on multiple, aligned lines:

.. .. math::
..    :type: eqnarray

..    g(x) &=& \int_0^\infty f(x) dx \\
..         &=& \ldots

.. The area of a circle and volume of a sphere are given as

.. .. math::
..    :label: circarea

..    A(r) = \pi r^2.

.. .. math::
..    :label: spherevol

..    V(r) = \frac{4}{3} \pi r^3

.. We can then refer back to Equation (:ref:`circarea`) or
.. (:ref:`spherevol`) later.

.. Mauris purus enim, volutpat non dapibus et, gravida sit amet sapien. In at
.. consectetur lacus. Praesent orci nulla, blandit eu egestas nec, facilisis vel
.. lacus. Fusce non ante vitae justo faucibus facilisis. Nam venenatis lacinia
.. turpis. Donec eu ultrices mauris. Ut pulvinar viverra rhoncus. Vivamus
.. adipiscing faucibus ligula, in porta orci vehicula in. Suspendisse quis augue
.. arcu, sit amet accumsan diam. Vestibulum lacinia luctus dui. Aliquam odio arcu,
.. faucibus non laoreet ac, condimentum eu quam. Quisque et nunc non diam
.. consequat iaculis ut quis leo. Integer suscipit accumsan ligula. Sed nec eros a
.. orci aliquam dictum sed ac felis. Suspendisse sit amet dui ut ligula iaculis
.. sollicitudin vel id velit. Pellentesque hendrerit sapien ac ante facilisis
.. lacinia. Nunc sit amet sem sem. In tellus metus, elementum vitae tincidunt ac,
.. volutpat sit amet mauris. Maecenas [#]_ diam turpis, placerat [#]_ at adipiscing ac,
.. pulvinar id metus.

.. .. [#] On the one hand, a footnote.
.. .. [#] On the other hand, another footnote.

.. .. figure:: figure1.png

..    This is the caption. :label:`egfig`

.. .. figure:: figure1.png
..    :align: center
..    :figclass: w

..    This is a wide figure, specified by adding "w" to the figclass.  It is also
..    center aligned, by setting the align keyword (can be left, right or center).

.. .. figure:: figure1.png
..    :scale: 20%
..    :figclass: bht

..    This is the caption on a smaller figure that will be placed by default at the
..    bottom of the page, and failing that it will be placed inline or at the top.
..    Note that for now, scale is relative to a completely arbitrary original
..    reference size which might be the original size of your image - you probably
..    have to play with it. :label:`egfig2`

.. As you can see in Figures :ref:`egfig` and :ref:`egfig2`, this is how you reference auto-numbered
.. figures.

.. .. table:: This is the caption for the materials table. :label:`mtable`

..    +------------+----------------+
..    | Material   | Units          |
..    +============+================+
..    | Stone      | 3              |
..    +------------+----------------+
..    | Water      | 12             |
..    +------------+----------------+
..    | Cement     | :math:`\alpha` |
..    +------------+----------------+


.. We show the different quantities of materials required in Table
.. :ref:`mtable`.


.. .. The statement below shows how to adjust the width of a table.

.. .. raw:: latex

..    \setlength{\tablewidth}{0.8\linewidth}


.. .. table:: This is the caption for the wide table.
..    :class: w

..    +--------+----+------+------+------+------+--------+
..    | This   | is |  a   | very | very | wide | table  |
..    +--------+----+------+------+------+------+--------+

.. Unfortunately, restructuredtext can be picky about tables, so if it simply
.. won't work try raw LaTeX:


.. .. raw:: latex

..    \begin{table*}

..      \begin{longtable*}{|l|r|r|r|}
..      \hline
..      \multirow{2}{*}{Projection} & \multicolumn{3}{c|}{Area in square miles}\tabularnewline
..      \cline{2-4}
..       & Large Horizontal Area & Large Vertical Area & Smaller Square Area\tabularnewline
..      \hline
..      Albers Equal Area  & 7,498.7 & 10,847.3 & 35.8\tabularnewline
..      \hline
..      Web Mercator & 13,410.0 & 18,271.4 & 63.0\tabularnewline
..      \hline
..      Difference & 5,911.3 & 7,424.1 & 27.2\tabularnewline
..      \hline
..      Percent Difference & 44\% & 41\% & 43\%\tabularnewline
..      \hline
..      \end{longtable*}

..      \caption{Area Comparisons \DUrole{label}{quanitities-table}}

..    \end{table*}

.. Perhaps we want to end off with a quote by Lao Tse [#]_:

..   *Muddy water, let stand, becomes clear.*

.. .. [#] :math:`\mathrm{e^{-i\pi}}`

.. Customised LaTeX packages
.. -------------------------

.. Please avoid using this feature, unless agreed upon with the
.. proceedings editors.

.. ::

..   .. latex::
..      :usepackage: somepackage

..      Some custom LaTeX source here.

References
----------
.. [Atr03] P. Atreides. *How to catch a sandworm*,
           Transactions on Terraforming, 21(3):261-300, August 2003.


