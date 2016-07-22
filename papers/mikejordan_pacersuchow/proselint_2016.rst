:author: Michael D. Pacer
:email: mpacer@berkeley.edu
:institution: University of California, Berkeley

:author: Jordan W. Suchow
:institution: University of California, Berkeley

:bibliography: mybib

========================================================================
Proselint: the linting of science prose and the science of linting prose
========================================================================

.. class:: abstract

   Writing is notoriously hard, even for the best writers, and it's not for lack of good advice — a tremendous amount of knowledge about the craft is strewn across usage guides, dictionaries, technical manuals, essays, pamphlets, websites, and the hearts and minds of great authors and editors. But much of this knowledge is trapped, waiting to be extracted and transformed.

   We built Proselint, a Python-based linter for prose that identifies violations of style and usage guidelines. Proselint is open-source software released under the BSD license and is compatible with Pythons 2 and 3. It runs as a command-line utility or as a text-editor plugin. Proselint's modules address redundancy, jargon, illogic, clichés, unidiomatic vocabulary, sexism, inconsistency, misuse of symbols, malapropisms, oxymorons, security gaffes, hedging, apologizing, and pretension. Furthermore, Proselint is extensible, enabling creation of domain-specific modules or implementation of house style guides.

   Proselint can be seen as both a language tool for scientists and a tool for language science. On the one hand, it can help scientists communicate their ideas to each other and to the public by promoting clear and consistent prose. On the other hand, scientists can use Proselint to measure language usage, to provide style- and usage-based features for tasks such as authorship identification, and to explore the factors that make a linter useful (e.g., low false-positive rate).

.. class:: keywords

   linters, writing tools, copyediting

The problem
===========

Writing is notoriously hard, even for the best writers, and it's not for lack of good advice — a tremendous amount of knowledge about the craft is strewn across usage guides, dictionaries, technical manuals, essays, pamphlets, websites, and the hearts and minds of great authors and editors. Consider, for example, *Garner's Modern English Usage*, an authoritative usage guide with 11,000 entries covering a broad range of advice that, when followed, helps writers produce clear and idiomatic prose :cite:`garner2016garner`. Or consider the *Federal Plain Language Guidelines*, a guide created by employees of the U.S. federal government to promote writing that is clear, concise, and well-organized :cite:`Plain2011`. Professional conferences such as the annual meeting of the American Copy Editors Society are dedicated to sharing knowledge about editing prose. And within the academy, organizations such as the American Psychological Association publish manuals whose guidance on style has been adopted as a standard :cite:`american1994publication`.

Advice on writing touches upon everything from superficial conventions to the deepest reflections of our society and its attitudes. Take, for example, advice concerning the preferred forms of words such as "connote" (vs. "connotate"), which may help to prune needless variants in spelling, but are unlikely to affect the reader's understanding of the text and its author. Compare this to advice concerning needlessly gendered language ("woman scientist", "policeman"), which by being commonplace in language may perpetuate social inequality :cite:`Philips2004`.

Amassing a pile of advice is not enough to make writing better. This is because advice, though it may be principled, thoughtful, and worth following, is hard to apply in new settings once it has been learned :cite:`Argote2000`. Thus even if an author could absorb all the knowledge contained in extant sources of advice on writing, the author would still face the problem of recalling and systematically applying that knowledge during the acts of writing and editing. Furthermore, developing a new habit (linguistic or otherwise) is slow, costly, and effortful :cite:`Fogg2010`, causing errors to appear even though, in some sense, the author knows the rules.

Today, an author who wishes to improve a piece of writing by applying the collective wisdom of experts must rely on indirect means. The most common approach, used extensively in publishing, is a division of labor whereby dedicated staff with deep knowledge of best practices in writing copyedit a piece to their satisfaction. For example, *The New Yorker* uses an editing team that includes fact checkers, editors, grammarians, and others :cite:`Norris2009`. Another approach, used extensively in desktop publishing, is to use software-based tools such as spelling and grammar checkers that mark unrecognized words and purported violations of grammatical rules.

Neither approach fully solves the problem of successful adoption of best practices in writing. Few people have the resources needed to outsource  editing, and for those who do, editing by external staff is slow. Copy editors must read the text carefully and are normally unavailable during the act of writing. By the time an editor's notes are received, then, an opportunity to strengthen the writer's craft has passed. Time-sensitive writing exacerbates this problem, where the delay introduced by the editor may diminish the communication's value. In contrast, software-based tools, though they are inexpensive and fast, are typically incomplete, imprecise, or inaccessible (see Existing Tools, below).

Much of our collective knowledge about best practices in writing is thus essentially trapped, waiting to be extracted and transformed into a medium that makes the knowledge immediately accessible to all authors.

The solution
============

To solve this problem, we built Proselint, a real-time linter for English prose. A linter is a computer program that, like a spell checker, scans through a document and analyzes it, identifying problems with its syntax or style :cite:`Johnson1977`. Proselint identifies violations of expert-endorsed style and usage guidelines [#]_  and gently alerts the writer of those violations as they are committed, an ideal opportunity to elicit long-term changes in behavior :cite:`ferster1957schedules`. In doing so, Proselint gives the experts a voice while teaching at a speed and scale unreachable by humans.

.. [#] Proselint differs from a spell-checker in that its recommendations do not specifically counter spelling errors, but rather errors of style and usage, though the two occasionally overlap. For example, consider the malapropism "attacking your voracity", where it is not that "voracity" is a spelling error per se but that the appropriate word is its phonetic neighbor "veracity". Compare this to "attacking your verqcity", almost certainly a typo.

Proselint is open-source software released under the BSD license and compatible with Pythons 2 and 3. It runs as a command-line utility or editor plugin for Sublime Text, Atom, Emacs, vim, etc. It outputs advice in JSON and the standard linting format (:math:`\textsc{SLF}`), promoting integration with external services :cite:`wasserman1990tool` and providing human-readable output. Proselint includes modules on a variety of usage problems, including redundancy, jargon, illogic, clichés, sexism, misspelling, inconsistency, misuse of symbols, malapropisms, oxymorons, security gaffes, hedging, apologizing, pretension, and more (see Tables 1 and 2 for a fuller listing).

Proselint is both a language tool for scientists and a tool for language science. On the one hand, it can help scientists communicate their ideas to each other and to the public by promoting clear and consistent prose. On the other hand, scientists can use Proselint to studying language and linting.

A language tool for scientists
------------------------------

Scientists use the written word to communicate science to each other and to the public. Proselint improves writing across a number of dimensions relevant to science communication, including consistency in terminology & typography, concision, and elimination of redundancy. For example, Proselint detects the letter x used in place of the multiplication symbol × (e.g., 1440 x 900), misspecified *p* values resulting from data-analysis software that truncates small numbers (e.g., *p* = 0.00), and colloquialisms that obscure the mechanisms of science-based technology (e.g., "lie detector test" for the polygraph machine, which measures arousal, not lying per se).

A tool for language science
---------------------------

Linguistics is largely descriptivist, tending to describe language as it is used rather than prescribe how it ought to be used :cite:`garner2016garner`. Errors are considered mostly in the context of language learning (especially children's) because those errors reveal the structure of the language learning mechanism (see, e.g., overregularization by young English speakers :cite:`marcus1992overregularization`). Though linting prose is implicitly prescriptivist because its detection of norm violations presupposes the existence of norms :cite:`garner2016garner`, even so, language science can benefit from Proselint's advice without making normative claims. For example, linguists can use Proselint to detect patterns of usage and style in corpora of written text, for authorship identification, and as input to standard Natural Language Processing (:math:`\textsc{nlp}`) techniques in place of the more typical word frequencies and syntactic structures :cite:`Bird:2009:NLP`.

The advice
==========

Proselint is built around advice derived from works by Bryan Garner, David Foster Wallace, Chuck Palahniuk, Steve Pinker, Mary Norris, Mark Twain, Elmore Leonard, George Orwell, Matthew Butterick, William Strunk, E.B. White, Philip Corbett, Ernest Gowers, and the editorial staff of the world’s finest literary magazines and newspapers, among others. [#]_ 

.. [#] Proselint has not been endorsed by these individuals; we have merely implemented their words in code.

Our standard for including a new rule is that it should be accompanied by an appropriate citation from a recognized expert on language usage. Though we have no explicit criteria for what makes a citation appropriate, we have, in practice, given greater weight to works from well-established publishers and those widely cited as reliable sources of advice. The choice of which rules to implement is ultimately a question of feasibility of implementation, utility, and preference, and our guiding preference is to make Proselint widely useful by default. Though it has not arisen, in the case of unresolved conflicts between advice from multiple sources, our default is to exclude all forms of the advice, under the logic that it is unreasonable to hold users to a higher standard than we do the experts, at least one of whom has endorsed the user's choice. Because we aim to have excellent defaults without hampering customizability, Proselint can be extended by adding new rules or filtered by excluding existing rules through a configuration file.

Tables 1 and 2 list much of the advice that Proselint currently implements; that advice is organized into modules.

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
   |``cliches.misc``                 | Avoiding clichés                            |
   +---------------------------------+---------------------------------------------+
   |``consistency.spacing``          | Consistent sentence spacing                 |
   +---------------------------------+---------------------------------------------+
   |``consistency.spelling``         | Consistent spelling                         |
   +---------------------------------+---------------------------------------------+
   |``corporate_speak.misc``         | Avoiding corporate buzzwords                |
   +---------------------------------+---------------------------------------------+
   |``cursing.filth``                | Avoiding cursing                            |
   +---------------------------------+---------------------------------------------+
   |``cursing.nfl``                  | Avoiding words banned by the NFL            |
   +---------------------------------+---------------------------------------------+
   |``dates_times.am_pm``            | Using the right form for time               |
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
   |``misc.but``                     | Avoiding starting a paragraph with "But..." |
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

.. table:: What Proselint checks (cont.). :label:`checkscont`

   +---------------------------------+---------------------------------------------+
   | ID                              | Description                                 |
   +=================================+=============================================+
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
   |``terms.eponymous_adjs``         | Calling people by the right name            |
   +---------------------------------+---------------------------------------------+
   |``terms.venery``                 | Call groups of animals by the right name    |
   +---------------------------------+---------------------------------------------+
   |``typography.diacritics``        | Using dïacríticâl marks                     |
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

Rule modules
------------

Proselint rules are organized into modules that reflect the structure of usage guides :cite:`garner2016garner`. For example, Proselint includes a module ``terms`` that encourages expressive vocabulary by flagging use of unidiomatic and generic terms, with submodules for categories of terms found as entries in usage guides. For example, one such submodule, ``terms.venery``, pertains to *venery terms*, which arose from hunting tradition and describe groups of animals of a particular species — a *pride* of lions or an *unkindness* of ravens. Another such submodule, ``terms.denizen_labels``, pertains to *demonyms*, which are used to describe people from a particular place — *New Yorkers* (New York), *Mancunians* (Manchester), or *Novocastrians* (Newcastle).

Organizing rules into modules is useful for two reasons. First, it allows for a logical grouping of similar rules, which often require similar computational machinery to implement. Second, it allows users to include and exclude rules at a higher level of abstraction than an individual word or phrase.

Converting a rule to code: rule templates
-----------------------------------------

Suppose you wanted to implement the following usage-guide entry as a rule in Proselint:

  :math:`\footnotesize\textsc{DECIMATE}`. Originally this word meant “to kill one in every ten,” but this etymological sense, because it’s so uncommon, has been abandoned except in historical contexts. Now *decimate* generally means “to cause great loss of life; to destroy a large part of.” ... In fact, though, the word might justifiably be considered a :math:`\footnotesize\textsc{SKUNKED TERM}`. Whether you stick to the original one-in-ten meaning or use the extended sense, the word is infected with ambiguity. And some of your readers will probably be puzzled or bothered. :cite:`garner2016garner`. 

In general, a rule's implementation need only be a function that takes in a string of text, applies logic identifying whether the rule has been violated, and then returns a value identifying the violation in the correct format. The weakness of these requirements, paired with Python's expressiveness, allows developers to build detectors for all computable usage and style requirements. However, it provides little guidance when implementing new rules.

To ease implementation of new rules, we wrote functions that help to follow the protocol and that provide common logical forms of rules. These include checking for the existence of a given word, phrase, or pattern (``existence_check()``), for intra-document consistency in usage (``consistency_check()``), and for use of a word's preferred form (``preferred_forms_check()``).

The entry on *decimate* bans a word and so can be implemented using the ``existence_check`` template:

.. code-block:: python
    :linenos:
    
    def check_for_decimate(text):
        err = "skunked_terms.decimate"
        msg = (u"'{}' is a skunked term — impossible to 
               "use without someone taking issue. Find" 
               "another way to say it")
        regex = "decimat(?:e|es|ed|ing)?"
        return existence_check(
            text, [regex], err, msg, join=True)

The function first defines an error code, an error message, and a regualar expression that matches the word *decimate* in its various forms, then applies the existence check.

Using Proselint
===============

Installation
------------
Proselint is available on the Python Package Index and can be installed using pip:

.. code-block:: bash

   pip install proselint

Alternatively, developers can retrieve the Git repository from GitHub (`https://github.com/amperser/Proselint <https://github.com/amperser/Proselint>`_) and then install the software using setuptools: 

.. code-block:: bash

   pip install --editable


Command-line utility
--------------------

Proselint is a command-line utility that reads in a text file:

.. code-block:: bash

   proselint text.md

Running this command prints a list of suggestions to stdout, one per line. The GNU Error Message Formatting standard :cite:`stallman2016gnu` is the basis  for the format of displaying these suggestions. Like many other linters, we  further require that the error code (here, the ``check_name``) should be separated from the error message by a space. Because this format is used by many linters, we call it the Standard Linting Format (:math:`\textsc{slf}`). An :math:`\textsc{SLF}`-formatted suggestion has the form:

.. code-block:: bash

   text.md:<line>:<column>: <check_name> <message>

For example,

.. code-block:: bash

  text.md:0:10: skunked_terms.misc 'decimate' is ...
  a skunked term — impossible to use without ...
  someone taking issue. Find another way to say it."

This message suggests that, at column 10 of line 0, the module ``skunked_terms.misc`` detected the presence of the skunked term *decimate*. The command-line utility can instead print the list of suggestions in JSON through the ``--json`` flag. In this case, the output is considerably richer:

.. code-block:: javascript

  {
      // The check originating this suggestion
      "check": "uncomparables.misc", 
      
      // The line where the error starts
      "line": 1, 

      //The column where the error starts
      "column": 1, 
      
      // Index in the text where the error starts
      "start": 1,

      // the index in the text where the error ends
      "end": 18, 
      
      // start - end
      "extent": 17, 
      
      // Message describing the advice
      "message": "Comparison of an uncomparable: ...
      'very unique\n' is not comparable.",
      
      // Possible replacements
      "replacements": null, 

      // Importance("suggestion", "warning", "error")
      "severity": "warning"
  }

Text editor plugins
-------------------
Proselint is available as a plugin for popular text editors, including Emacs, vim, Sublime Text, and Atom. Embedding linters within the tools that people already use to write removes a barrier to adoption the linter and thereby promotes adoption of best practices in writing.

A proof of concept
==================

As a proof of concept, we used Proselint to make contributions to several documents. These include the White House's `Federal Source Code Policy <https://github.com/WhiteHouse/source-code-policy>`_; `The Open Logic Project <https://github.com/OpenLogicProject/OpenLogic>`_, a textbook on advanced logic; Infoactive's `Data + Design book <https://github.com/infoactive/data-design>`_; and many of the other papers that were submitted for potential contribution to `SciPy 2016 <https://github.com/scipy-conference/scipy_proceedings/tree/2016>`_. In addition, to evaluate Proselint's false-positive rate, we developed a corpus of essays from well-edited magazines such as *Harper's Magazine*, *The New Yorker*, and *The Atlantic* (`full list <https://github.com/amperser/proselint/tree/master/corpora>`_). We then measured the lintscore, defined below. Because the essays included in our corpus were edited by a team of experts, we expect Proselint to remain mostly silent, commenting only on the rare error that slips through unnoticed by the editors or, more commonly, on finer points of usage, about which the experts sometimes disagree. When run over v0.1.0 of our corpus, we achieved a lintscore (*k* = 2) of 98.8.

The theory behind Proselint
===========================

What to check: usage, not grammar
---------------------------------

Proselint does not detect grammatical errors, which is both too easy and too hard:

Detecting grammatical errors is too easy in the sense that, for most native speakers, they are readily identified, if not easily fixed. The errors that leave the greatest negative impression in the reader's mind are often glaring to native speaker. (On the other hand, more subtle errors, such as a disagreement in number set apart by a long string of intermediary text, escapes even a native speaker's notice.)

Detecting grammatical errors is too hard in the sense that, in its most general form, it is AI-hard, requiring at least human-level artificial intelligence and a native speaker's ear. 

Modern :math:`\textsc{nlp}` techniques that detect grammatical errors are unavoidably statistical :cite:`Bird:2009:NLP` :cite:`leacock2010automated` and produce many false positives. This is in part because syntax parsers used in grammatical error detection must tolerate grammatical errors, a problem that is compounded in writing by English-language learners :cite:`leacock2010automated`. Once a grammatical error has been detected, determining the correct replacement hinges on the intended meaning. Occasionally, the intended meaning will determine even *whether* a grammatical error is present: e.g., is "Man bites dog" a headline about canine aggression, or are the subject and object swapped in error?

Instead of focusing on grammatical errors, Proselint addresses errors of usage and style, including redundancy, jargon, illogic, clichés, sexism, inconsistency, misuse of symbols, malapropisms, oxymorons, security gaffes, hedging, apologizing, pretension, and more.

Published expertise as primary sources
--------------------------------------

People have strong shared intuitions about grammar – so much so that a common experimental measure in linguistics is the grammaticality of a sentence as measured by the intuitions of native speakers :cite:`keller2000gradience`. But style and usage inspire a multitude of intuitions. Authors of usage guides have done much of the work of hashing out these conflicting intuitions to arrive at sensible everyday advice :cite:`garner2016garner`. Proselint thus defers to them, and in doing so provides access to our collective understanding about the craft of writing with style.

Levels of difficulty
--------------------

In a loose analogy to the Chomskian hierarchy of formal grammars :cite:`chomsky1956three`, usage errors differ in the level of difficulty in detecting and correcting them:

#. AI-hard
#. :math:`\textsc{nlp}`, beyond state-of-the-art
#. :math:`\textsc{nlp}`, state-of-the-art
#. Syntax-dependent rules
#. Regular expressions
#. One-to-one replacement rules. 

At the lowest levels of the hierarchy are usage errors that a linter can reliably detect and correct through one-to-one replacement rules. At the highest levels are usage errors whose detection and correction are such hard computational problems that it would require at least human-level intelligence to solve in the general case, if a solution is possible at all. Consider, for example, usage errors pertaining to placement of the word "only", which depends on the intended meaning. For example, in "John hit Peter in his only nose", is the "only" misplaced or is it unusual that Peter has only one nose? Usage errors at this highest level of the hierarchy are hard to identify without introducing false positives and determining the correct replacement requires understanding the intended meaning. Development of Proselint begins at the lowest levels of the hierarchy and builds upwards.

Signal detection theory and the lintscore
-----------------------------------------

Any new tool, for language or otherwise, faces a challenge to its adoption: it must demonstrate that the utility provided by the tool outweighs the cost of learning to use it :cite:`wasserman1990tool`. Pen & ink, paper, and the computer each enabled new modes of communication and, in doing so, provided obvious value. In contrast, tools that merely improve existing capabilities must demonstrate a substantial improvement over the status quo.

Because of their need to demonstrate utility, earlier language tools attempted to offer as much help as possible. Each issue flagged might be an error, but it might instead be a false positive. Let :math:`T` be the number of true errors, and :math:`F` be the number of false positives, thus making :math:`T+F` the total number of flags raised by the tool. Their approach attempts to maximize :math:`T` by flagging as many errors as possible, without considering :math:`F`. The tools identify many genuine errors but raise so many false positives that their advice cannot be trusted because writers must evaluate each proposed error.

With Proselint, we aim for a tool so precise that it becomes possible to unquestioningly adopt its recommendations and still come out ahead, reasoning that it is better to be quiet and authoritative than loud and unreliable. To achieve this, we penalize the number of false positives :math:`F` by evaluating Proselint in terms of its *empirical lintscore*. The lintscore gives one point for every true positive :math:`T` and penalizes on the basis of the false-positive rate :math:`\alpha = \frac{F}{T+F}`. The lintscore is given by

.. math::
    l(T,F;k) = T(1-\alpha)^k,

where the parameter :math:`k` controls the strength of the :math:`1-\alpha` penalty.

We can estimate a lintscore for documents with unknown empirical false-positive rates using a straightforward probabilistic model that assigns credit only in the best-case scenario, where every error is a true positive. This probabilistic model treats each identified error as an independent identically distributed Bernoulli random variable. We suppose that each flag produces a false positive with probability equal to the empirical false-positive rate estimated from a known corpus of related documents, :math:`\hat{\alpha}=\frac{\hat{F}}{\hat{T}+\hat{F}}`. For :math:`N` flags, the probability that every flag is correct is :math:`(1-\hat{\alpha})^N`. If we receive 0 points in all but the best case (where we receive :math:`T\equiv N` points), the expected score is :math:`N(1-\hat{\alpha})^N`. This *generalized lintscore* has the same form as an empirical lintscore, but with :math:`\hat{\alpha}` as an estimated :math:`\alpha` and :math:`k` as the maximal number of successes :math:`k\equiv N`. The choice of reference corpus is a free parameter.

Note that the lintscore is not a readability metrics because it evaluates linters, not prose. Given a set of documents, signal detection theory makes it possible to estimate a linters' trustworthiness through the lintscore.

Speed via Memoization
---------------------

Proselint must be efficient for use as a real-time linter. Avoiding redundant computation by storing the results of expensive function calls ("memoization") improves efficiency. Consider, for example, that most paragraphs do not change from moment to moment during editing of a sizable document. Memoizing Proselint's output over paragraphs and recomputing only when a paragraph has changed (otherwise returning the memoized result) reduces the total amount of computation and thus improves the running time.

Existing tools
==============

We have curated a list of known tools for automated language checking, stored within the Proselint repository. The dataset contains the name of each tool, a link to its website, and data about its basic features, including languages and licenses (`link <github.com/amperser/proselint>`_). The tools are varied in their approaches and coverage, but tend to focus on grammar versus usage and style, are often closed source, and rarely extensible. The greatest difference from Proselint arises from a willingness to sacrifice coverage to maintain user trust through low false-positive rates.

Future development and possible applications
============================================

We see a number of directions for future development of Proselint that improve the tool and its utility for science:

Context-sensitive rule application and machine learning
-------------------------------------------------------

Many rules apply better to some kinds of documents than to others. For example, in most cases "extendable" is preferable to "extensible", but in software development the opposite is true. Applying these rules without consideration of the context will systematically introduce false positives.

Silencing rules that are predicted to be irrelevant because of the context allows a greater variety of rules to be included without introducing false positives. For example, consider the advice that, when specifying a decade, an apostrophe is unecessary: Eisenhower was president in the 50s, not the 50's. However, not all instances of "50's" are problematic. Consider, for example, the posessive form of the musical artist 50 Cent. One can validly write "50's manager" to refer to 50's manager without having made a usage error about decades. To account for this context sensitivity, Proselint detects whether a document's topic is 50 Cent, identifying "50's" as a usage error only when the topic is not detected.

The 50 Cent topic detector was hand-crafted in the fashion of expert knowledge systems research :cite:`jackson1986introduction`. Generalizing this ability will be crucial to safely growing Proselint's coverage of usage errors. Machine learning techniques for identifying the topic (or mixture of topics) that apply at any point in a document (e.g., topic models :cite:`blei2009topic`) will be needed. Once incorporated, generalizing this to hierarchical, nonparametric topic models will enable taking document sub-structure into account as a form of context :cite:`blei2010nested`.

Evaluating linters by testing on multiple corpora
-------------------------------------------------

In our internal evaluations of Proselint, we calculate the empirical lintscore manually on a static corpus of professionally edited documents, which we assume will have few errors. This efficiently alerts us to false positives that are introduced by the inclusion of new rules. However, it does a poor job of estimating performance on other metrics. A major improvement would be to compute the lintscore on other corpora, such as student essays. 

A corpus of relatively green documents are more likely to have true positives and, consequently, will improve our estimates of Proselint's positive utility. If these documents are modified in accordance with Proselint's suggestions, it will create new opportunities in the theory of linting. Lintscores are likely to decrease between drafts if advice is accepted and no new errors are introduced, because there will be fewer true positives, but lower lintscores are generally worse. We need new metrics that track Proselint's success in improving documents.

Corpora of documents drawn from different content-based categories (technical papers, scientific articles, software documentation, fiction, journalism, etc.) will allow us to determine Proselint's performance in evaluating these specific fields. Certain rules may be relevant to some fields more than other, and testing with diverse corpora will ensure that Proselint can be used by a diverse range of individuals. Furthemore, this will allow us to learn which rule-sets are relevant in which semantic contexts.

File formats and markup languages for documents (e.g, reStructuredText, LaTeX, Markdown, HTML, etc.) often rely on syntactical conventions that Proselint falsely identifies as errors. Similar concerns arise for documentation written as docstrings or code comments in a variety of programming languages. Corpora focusing on individual formats and languages will aid in identifying and filtering these errors, enabling development targeted at addressing these problems.

Stylometrics and machine learning
---------------------------------

The field of stylometrics has extensively studied the problem of identifying the true authors of documents :cite:`zheng2006framework`. Many of these studies focus on the relative frequencies with which individual words are used, especially function words. For example, on the basis of the frequency of function words such as "to" and "by", Mosteller and Wallace :cite:`mosteller1963inference` inferred the authorship of twelve essays in the *Federalist Papers*. Proselint provides new measures that could be used to improve this kind of stylometric analysis. 

Several applications follow from authorship identification: 

One application uses its ability to detect ghost-written documents, though this assumes that there is a ground-truth corpus with samples of the author's writing. This could have benefit for identifying academic dishonesty (e.g., purchasing and selling of ghost-written essays). On the other hand, someone who applies Proselint to their text may be able to *escape* identification by avoiding features that distinguish the author's writings.

A second application inverts and generalizes the process of identifying authors by selectively introducing, changing, or removing usage choices to obfuscate or encrypt messages. With some modifications and a protocol for establishing usage-based keys, Proselint could become a system for designing content-aware steganographic systems, allowing users to convey hidden messages in their choice of words and styles :cite:`bergmair2006content`. Encryption would require modifying the Proselint infrastructure to identify when more than one acceptable choice exists.

Unlike our current rules, these techniques are fundamentally statistical. Machine-learning techniques for inferring identity from sparse data will be particularly applicable. The errors Proselint finds are rare, and sparse measures pose difficultly for methods like those in :cite:`mosteller1963inference`. Furthermore, this endeavor will benefit from an approach that considers the cross product of authors and topics (in the vein of :cite:`rosen2004author`).

Automated usage and style metrics
---------------------------------

Readability metrics such as the Flesch-Kincaid Grade Level and the Gunning fog index are not defined in a way that captures usage and style, measuring reading ease rather than conventionality :cite:`flesch1948new`. Proselint could be used to create automated metrics for the consistency and stylishness of written language. Such metrics may also find use as part of automated essay-grading tools :cite:`valenti2003overview`.

Tracking historical trends in usage
-----------------------------------

One application of Proselint as a tool for language science is in tracking historical trends in usage. Corpora such as Google Books have been useful for measuring changes in the prevalence of words and phrases over several hundred years. Our tool, in providing a feature set for usage, can be used in a similar way. For example, one might study the prevalence of airlinese (including, e.g., use of "momentarily" to mean "in a moment", as in the phrase "we are taking off momentarily") and its alignment with the rise of that industry.

An unsolved problem: foreign languages
--------------------------------------

We have no immediate plans for extending Proselint to other languages, in part because addressing the problem of linting prose for style and usage errors in English (of both American and British varieties) is challenging enough for a native speaker, and attempting to build a linter for languages in which the creators lack fluency would seem to be an exercise in folly. An open problem, then, is how to extend Proselint to become a universal linter for prose. 

Missing corpora
---------------

To evaluate Proselint's false-positive rate, we built a corpus of text from well-edited magazines believed to contain low rates of usage errors. In the course of assembling this corpus, we discovered a lack of annotated corpora that provide false-positive rates for style and usage violations [#]_. The Proselint testing framework is an excellent opportunity to develop such a corpus. Unfortunately, because our current corpus derives from copyrighted work, it cannot be released as part of open-source software. Developing an open-source corpus of style and usage errors will be necessary if these tools are to be made available for :math:`\textsc{nlp}` research outside internal testing of Proselint.

.. [#] Editor :cite:`editor_compare` has built a corpus which compares the performance of various grammar checkers. Their corpus contains "real-world examples of grammatical mistakes and stylistic problems taken from published sources". A corpus made of errors will maximize true positives, but misestimates false-positive rates in real-world documents. Their corpus is not publicly available, and they do not provide a standard format for describing corpora annotated with false positives and negatives.

A critique of normativity in prose styling, and a response
==========================================================

One critique of Proselint :cite:`hackernews2016` is a concern that introducing any kind of linter-like process to the act of writing diminishes the ability for authors to express themselves creatively. These arguments suggest that authors will find themselves limited by the linter's rules and that, as a result, this will have a shaping or homogenizing effect on language.

In response to this critique, we note that our goal is not to homogenize text for the sake of uniformity (though perhaps there is value there, too), but rather to detect instances of language use that have been identified by experts as problematic. Creative use of language is not flagged unless it has been previously identified as problematic.

Furthermore, technical writing of all kinds is often characterized by consistent language use and precise terminology. Even an author who views all writing as inextricably creative must sometimes direct that creativity toward a particular aim :cite:`bringhurst2004elements`. Software documentation, technical manuals, and legal briefs, and pedagogical writing all feature this need and are improved when the author follows the conventions of a field.

Lastly, science demands consistency to promote clarity and replication. At the same time, scientists are in the business of expressing ideas that challenge even the greatest of minds, and their success depends on conveying those ideas to people who then use the ideas in their own work. When an idea is hard to grasp, simplicity and clarity will further its proliferation.

Contributing to Proselint
=========================

The primary avenue for contributing to Proselint is by contributing code to its GitHub repository, used to organize work on the project. In particular, we have developed an extensive set of Issues that range from trivial-to-fix bugs to lofty features whose addition are entire research projects in their own right. To merit inclusion in Proselint, contributed rules must be accompanied by a citation of an expert who endorses the rule. This is not because language experts are the only arbiters of language usage, but because our goal is explicitly to aggregate best practices as put forth by the experts.

A secondary avenue for contributing to Proselint is through discovery of false positives: instances where Proselint flags well-formed idiomatic prose as containing a usage error. In this way, people with expertise in editing, language, and quality assurance can make a valuable contribution that directly improves the metric we use to gauge success.

Acknowledgments
===============

Work on Proselint was supported in part by the `Berkeley Center for Technology, Society and Policy`__ through the CTSP Fellows program, specifically for applying Proselint to the problem of improving governmental communications as laid out in the `Federal Plain Language Guidelines`__. We thank several reviewers who gave feedback on the manuscript, including David Lippa, Scott Rostrup, and Dan Lewis. This work was presented as a talk at *SciPy* 2016 (`YouTube <https://www.youtube.com/watch?v=S55EFUOu4O0>`_).

.. __: https://ctsp.berkeley.edu/

.. __: http://www.plainlanguage.gov/howto/guidelines/FederalPLGuidelines
