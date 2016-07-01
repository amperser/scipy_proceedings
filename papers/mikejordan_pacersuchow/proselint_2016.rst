:author: Michael D. Pacer
:email: mpacer@berkeley.edu
:institution: University of California, Berkeley

:author: Jordan W. Suchow
:email: suchow@berkeley.edu
:institution: University of California, Berkeley

:video: http://www.youtube.com/
:bibliography: mybib

.. raw:: latex

    \newcommand{\DUrolesc}{\textsc}
    \newcommand{\DUrolesf}{\textsf}
    \newcommand{\DUroleprotect[1]}{\protect{#1}}
    
.. role:: sc

.. role:: sf

.. role:: protect

========================================================================
Proselint: the linting of science prose and the science of linting prose
========================================================================

.. class:: abstract

   Writing is notoriously hard, even for the best writers, and it's not for lack of good advice — a tremendous amount of knowledge about the craft is strewn across usage guides, dictionaries, technical manuals, essays, pamphlets, websites, and the hearts and minds of great authors and editors. But this knowledge is trapped, waiting to be extracted and transformed.

   We built Proselint, a Python-based linter for prose. Proselint identifies violations of expert style and usage guidelines. Proselint is open-source software released under the BSD license and is compatible with Python 2 and 3. It runs as a command-line utility or editor plugin (e.g., for Sublime Text, Atom, Vim, Emacs) and outputs advice in standard formats, including JSON. Proselint includes modules that address redundancy, jargon, illogic, clichés, unidiomatic vocabulary, sexism, misspelling, inconsistency, misuse of symbols, malapropisms, oxymorons, security gaffes, hedging, apologizing, and pretension. Further, Proselint is extensible, enabling creating of domain-specific modules or implementation of house style guides.

   Proselint can be seen as both a language tool for scientists and a tool for language science. On the one hand, it includes modules that promote clear and consistent prose in science writing, helping scientists to communicate their ideas and promoting the public's understanding of science. On the other, it measures language usage and explores the factors relevant to creating a useful linter.

.. class:: keywords

   linters, writing tools, copyediting

The problem
===========

.. add a tikz amperser

Writing is notoriously hard, even for the best writers, and it's not for lack of good advice — a tremendous amount of knowledge about the craft is strewn across usage guides, dictionaries, technical manuals, essays, pamphlets, websites, and the hearts and minds of great authors and editors. Consider, for example, *Garner's Modern English Usage*, an authoritative usage guide with 11,000 entries covering a broad range of advice that, when followed, helps writers produce clean and idiomatic prose. Or consider the *Federal Plain Language Guidelines*, a 2011 guide created by employees of the U.S. federal government to promote writing that is clear, concise, and well-organized. Professional conferences such as the annual meeting of the American Copy Editors Society are dedicated to sharing knowledge about editing prose. And within the academy, organizations such as the American Psychological Association publish manuals whose guidance on style has been adopted as a standard. Advice on writing abounds.

Advice on writing touches upon everything from superficial conventions to the deepest reflections of our society and its attitudes. Take for example advice concerning the preferred forms of words such as "connote" (vs. "connotate"), which may help to prune needless variants in spelling, but are unlikely to effect the reader's understanding of the text and its author. Compare this to advice concerning needlessly gendered language ("woman scientist", "policeman"), which by being commonplace in language may perpetuate social inequality.

Having amassed a pile of useful advice is not enough to make writing better. This is becasue advice, though it may be principled, thoughtful, and worth following, is hard to apply in new settings once it has been learned :cite:`Argote2000`. Thus, even if one could absorb all the knowledge contained in these sources, there would still be the problem of recalling and systematically applying it. And even when its applicability is recognized, developing a new habit is still slow, costly, and difficult :cite:`Fogg2010`. Errors will appear and mistakes will be made.

.. linter advantage: Instant feedback? e.g.,

Today, an author wishing to improve a piece of writing by applying the collective wisdom of experts must rely on indirect means. The most common approach, used extensively in publishing, is a division of labour whereby dedicated staff with deep knowledge of best practices in writing copyedit a piece to their satisfaction. This is the approach used, for example, by *The New Yorker*, whose editing team includes fact checkers, editors, grammarians, and more. A second approach, used extensively in desktop publishing, is to use software-based tools such as spelling and grammar checkers that mark unrecognized words and purported violations of grammatical rules.

Neither approach fully solves the problem of adopting best practices in writing. Few people have the resources to outsource editing to expert staff, and even if they did, getting that advice inevitably takes time because copyeditors do not look over one's shoulder and whisper advice during the act of writing. By the time an editor's notes are received, the best opportunity to strengthen the writer's craft has passed. Software-based tools, though they are inexpensive and fast, are typically incomplete, imprecise, or inaccessible.

Our collective knowledge about best practices in writing is thus essentially trapped, waiting to be extracted and transformed into a medium that makes the knowledge immediately accessible to all authors.

The solution
============

To solve this problem, we built Proselint, a real-time linter for English prose. A linter is a computer program that, like a spell checker, scans through a document and analyses it, identifying problems with its syntax or style. Though many linters are used only after the fact, writing advice is best dispensed as you write. Our goal with Proselint is to aggregate knowledge about best practices in writing and to make that knowledge immediately accessible to authors in the form of a linter for prose. Proselint thus identifies violations of the style and usage guidelines that have been endorsed by experts.

Proselint is open-source software released under the BSD license and compatible with Python 2 and 3. It runs efficiently as a command-line utility or editor plugin for SublimeText, Atom, Emacs, vim, &c. It outputs advice in standard formats, including JSON, allowing for integration with external services. Proselint includes modules on a variety of usage problems, including redundancy, jargon, illogic, clichés, sexism, misspelling, inconsistency, misuse of symbols, malapropisms, oxymorons, security gaffes, hedging, apologizing, pretension, and more. 

Two views on Proselint
======================

Proselint can be seen as both a language tool for scientists and a tool for language science. On the one hand, it can be used to improve writing, and it includes modules that promote clear and consistent prose in science writing. On the other, it can be used to measure language usage and to consider the factors relevant to a linter's usefulness.


As a language tool for scientists
----------------------------------

Science and writing are fast friends --- science as we know it would be impossible without the written word. But scientific research is, by necessity, hard to understand by all but those most acquainted with it, and harder still to communicate to other scientists and to the public. This leaves room for tools that assist in writing to further the aims of scientists and promote the public's understanding of science. 

Proselint improves writing across a number of dimensions relevant to the communication of science, including consistency in terminology and typography; concision; and redundancy. For example, Proselint checks for use of the multiplication symbol × when giving screen dimensions (e.g. 1440 × 900), mispecifications of *p* values commonly caused by software package's truncation of small numbers (*p* = 0.00), and colloquialisms that obscure the mechanisms of science-based technology (e.g., "lie detector test" for the polygraph machine, which measures arousal, not lying per se).

As a tool for language science
------------------------------

Linguistics as a science is largely a descriptivist enterprise, seeking to describe language as it is used rather than prescribe how it ought to be used. Errors are considered in the context of how people successfully learn language and how their errors in doing so (especially children's) reveal the underlying structure of the language learning mechanism (see, e.g.,  overregularization by young English speakers :cite:`marcus1992overregularization`). A focus on identifying the stylistic errors in peoples' language use does not fit the descriptivist approach common to linguists.

One application of Proselint as a tool for language science is in tracking historical trends in usage. Corpora such as the Google Books have been useful for measuring changes in the prevalence of words and phrases over several hundred years. Our tool, in providing a feature set for usage, can be used in a similar way. For example, one might study the prevelance of airlinese (e.g., use of "momentarily" to mean "in a moment", as in the phrase "we are taking of momentarily") and its alignment with the rise of that industry.

Another application of Proselint as a tool for language science is in stylometry and authorship identification; instead of using standard stylometric measures, which include word frequencies, we can consider Proselint's rules as a feature set that can be used to identify authors. In a sense, this would allow us to identify authors based not on their language use, but on their language misuse. 

This second application enables further extensions and generalizations, including for example the obfuscation of identity or coding of messages by selective introduction or removal of usage choices. Though we have emphasized cases where the goal is to recommend best practices in usage, the Proselint infrastructure can alternatively be used to identify cases where there is more than one acceptable choice. One could, for example, take a document and identify instances where multiple phrases could be reasonably substituted. One could then create a modified version of the document that uses these usage choices to encode a message, without the document demonstrating itself to contain an encoded message. With moderate modifications, then, Proselint could be a system for designing content-aware steganographic systems, conveying hidden messages in their choice of words and styles :cite:`bergmair2006content`.

In our testing of Proselint, we assembled a corpus of text from well-edited magazines containing low rates of usage errors. When doing so, we noticed that there are no available annotated corpora that can provide stylistic false-positive rates. The theoretical work analyzing lintscores and the problem of error detection from a framework inspired by signal detection theory would be difficult to fathom without first postulating the existence of such a corpus. The Proselint testing framework is an excellent opportunity to develop such a corpus.


Results
=======
As a proof of concept, we used Proselint to make contributions to several documents, including the White House's Federal Source Code Policy; The Open Logic Project textbook on advanced logic; Infoactive's *Data + Design* book; and many of the other papers contributed to *SciPy 2016*. In addition, to evaluate Proselint's false-alarm rate, we developed a corpus of essays from well-edited magazines such as *Harper's Magazine*, *The New Yorker*, and *The Atlantic* and measured the lintscore, defined below. Because the essays included in our corpus were edited by a team of experts, we expect Proselint to remain mostly silent, commenting only on the rare error that slips through unnotcied by the editors or, more commonly, on the finer points of usage, about which experts may disagree. When run over v0.1.0 of our corpus, we acheived a lintscore of 98.8, reflecting detection of XX errors with XX false alarms (*k* = 2).

.. Our general approach
.. ====================

.. Dividing up the problem space
.. -----------------------------

.. There are many ways to divide up the kinds of problems that plague any language error correction system.


.. Difficulty in defining rules and detecting violations
.. ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. A linter makes a decision at every line whether or it violates any particular rule.
.. There is no way around that problem, as the key is to provide immediate feedback to writers as they write.
.. We have discovered rough difficulty classes in detecting whether a rule should be fired for any particular string. 
.. That difficulty 

.. #.  Divide up problem types into levels of difficulty. (how hard is it to identify that a rule should be fired)

..     #. One-to-one replacement rules
..     #. Regular expressions
..     #. Basic syntax processing
..     #. NLP, state-of-the-art
..     #. NLP, beyond state-of-the-art
..     #. AI-hard



.. #.  Divide up by content (What sorts of rules say similar things to this one?)

..     #. This is the basis for our module structure.

.. #. Divide up by response type (recommendation vs. prohibition)(what should you do when this rule fires)


.. Desiderata for a linter
.. -----------------------

.. Desiderata are a set of desired criteria; these exist for almost all artefact classes, and usually stem from the aim for which the artefact is created. Like other designed systems, linters' ideal features stem from both the nature of the problem that they solve and the manner in which they attempt to solve the problem. 

.. Linters (in a programming context) identify instances of code that either explicitly violates a set of stylistic rules (as in PEP8_) or is otherwise suspicious (as in cases where a variable is used before it has a value).

.. .. _PEP8: https://www.python.org/dev/peps/pep-0008/

.. Thus to fulfill their aim, linters should  

.. *   scale to arbitrarily many rules,
.. *   flag exactly those instances of code that are suspicious,
.. *   and flag no nonsuspicious code spuriously.

.. In most software linters, the perfect false positive rate and negative rate will be established by fiat; style rules that cannot be so implemented are simply not implemented. 
.. In a linter for natural language one cannot count on the linter to be so accurate. 
.. Additionally, we see some features as desirable in a prose linter that are not strictly necessary for software linters. 

.. We want our linter to respond in 

.. *   respond needs to be in real time



..     * This limits how much processing can occur per rule.

.. *   responses should be relatively monotonic (i.e., we should minimise the number of lints that are due to sentences that have not yet been completed)
.. *   it needs to be able to be installed easily by the end-user
.. *   it should be modifiable fairly easily (i.e., if a user does not like a particular rule set it should be able to be turned off)
.. *   it needs to explain why it raising the flags it raises

.. We have identified several features implicit to the problem of error detection and correction in general, and of language linting specifically.


.. Large-scale problems require scalable resources
.. -----------------------------------------------

.. Open source license allows the community of users to become a community of builders. 
.. Many of the rules' implementations are particularly well-suited to small-scale coding projects or assignments.


.. the principles we've identified
.. -------------------------------

.. Low false positive rates

.. how our tool address or uses each of those principles
.. -----------------------------------------------------

Using Proselint
===============

Installation
------------
Proselint is available on the Python Package Index and can be installed using pip:

.. code-block:: bash

   pip install Proselint

Alternatively, those wishing to develop Proselint can retrive the Git reposity from https://github.com/amperser/Proselint and then install the software using setuptools: 

.. code-block:: bash

   python setup.py develop


Command-line utility
--------------------

At its core, Proselint is a command-line utility that reads in a text file:

.. code-block:: bash

   Proselint text.md

Running this command prints a list of suggestions to stdout, one per line. Each suggestion has the form:

.. code-block:: bash

   text.md:<line>:<column>: <check_name> <message>

For example,

.. code-block:: bash

  text.md:0:10: uncomparables.misc Comparison of ... 
  an uncomparable: 'unique' can not be compared.

suggests that, at column 10 of line 0, the check ``uncomporables.misc`` detected an issue where the uncomparable adjective "unique" was compared, as in "very unique". The command line utility can also print the list of suggestions in JSON using the ``--json`` flag. In this case, the output is considerably richer:

.. code-block:: javascript

  {
      // The check originating this suggestion.
      "check": "uncomparables.misc",

      // Message describing the suggestion.
      "message": "Comparison of an uncomparable: ...
      'unique' can not be compared.",

      // The source of the suggestion.
      "source": "David Foster Wallace"

      // URL pointing to source material.
      "source_url": "http://www.telegraph.co.uk ...
      /a/9715551"

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

      // Importance ("suggestion", "warning", "error")
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
An effective way to promote adoption of best practices in writing through linters is to embed linters within the tools that people already use to write. Towards that aim, available for Proselint are plugins for popular text editors, including Emacs, vim, Sublime Text, and Atom, some created by us, some contributed by others.


Advice: sources and examples
============================

Proselint is built around advice [#]_ derived from works by Bryan Garner, David Foster Wallace, Chuck Palahniuk, Steve Pinker, Mary Norris, Mark Twain, Elmore Leonard, George Orwell, Matthew Butterick, William Strunk, E.B. White, Philip Corbett, Ernest Gowers, and the editorial staff of the world’s finest literary magazines and newspapers, among others. Our goal is to aggregate knowledge about best practices in writing and to make that knowledge immediately accessible to all authors in the form of a linter for prose. Tables 1 and 2 list many of the rules that Proselint currently implements.

.. [#] Proselint has not been endorsed by these individuals; we have merely taken their words and implemented them in code. 


Examples of some rules
----------------------

The following are examples of rules meant to give a taste of the range of advice that Proselint can give:

#. Detecting the word "agendize", Proselint notes, "agendize is jargon, could you replace it with something more standard?" :cite:`garner2016garner`

#. In response to "In recent years, an increasing number of psychologists have", Proselint notes, "Professional narcisissm. Talk about the subject, not its study." :cite:`pinker2015sense`

#. In response to "A group of starlings", Proselint notes "The venery terms is 'murmuration'"". :cite:`garner2016garner`


.. One Issues are on github repo. 

.. Any new rules need to be accompanied by an expert source meriting the inclusion of the rule. 

.. Final decision of whether to include it in the default set of rules is up to us.

.. We have not included rule modules that are by default left off but can be turned on. 
.. Though we are not opposed to this in principle, it is difficult to see why we should do so. 
.. If someone wants to include rules that are not properly attributed, they are welcome to add the module to their own linter. 
.. We want to make that process simple. 
.. If someone wants to include rules that are properly attributed it is unclear why we would ever want to turn them off by default.
.. Furthermore, doing so would weaken our emphasis on encouraging contributions while leaving open the door for extensive customisation to adapt to your personal "style".

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
   |``dates_times.am_pm``            | Using the right form for  time              |
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
   |``misc.commercialese``           | Avoiding commerical jargon                  |
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

.. table:: What Proselint checks (cont.). :label:`checkscont`

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


Proselint's approach
======================================

Check usage, not grammar
------------------------

Proselint does not focus on grammar, which is at once too easy and too hard:

Grammar is too easy in the sense that, for most native speakers, grammatical errors are readily identified, if not easily fixed. The errors that leave the greatest negative impression in the reader's mind are often glaring to native speaker. On the other hand, more subtle errors such as disagreement in number across long ranges can go undetected even by native speakers [sic].

In contrast, grammar is too hard in the sense that, in its most general form, detecting grammatical errors is AI-hard, requiring human-level intelligence and the expertise of a native speaker to get things right. Even then, it might not be enough.

Instead of focussing on grammar, we consider errors of usage and style: redundancy, jargon, illogic, clichés, sexism, misspelling, inconsistency, misuse of symbols, malapropisms, oxymorons, security gaffes, hedging, apologizing, pretension, and more.


Levels of difficulty
--------------------

.. possibly replace with image?

In a loose analogy to the Chomskian hierarchy of formal grammars, we have identified several levels of difficulty in the implementation of the detection and correction of usage errors:

#. AI-hard
#. NLP, beyond state-of-the-art
#. NLP, state-of-the-art
#. Syntax processing
#. Regular expressions
#. One-to-one replacement rules. 

At one extreme are usage errors that can be detected and corrected through one-to-one replacement rules, detecting the presence of a specific word or phrase and suggesting another in its place. At the other are usage errors whose detection and correction are such hard computational problems that it would require human-level intelligence to solve in the general case. Consider, for example, usage errors pertaining to the word "only", whose correct placement depends on the intended meaning (e.g., in "John hit Peter in his only nose", is the "only" misplaced or is it unusual that Peter has only one nose?). These usage errors, which are at the hierarchy's highest levels, are harder to successfully identify without introducing many false positives into the mix. Our development of Proselint begins at the lowest levels of the hierarchy, building upwards.

Rapiers, cudgels, and the lintscore
-----------------------------------

Any new tool (for language, or otherwise) faces a challenge to its adoption: it must demonstrate that the cost of learning to use the tool is outweighed by the marginal utility it provides. Pen & ink, paper, and the computer each facilitated language production by enabling new modes of communication and, in doing so, provided obvious value. In contrast, tools that improve existing capabilities are at a comparative disadvantage: they must demonstrate a substantial improvement over the status quo. This is the case for Proselint. When the use of the tool requires modifying existing workflows, greater utility must be demonstrated to offset the additional cost.

Because of this need to demonstrate utility, earlier language tools attempted to offer as much help as possible. In a sense, they wielded a cudgel, a tool that indiscriminately injures large areas of flesh. Each time a language tool flags an issue, it might be an error, but it might instead be a false alarm. Let :math:`T` be the number of true errors, and :math:`F` be the number of false alarms (thus making :math:`T+F` the total number of flags raised by the tool). The cudgel approach attempts to maximize :math:`T`, finding as many errors as possible, without considering :math:`F`. Writers who use those tools would see many genuine errors, even errors that Proselint would not detect. However, their emphasis on maxizing :math:`T` is to their detriment because these tools raise so many false alarms that their advice cannot be trusted. The writer must carefully consider whether to accept or reject each change. 

Proselint aims to be not a cudgel, but a rapier, a tool that pinpoints weak spots and strikes where it will make the most impact. With Proselint, we aim for a tool so precise that it becomes possible to unquestioningly adopt its recommendations and still come out ahead with stronger, tighter prose. Better to be quiet and authoritative than loud and unreliable. 

To acheive this, we limit the number of false positives :math:`F` by measuring the performance of Proselint through its lintscore. The lintscore gives one point for every true positive (:math:`T`) and penalizes on the basis of the false-positive rate (:math:`\alpha = \frac{F}{T+F}`). The lintscore is given by

.. math::
    l(T,F;k) = T(1-\alpha)^k,

where :math:`k` is a free parameter that controls the strictness of the penalty imposed by :math:`1-\alpha`.

Published expertise as primary source
-------------------------------------

This is one part of the motivation for using only expert language guides — they are human prose crafters who have honed their skills at identifying well and poorly styled prose.

Proselint defers to the world’s greatest writers and editors. We didn’t make up this advice on our own. Instead, we aggregated their expertise, giving you direct access to humanity’s collective understanding about the craft of writing.


Existing tools
==============

Here are some of the existing tools for automated language checkers:
`1Checker <http://www.1checker.com/>`_, `AbiWord's grammar checker <http://www.abisource.com/>`_, `After the Deadline <https://openatd.wordpress.com/>`_, `Alex <http://alexjs.com/>`_, `Autocrit <https://www.autocrit.com/editor/>`_, `ClearEdits <http://www.clearwriter.com/clearedits.html>`_, `CorrectEnglish <http://www.correctenglish.com/>`_, `CKEditor <http://www.webspellchecker.net/>`_, `Editor <http://www.serenity-software.com/>`_, `The Editorium <http://www.editorium.com/ETKPlus2014.htm>`_, `EditorSoftware <http://www.editorsoftware.com/>`_, `Edminton <http://editminion.com/>`_, `Expresso <http://expresso-app.org/>`_, `Ghotit <http://www.ghotit.com/>`_, `Ginger <http://www.gingersoftware.com/>`_, `GNU Diction <https://www.gnu.org/software/diction/>`_, `GNU Style <http://archive09.linux.com/feature/56833>`_, `Grac <http://grac.sourceforge.net/>`_, `GrammarBase <http://www.grammarbase.com/>`_, `GrammarCheck <http://www.grammarcheck.net/>`_, `Grammar Check Anywhere <https://www.spellcheckanywhere.com/grammar_check/>`_, `Grammar Expert Plus <http://www.wintertree-software.com/app/gramxp/>`_, `GrammarianPro <http://linguisoft.com/gramerrorfeatures.html>`_, `Grammark <https://github.com/markfullmer/grammark>`_, `Grammarly <https://www.grammarly.com/>`_, `Grammar Slammer <http://englishplus.com/grammar/>`_, `Grammatica <http://grammatica-english.soft32.com/>`_, `Grammatik <https://en.wikipedia.org/wiki/Grammatik>`_, `Graviax <http://graviax-grammar-checker.soft112.com/>`_, `Hemmingway <http://www.hemingwayapp.com/desktop.html>`_, `ivanistheone's scripts <https://github.com/ivanistheone/writing_scripts>`_, `Language Tool <https://www.languagetool.org/>`_, `Matt Might's shell scripts <http://matt.might.net/articles/shell-scripts-for-passive-voice-weasel-words-duplicates/>`_, `Microsoft Word's grammar check <https://support.office.com/en-us/article/Check-spelling-and-grammar-cab319e8-17df-4b08-8c6b-b868dd2228d1>`_, `OnlineCorrection.com <http://www.onlinecorrection.com/>`_, `PaperRater <https://www.paperrater.com/>`_, `PerfectIt <http://www.intelligentediting.com/>`_, `ProWritingAid <https://prowritingaid.com/>`_, `Reverso <http://www.reverso.net/>`_, `RightWriter <http://www.right-writer.com/>`_, `Rousseau <https://github.com/GitbookIO/rousseau>`_, `SpellCheckPlus <http://spellcheckplus.com/>`_, `Stilus <http://www.mystilus.com/Main>`_, `Textanz <http://www.textanz.com/>`_, `Virtual Writing Tutor <http://virtualwritingtutor.com/>`_, `Wave <https://en.wikipedia.org/wiki/Apache_Wave>`_, `WhiteSmoke <http://www.whitesmoke.com/>`_, `WordPerfect <http://www.wordperfect.com/us/>`_, `WinProof <http://www.franklinhu.com/winproof.htm>`_, `WordRake <http://www.wordrake.com/>`_, `write-good <https://github.com/btford/write-good>`_, and `Writer's Workbench <http://www.emo.com/>`_.

Infrastructural details
=======================

Contribution infrastructure
---------------------------

There are many ways to contribute to Proselint. 

One primary avenue is to use issues on our GitHub repository. 

New rules need to be accompanied by an expert source meriting the inclusion of the rule. 

The final decision of whether to include it in the default set of rules is up to us.

We have not included rule modules that are by default left off but can be turned on. 
Though we are not opposed to this in principle, it is difficult to see why we should do so. 
If someone wants to include rules that are not properly attributed, they are welcome to add the module to their own linter. 
We want to make that process simple. 
If someone wants to include rules that are properly attributed it is unclear why we would ever want to turn them off by default.
Furthermore, doing so would weaken our emphasis on encouraging contributions while leaving open the door for extensive customisation to adapt to your personal "style".


Code infrastructure
-------------------

:sc:`Rule modules`
^^^^^^^^^^^^^^^^^^

Proselint rules are organized into modules that reflect the structure on language advice found in usage guides. For example, Proselint includes a module ``terms`` that encourages idiomatic vocabulary. It has submodules with specific kinds of terms that can be found as entries in usage guides. For example, one such submodule, ``terms.venery``, pertains to *venery terms*, which arose from hunting tradition and are used to describe groups of particular animals: for example, a "pride" of lions or an "unkindness" of ravens. Another such submodule, ``terms.denizen_labels``, pertains to *demonyms*, which are used to describe people from a particular place: for example, *New Yorkers* (New York), *Mancunians* (Manchester), or *Novocastrians* (Newcastle).

Organizing rules into modules is useful for a couple of reasons. It allows for a logical separation of similar rules, which often require similar computational machinery to implement. It also allows users to include and exclude rules at a higher level of abstraction than an individual word or phrase. But people may wish to customise their linting rules at a level more finely grained than the submodule. It is unclear how to allow this without making that format for customisation painful to navigate, modify or comprehend.

:sc:`Rule templates`
^^^^^^^^^^^^^^^^^^^^

In general a rule needs to simply take in a string of text of some sort, and then apply some sort of logic identifying whether a rule has been violated, and return a value in the correct format.

In order to ease the production of new rules, we have written functions that help in following the protocol for commonly used kinds of rules. These include checking checking for whether a word exists (``existence_check()``), cross-document consistency in usage (``consistency_check()``), and suggesting preferred forms of usage (``preferred_forms_check()``). 

Here is an example of a rule as implemented by the ``existence check`` rule template. 

.. code-block:: python

    @memoize
    def check_midnight_noon(text):
        """Check the text."""
        err = "dates_times.am_pm.midnight_noon"
        msg = (u"12 a.m. and 12 p.m. are wrong and confusing."
               " Use 'midnight' or 'noon'.")
        regex = "12 ?[ap]\.?m\.?"
        return existence_check(text, [regex], err, msg)

This checks whether someone has used either 12am or 12pm (or many variants, e.g., 12AM, 12 P.M, 12aM.) and suggests the author use noon or midnight as is appropriate [#]_. 

.. [#] Note, we could not used a preferred forms template because it is not clear which of these the author used due to the ambiguity of the terms that the rule is trying to alleviate.

.. A simplified version of ``existence_check()`` ``consistency_check()`` and ``preferred_forms_check()`` follow.

.. .. code-block::python
    
..     def consistency_check(text, word_pairs, err, msg, offset=0):
..         """Build a consistency checker."""
..         errors = []
..         msg = " ".join(msg.split())
..         for w in word_pairs:
..             matches = [
..                 [m for m in re.finditer(w[0], text)],
..                 [m for m in re.finditer(w[1], text)]
..             ]
..             if len(matches[0]) > 0 and len(matches[1]) > 0:
..                 idx_minority = len(matches[0]) > len(matches[1])
..                 for m in matches[idx_minority]:
..                     errors.append((
..                         m.start() + offset,
..                         m.end() + offset,
..                         err,
..                         msg.format(w[~idx_minority], m.group(0)),
..                         w[~idx_minority]))
..         return errors


..     def preferred_forms_check(text, list, err, msg,
..                               ignore_case=True, offset=0,
..                               max_errors=float("inf")):
..         """Build a checker that suggests the preferred form."""
..         if ignore_case: flags = re.IGNORECASE
..         else: flags = 0
..         msg = " ".join(msg.split())
..         errors = []
..         regex = u"[\W^]{}[\W$]"
..         for p in list:
..             for r in p[1]:
..                 for m in re.finditer(regex.format(r), text, flags=flags):
..                     txt = m.group(0).strip()
..                     errors.append((
..                         m.start() + 1 + offset,
..                         m.end() + offset,
..                         err,
..                         msg.format(p[0], txt),
..                         p[0]))
..         errors = truncate_to_max(errors, max_errors)
..         return errors


..     def existence_check(text, list, err, msg, ignore_case=True,
..                         str=False, max_errors=float("inf"), offset=0,
..                         require_padding=True, dotall=False,
..                         excluded_topics=None, join=False):
..         """Build a checker that blacklists certain words."""
..         flags = 0
..         msg = " ".join(msg.split())
..         if ignore_case: flags = flags | re.IGNORECASE
..         if str: flags = flags | re.UNICODE
..         if dotall: flags = flags | re.DOTALL
..         if require_padding: regex = u"(?:^|\W){}[\W$]"
..         else: regex = u"{}"
..         errors = []
..         if excluded_topics:
..             tps = topics(text)
..             if any([t in excluded_topics for t in tps]):
..                 return errors
..         rx = "|".join(regex.format(w) for w in list)
..         for m in re.finditer(rx, text, flags=flags):
..             txt = m.group(0).strip()
..             errors.append((
..                 m.start() + 1 + offset,
..                 m.end() + offset,
..                 err,
..                 msg.format(txt),
..                 None))
..         errors = truncate_to_max(errors, max_errors)
..         return errors

:sc:`Memoization`
^^^^^^^^^^^^^^^^^

One of our goals is for Proselint to be efficient, able to run over a document in real time as an author writes it. To achieve this goal, it is helpful to avoid redundant computation by storing the results of expensive function calls from one run of the linter to the next, a technique called memoization. For example, consider that many of Proselint's checks can operate at the level of a paragraph, and most paragraphs do not change when a sizeable document is being edited --- at the extreme, where the linter is run after each keystroke, this is true by definition. By running checks over paragraphs, and recomputing only when the paragraph has changed, otherwise returning the memoized result, it is possible to reduce the total amount of computation and thus improve the linter's running time.

Concerns around normativity in prose styling
============================================

One of the most common `critiques <https://news.ycombinator.com/item?id=11232882>`_ of Proselint is a concern that introducing any kind of linter-like process to the act of writing prose would in some way diminish the ability for authors to express themselves creatively.
These arguments suggest that authors will find themselves limited in the set of things that are consistent with the linter's rules, and as a result that this will have a shaping or homogenising effect on prose.
There are many nuances around how exactly this is stated, but that general gist covers the core of the critique. 

To this critique there are several possible responses.
The first few responses apply in general, the latter apply in the case of technical and scientific writing.

A good deal of the advice in Proselint points out that certain word sequences are problematic without suggesting any particular replacement text. 
There are a few reasons for this (including the computational natures of error-detection vs. solution-recommendation problems). 
The reason most relevant to this concern is that solution-recommendations are more likely to produce a homogenizing effect because they have a driving effect, wherein using a particular set of words is deemed superior to another set of words. 
Much in the way that the diversity of life-forms has arisen because of selective pressures, by eliminating the least fit combinations of words, the native variation in writing can flourish all the more readily.

The goal is not to homogenize text for the sake of uniformity, but rather to identify those cases that have been identified by respected authors and usage guides as being specifically problematic. 
Any text that is sufficiently artful and compelling to have not been specifically addressed by these sources should not be able to be caught by the linter.
Novelty will continue to introduce new usages, and some of them will be poor. 
Authors identified as trustworthy may point these out, but this will only be in retrospect. 
If one does not trust a guide's point of view, our strongest recommendation would be to turn off the modules associated with that guide.

Technical writing of all kinds is often characterised by consistent language use and precise terminology. Even if one views all writing as a inextricably creative endeavor, that creativity – in some cases – needs to be directed toward particular aims. Software documentation, technical manuals, legal and pedagogical writing all feature this need. The needs of each of these cases will not be well addressed by the same set of guidelines, but each will have a guideline it is intended to follow.

Science demands consistency in order to ensure that replication and clarity is possible. At the same time, scientists are in the business of expressing ideas that challenge even the greatest of minds. Their success depends upon their ability to accessibly and captivatingly convey worthwhile ideas that people wish to use in their own work. In cases where the ideas themselves are difficult to grasp, eradicating opacity from prose is tantamount; opacity is the enemy of the proliferation of any idea.

And, as a final point, we can do little better than to give a modified quote from the Foreword [#]_ in Robert Bringhurst's The Elements of Typographic Style (version 3.2, 2004)

    [Language usage] thrives as a shared concern — and there are no paths at all where there are no shared desires and directions. A [language user] determined to forge new routes must move, like other solitary travellers, through uninhabited country and against the grain of the land, crossing common thoroughfares in the silence before dawn. The subject… is not [stylistic] solitude, but the old, well-travelled roads at the core of the tradition: paths that each of us is free to follow or not, and to enter and leave when we choose — if only we know the paths are there and have a sense of where the lead. That freedom is denied us if the tradition is concealed or left for dead. Originality is everywhere, but much originality is blocked if the way back to earlier discoveries is cut or overgrown.

    -- Robert Bringhurst :cite:`bringhurst2004elements`


.. [#] Only because we are on the topic of historical traditions and stylistic guides, it should be mentioned that a foreword – according to book design tradition – would be written by an individual other than the author about the author, the book, and usually the relation between them. In this case, the section in Bringhurst's masterpiece labelled "Foreword" would likely be better described as "Preface" or "Introduction". Given his knowledge of book design, I shall assume that this was a conscious departure from the road of tradition, even if I cannot appreciate the new view that it offers.


Future
======
We see a number of directions for future development. 

Scalable, dynamic false-positive detection
------------------------------------------

The key feature to Proselint's success are its low false positive rates. 
However, to identify the rate, we first must identify whether a flag is a false or true positive.
Currently, detecting false positives requires an author manually evaluating the output of each linting flag.
This does not scale to even small documents sets.
The problem is made worse when you consider that each time the linter is run this process would need to be repeated. 

To address dynamic documents, it would be useful to have the ability to detect when an error that has already been flagged.
Until this is addressed a false positive analysis will only be efficient when done over static corpora of documents. 
Adding this ability would also allow people to turn off an instance of a flag in a persistent manner.

We are investigating mechanisms for allowing for scalable dynamic false positive detection.
One mechanism is to divide this task into independent isolable chunks. 
This combined with a process for rapidly evaluating those chunks will make checking for false positives much easier even on an individual level.
It also would open the door to load distribution mechanisms (such as crowd sourcing) as a way to take the burden of evaluation off of the author.

This would require solving some decision theoretic problems in order to efficiently sample the false positive rate as it applies particular linting flags or even entire rules.
If this can be accomplished and automated, we could easily estimate the false positives found in a paper or a corpus.  
More generally, we could build even richer versions of the generalised lintscore metric based not only on the similarity of a document to a corpus, but on the identity of the rules themselves.

Prosewash: False positive elimination as a service
--------------------------------------------------

Any sort of load distribution mechanism will likely require some amount of human-time being devoted to the task of identifying whether particular flagged text is a false positive.
Expecting people to donate their time will only create a backlog in this mechanism if it experiences even moderate demand.
Thus, we may need to pay people to evaluate flags as false or true positives. 
That, then, requires paying for the cost of crowdsourcing, which opens the door for a sustainable business model for supporting Proselint, without abandoning any of our open source principles.
That is, we can successfully support our open source development efforts through a separate premium service model.


We will provide individuals the ability to reduce false positive rates by connecting them to other individuals who will evaluate their prose.
To pay for the costs of development, maintenance, and the crowd's time this will necessarily be a paid service, especially so for any solution that is intended to scale up to larger cases.
A traditional clothing "linter" relies on the static properties of the linter to extract lint making the clothes cleaner.
In analogy to this active evaluation process in contrast to the static linting process, we call the service Prosewash.

One advantage of this kind of business model is that it avoids some of the pitfalls that can face an open source project's attempt to support itself.
One pitfall is to take open source software and close off future development in order to extract rent from those advances.
This approach respects the extant contributors to the project and the Proselint community by keeping the tool and its source open.
Another pitfall is to develop features in software that could be given to everyone for free (in terms of the actual cost of distributing the feature), but are withheld from users who do not pay.
Our approach respects the users and contributors by not building a premium programme and then hiding its capabilities from users.
This would be a service not a feature; every time we recruit a crowd to solve a problem it will cost money.
There is no way to provide that service without incurring costs, so we are not withholding any capabilities from users of Proselint.

This also offers the advantage that in the course of running the service, we are collecting more and more data about Proselint in the wild.
We can learn the base-rates at which different rules are invoked as well as their specific false positive rates.
As we introduce more contextual information (and thus riskier rules), this data will be invaluable to effectively tune our rule-set.
So while this financially supporting further development on Proselint, that is not the only way Prosewash improve Proselint. 
The data gathered through the process of washing people's prose more actively, can then be fed back to improve Proselint and tune its rulesets and defaults. 
Thus participation in the premium service will provide direct improvements to the Proselint community irrespective of assigned development time.

Context sensitive rule application
----------------------------------

Many rules may apply better to some kinds of documents than others. For example, in most cases "extendible" will be conventionally preferable to "extensible"; in software development the opposite is likely to be the case. Applying these rules without consideration of the document context will introduce false positives in a systematic fashion. We have often avoided those rules, as they guarantee an increase in the number of false positives. 

If we detect the context in which a rule is to be applied (such as document topic, format or genre), we can predict whether a rule should be silenced. This allows including a greater variety of rules without introducing false positives. One example of this in practice is our "50's" detector, which identifies whether a document's topic includes the artist "50 cent". Were the topic not detected we would identify "50's" as a improperly giving a decade an apostrophe, if the "50 cent" topic is detected the rule is silenced.

Generalizing this ability will be crucial to safely growing Proselint error coverage. 
In the sense that a riskier rule is one with a higher false-positive rate, context sensitive rules are necessarily riskier than non-context sensitive rules.
To see why, consider that if a rule introduced many false positives across all contexts it would not be included in Proselint.
For rules that do not produce many false positives across contexts, there is no reason to make them context specific.
The only reason to include context specific rule applications is if there are some contexts in which a rule produces higher false-positive rates than in other contexts.
If those false-positive rates were low enough to not be excluded by the context insensitive version, their net false positive rate would only be lower, meaning it would certainly be included in the basic Proselint rule set (excluding it from candidacy as a context sensitive rule).
Accordingly, introducing a rule that *should* be context sensitive, but without the appropriate context sensitivity, will guarantee an increased false positive rate.


Improved self-evaluation procedure
----------------------------------

We currently calculate our lintscore manually on a static corpus of professionally edited documents. This process can be improved in a number of ways that will lead to different kinds of improvement in Proselint.  

:sc:`Multiple corpora with different features`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We currently only have a single corpus for analyzing Proselint's performance. 
It is composed of documents that have already been professionally edited, which we assume will have relatively few true errors. 
This efficiently alerts us to false-alarms that are introduced by the inclusion of new rules. 
However, it does a poor job of estimating performance on a variety of other metrics.

A corpus of relatively green documents are more likely to have true positives and (consequently) will improve our estimates of Proselint's positive utility. 

Corpora of documents drawn from different content-based categories (technical papers, scientific articles, software documentation, fiction, journalism, &c.) will allow us to distinguish between Proselint's performance in evaluating these different subfields. 
Given that certain rules could systematically be relevant to different fields or differentially successful on certain document types, this would allow us to ensure that Proselint can be used by the widest possible group of individuals. This also will allow us to know how to assign rulesets to different contexts.

Different document formats (e.g, ``.rst``, ``.tex``, ``.md``, ``.html``, &c.) often rely on syntactical conventions that Proselint systematically, falsely identifies as errors. Similar concerns arise for documentation written as docstrings or code comments in a variety of programming languages. Corpora focusing on individual formats and languages will aid in identifying these errors and allow targeted development to address these problems.

:sc:`Automating the evaluation process`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Currently the analysis procedure requires a particular individual evaluating the proposed errors and determining whether they are true or false positives.
Using some kind of load distribution mechanism (e.g., crowd sourcing) would make this easier. 

Additionally, there is no extant format for annotating the output of Proselint with true and false positive identities.
There are straightforward ways of doing this (e.g., adding a field to the ``json`` structure) but doing that will require reanalyzing the entirety of a document every time it changes.
While such a solution is workable, it would be good to have a way to track particular errors if the text has not changed (even if the line-number has) so that evaluations can transfer between different instances of the same living document.

Authorship attribution, ghost-writing, and anonymisation
--------------------------------------------------------

Stylometrics has extensively studied the problem of identifying the true authors of documents. 
Many of these studies focus on the relative frequencies with which individual words are used (especially function words).
For example, on the basis of the frequency of function words such as "to" and "by", Mosteller and Wallace :cite:`mosteller1963inference` inferred the authorship of twelve essays in the *Federalist Papers*.
Proselint provides new measures that could be used to improve this kind of stylometric analysis. 

One application improved authorship identification is the ability to detect ghost-written documents (assuming you have a ground corpus to identify stylometric patterns in the author's writing). This could have applications to identifying academic dishonesty (e.g., purchasing and selling of ghost-written essays). 

On the other hand, someone who applies Proselint to their text may be able to escape identification even by a group who has access to that a ground corpus by the author. In cases where anonymity is desired, Proselint can act as a tool to erase the author of a text.

Subdocument analysis
--------------------

Currently rule scope needs to be done at a word, sentence, paragraph or document level. 
Some rules may be better applied over different subdocument sections. 
For example, while an author may not overuse a sentential construction throughout a document, if a particular construction was used repeatedly throughout one section it would still be problematic.
Without subdocument level analyses, it would not be possible to detect stylistic errors of that sort.

The central challenges to this are the combinatoric issues that this problem introduces if approached naïvely and the inferential problems that could allow proper scaling. 
If one simply looked at all possible subsequences of characters, there is no way the method could scale appropriately with larger documents. 
The number of potential subsections that would need to be analysed would grow faster than could be kept up with by even the fastest of today's computers.
On the other hand inferring the structure of a document based on its content if that structure is not of a pre-specified variety is not a solved problem.


.. Including rules set to be off by default. One reason to have rules off by default but included might be because of their effect on the false positive rate.

.. Prosewash
.. ---------
.. Next steps: more intense processing with riskier rules
.. False positive checking with crowd sourcing
.. Feeds back to improve Proselint
.. 

.. Isolable 



Acknowledgements
================
Work on Proselint was supported in part by the `Berkeley Center for Technology, Society and Policy`__ through the CTSP Fellows program, specifically as regards applying Proselint to the problem of improving governmental communications as required the by `Federal Plain Language Guidelines`__.

.. __: https://ctsp.berkeley.edu/

.. __: http://www.plainlanguage.gov/howto/guidelines/FederalPLGuidelines
