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

   Writing is notoriously hard, even for the best writers, and it's not for lack of good advice — a tremendous amount of knowledge about the craft is strewn across usage guides, dictionaries, technical manuals, essays, pamphlets, websites, and the hearts and minds of great authors and editors. But much of this knowledge is trapped, waiting to be extracted and transformed..

   We built Proselint, a Python-based linter for prose. Proselint identifies violations of expert style and usage guidelines. Proselint is open-source software released under the BSD license and is compatible with Python 2 and 3. It runs as a command-line utility or editor plugin (e.g., for Sublime Text, Atom, Vim, Emacs) and outputs advice in standard formats, including JSON and standard linting format(``slf``). Proselint includes modules that address redundancy, jargon, illogic, clichés, unidiomatic vocabulary, sexism, misspelling, inconsistency, misuse of symbols, malapropisms, oxymorons, security gaffes, hedging, apologizing, and pretension. Furthermore, Proselint is extensible, enabling creation of domain-specific modules or implementation of house style guides.

   Proselint can be seen as both a language tool for scientists and a tool for language science. On the one hand, it includes modules that promote clear and consistent prose. In the context of science, this helps scientists communicate their ideas to each other and to the public. On the other hand, it measures language usage, explores the factors relevant to creating a useful linter (e.g., false positive rate, reflected in a "lintscore" that we introduce), and demonstrates the need for new corpora and datasets that identify usage errors and false positives. Linguistics and stylometrics rely on tokenized lists of linguistic features to infer properties of the text (e.g. for authorship identification), and in these settings Proselint can provide features based on style and usage.

.. class:: keywords

   linters, writing tools, copyediting

The problem
===========

Writing is notoriously hard, even for the best writers, and it's not for lack of good advice — a tremendous amount of knowledge about the craft is strewn across usage guides, dictionaries, technical manuals, essays, pamphlets, websites, and the hearts and minds of great authors and editors. Consider, for example, *Garner's Modern English Usage*, an authoritative usage guide with 11,000 entries covering a broad range of advice that, when followed, helps writers produce clean and idiomatic prose :cite:`garner2016garner`. Or consider the *Federal Plain Language Guidelines*, a guide created by employees of the U.S. federal government to promote writing that is clear, concise, and well-organized :cite:`Plain2011`. Professional conferences such as the annual meeting of the American Copy Editors Society are dedicated to sharing knowledge about editing prose. And within the academy, organizations such as the American Psychological Association publish manuals whose guidance on style has been adopted as a standard :cite:`american1994publication`. Advice on writing abounds.

Advice on writing touches upon everything from superficial conventions to the deepest reflections of our society and its attitudes. Take, for example, advice concerning the preferred forms of words such as "connote" (vs. "connotate"), which may help to prune needless variants in spelling, but are unlikely to affect the reader's understanding of the text and its author. Compare this to advice concerning needlessly gendered language ("woman scientist", "policeman"), which by being commonplace in language may perpetuate social inequality :cite:`Philips2004`.

Having amassed a pile of useful advice falls short make writing better. This is because advice – though it may be principled, thoughtful, and worth following – is hard to apply in new settings once it has been learned :cite:`Argote2000`. Thus even if one could absorb all the knowledge contained in extant sources of advice on writing, there would still be the problem of recalling and systematically applying that knowledge during the acts of writing and editing. It is slow, costly, and effortful to develop a new habit of any kind (i.e., linguistic or otherwise) :cite:`Fogg2010`. As a result, even after one reads, old habits persist;  errors appear – even though, in some sense – the author knows the rules.

Today, an author who wishes to improve a piece of writing by applying the collective wisdom of experts must rely on indirect means. The most common approach, used extensively in publishing, is a division of labor whereby dedicated staff with deep knowledge of best practices in writing copyedit a piece to their satisfaction. For example, *The New Yorker* uses an editing team that includes fact checkers, editors, grammarians, and more :cite:`Norris2009`. Another approach, used extensively in desktop publishing, is to use software-based tools such as spelling and grammar checkers that mark unrecognized words and purported violations of grammatical rules.

Neither approach fully solves the problem of successful adoption of best practices in writing. Few people have the resources needed to outsource editing to expert staff, and even for those who do, editing by external experts is slow. Copy editors must read the text carefully and are normally unavailable during the act of writing. By the time an editor's notes are received, then, a key opportunity to strengthen the writer's craft has passed. Time-sensitive writing exacerbates this problem, where the delay introduced by an editor may diminish the communication's value. In contrast, existing software-based tools, though they are inexpensive and fast, are typically incomplete, imprecise, or inaccessible (see Existing Tools, below). 

Much of our collective knowledge about best practices in writing is thus essentially trapped, waiting to be extracted and transformed into a medium that makes the knowledge accessible to all authors.

The solution
============

To solve this problem, we built Proselint, a real-time linter for English prose. A linter is a computer program that, like a spell checker, scans through a document and analyzes it, identifying problems with its syntax or style :cite:`Johnson1977`. Proselint identifies violations of expert-endorsed style and usage guidelines [#]_  and alerts the writer of those violations as they are committed, an ideal opportunity to elicit long-term changes in behavior :cite:`ferster1957schedules`. It is as though the experts sit by the writer's side, whispering gentle reminders about best practices in writing.

.. [#] Proselint differs from a spell-checker in that its recommendations do not specifically counter errors in which a word is spelled incorrectly, but rather errors of style and usage, though the two occasionally overlap. For example, consider the malapropism "attacking your voracity", where it is not that "voracity" is a spelling error per se but that the appropriate word is its phonetic neighbor "veracity". Compare this to "attacking your verqcity", almost certainly a typo.

Proselint is open-source software released under the BSD license and compatible with Pythons 2 and 3. It runs efficiently as a command-line utility or editor plugin for Sublime Text, Atom, Emacs, vim, &c. It outputs advice in standard formats – including JSON and standard linting format (``slf``) – allowing for integration with external services and human readable output. Proselint includes modules on a variety of usage problems, including redundancy, jargon, illogic, clichés, sexism, misspelling, inconsistency, misuse of symbols, malapropisms, oxymorons, security gaffes, hedging, apologizing, pretension, and more (see Tables 1 and 2 for a fuller listing).

Proselint can be seen as both a language tool for scientists and a tool for language science. On the one hand, it can be used to improve writing, and it includes modules that promote clear and consistent prose in science writing. On the other, it can be used to measure language usage and to consider the factors relevant to a linter's usefulness.

As a language tool for scientists
----------------------------------

Science and writing are fast friends — science as we know it would be impossible without the written word. But scientific research is, by necessity, hard to understand by all but those most acquainted with it, and harder still to communicate to other scientists and to the public. This leaves room for tools that assist in writing to further the aims of scientists and promote the public's understanding of science. 

Proselint improves writing across a number of dimensions relevant to science communication, including consistency in terminology & typography, concision, and removal of redundancy. For example, Proselint detects whether the lowercase letter x is used in place of the multiplication symbol × when giving screen dimensions (e.g., 1440 x 900), for misspecified *p* values that result from software packages that truncate small numbers (e.g., *p* = 0.00), and for colloquialisms that obscure the mechanisms of science-based technology (e.g., "lie detector test" for the polygraph machine, which measures arousal, not lying per se).

As a tool for language science
------------------------------

Linguistics as a science is largely a descriptivist enterprise, seeking to describe language as it is used rather than prescribe how it ought to be used :cite:`garner2016garner`. Errors are considered in the context of how people successfully learn language and how their errors in doing so (especially children's) reveal the underlying structure of the language learning mechanism (see, e.g.,  overregularization by young English speakers :cite:`marcus1992overregularization`). The nature of a linter runs against an exclusively descriptivist approach to language use because detection of norm violations presupposes the existence of norms :cite:`garner2016garner`.

Despite our implicit prescriptivism, Proselint can be of use to descriptivists, both as an input to standard Natural Language Processing (:math:`\textsc{nlp}`) techniques and as a method for detecting patterns of usage and style in existing corpora without making normative claims (see Applications, Realized and Potential). Though Proselint has not yet been used in extensive linguistic studies, its output fits the formal structure expected by many language-science techniques while emphasizing a different kinds of features: usage and style choices rather than word frequencies and syntactic structures :cite:`Bird:2009:NLP`.

The Proselintian theoretical approach
=====================================

What to check: usage, not grammar
---------------------------------

Proselint avoids detection of grammatical errors, which is both too easy and too hard:

Grammar is too easy in the sense that, for most native speakers, grammatical errors are readily identified, if not easily fixed. The errors that leave the greatest negative impression in the reader's mind are often glaring to native speaker. (On the other hand, more subtle errors, such as a disagreement in number set apart by a long string of intermediary text, escapes even a native speaker's notice.)

Grammar is too hard in the sense that, in its most general form, detecting grammatical errors is AI-hard, requiring artificial intelligence that at least matches human-level intelligence and a native speaker's ear to identify errors. 

Modern :math:`\textsc{nlp}` techniques that detect grammar errors are unavoidably statistical :cite:`Bird:2009:NLP` :cite:`leacock2010automated` and lead to many false positives. Furthermore, standard :math:`\textsc{nlp}` techniques for syntax parsing are designed to extract accurate structures from correct text, not to identify the nearby structures that were likely to be intended, and thus struggle with malformed text, particularly writing who second language is English :cite:`leacock2010automated`. If one assumes that errors are made, there will almost always be more than one nearby grammatical sentence, and which of these is the correct replacement hinges on the intended meaning. There are even cases where the intended meaning will determine *whether* a grammatical error is present: e.g., is "Man bites dog" a headline stating that a man bit a dog, or is there a grammatical error where the subject and object have been swapped? Correcting grammatical errors can be as challenging as detecting them. Compared to usage and style, grammar checking is an uncertain, slow, and complicated enterprise.

Instead of focusing on grammar, we consider errors of usage and style: redundancy, jargon, illogic, clichés, sexism, misspelling, inconsistency, misuse of symbols, malapropisms, oxymorons, security gaffes, hedging, apologizing, pretension, and more. 

Published expertise as primary sources
--------------------------------------

Unlike grammar, for which many people have strong shared intuitions – so much so that a common experimental measure in linguistics is the grammaticality of a sentence as measured by the intuitions of native speakers :cite:`keller2000gradience` – style and usage inspire a multitude of intuitions. Luckily, the authors of respected usage guides have done much of the work of hashing out these conflicting intuitions to arrive at sensible everyday advice :cite:`garner2016garner`. Proselint thus defers to some of the world’s greatest writers and editors, giving direct access to humanity’s collective understanding about the craft of writing English with style. (This conflict avoidance also motivates our policy of defaulting to silence when there are unresolved conflicts between experts, as described below.)

Levels of difficulty
--------------------

In a loose analogy to the Chomskian hierarchy of formal grammars :cite:`chomsky1956three`, we have identified several levels of difficulty in the implementation of the detection and correction of usage errors [#]_:

.. [#] To our knowledge, no one has posed a hierarchy of this sort for organizing the difficulty of identifying different style and usage violations.  

#. AI-hard
#. :math:`\textsc{nlp}`, beyond state-of-the-art
#. :math:`\textsc{nlp}`, state-of-the-art
#. Syntax-dependent rules
#. Regular expressions
#. One-to-one replacement rules. 

Our development of Proselint begins at the lowest levels of the hierarchy, building upwards. At one extreme are usage errors detectable and correctable through one-to-one replacement rules, detecting the presence of a specific word or phrase and suggesting another in its place. At the other extreme are errors whose detection and correction are such hard computational problems that it would require human-level intelligence to solve in the general case, if a solution is possible at all. Consider, for example, usage errors pertaining to the word "only", the correct placement of which depends on the intended meaning (e.g., in "John hit Peter in his only nose", is the "only" misplaced or is it unusual that Peter has only one nose?). Usage errors at this highest level of the hierarchy are hard to successfully identify without introducing many false positives into the mix. Correcting them poses an additional problem because there will often not be a unique solution that can be recommended above all the others. The intermediate cases vary along these dimensions, where, moving up the hierarchy, more false positives are introduced and unique correction becomes less feasible.

Rapiers, cudgels, and the lintscore
-----------------------------------

Any new tool, for language or otherwise, faces a challenge to its adoption: it must demonstrate that the cost of learning to use the tool is outweighed by the utility it provides. Pen & ink, paper, and the computer each enabled new modes of communication and, in doing so, provided obvious value. In contrast, tools that merely improve existing capabilities are at a comparative disadvantage because they must demonstrate a substantial improvement over the status quo. This is the case for Proselint. 

Because of this need to demonstrate utility, earlier language tools attempted to offer as much help as possible. In a sense, they wielded a cudgel, a tool that indiscriminately affects large areas of flesh. Each issue flagged might be an error, but it might instead be a false alarm. Let :math:`T` be the number of true errors, and :math:`F` be the number of false alarms (thus making :math:`T+F` the total number of flags raised by the tool). The cudgel approach attempts to maximize :math:`T`, flagging as much as possible, without considering :math:`F`. Writers who use those tools would see many genuine errors, errors that Proselint might not yet detect. However, their emphasis on maximizing :math:`T` at the expense of :math:`F` is to their detriment. These tools raise so many false alarms that their advice cannot be trusted: writers must weigh each proposed error.

Proselint aims to be not a cudgel, but a rapier, a tool that pinpoints weak spots and strikes where it will make the most impact. With Proselint, we aim for a tool so precise that it becomes possible to unquestioningly adopt its recommendations and still come out ahead with stronger, tighter prose. Better to be quiet and authoritative than loud and unreliable. 

To achieve this, we penalize false positives :math:`F` by evaluating Proselint in terms of its *empirical lintscore*. The lintscore gives a point for every true positive (:math:`T`) and penalizes on the basis of the false-positive rate :math:`\alpha = \frac{F}{T+F}`. The lintscore is given by

.. math::
    l(T,F;k) = T(1-\alpha)^k,

where the parameter :math:`k` controls the strength of the :math:`1-\alpha` penalty.

We can estimate a lintscore for documents with unknown empirical false-positive rates using a straightforward probabilistic model where we only receive credit in the best-case (where every error is a true positive). This probabilistic model treats each identified error as an independent identically distributed Bernoulli random variable. We suppose each flag produces a false positive with probability equal to the empirical false positive rate estimated from a known corpus of related documents (:math:`\hat{\alpha}=\frac{\hat{F}}{\hat{T}+\hat{F}}`). For :math:`N` flags, the probability that every flag is correct is :math:`(1-\hat{\alpha})^N`. If we receive 0 points in all but the best case (where we receive :math:`T\equiv N` points), the expected score is :math:`N(1-\hat{\alpha})^N`. This *generalised lintscore* has the same form as an empirical lintscore, but with :math:`\hat{\alpha}` as an estimated :math:`\alpha` and :math:`k` as the maximal number of successes (:math:`k\equiv N`). The choice of reference corpus is a free parameter.

Note, lintscores are not readability metrics. They evaluate linters, not documents; given a set of documents, signal detection theory allows indirectly estimating prose linters' trustworthiness.

The advice
==========

Proselint is built around advice derived from works by Bryan Garner, David Foster Wallace, Chuck Palahniuk, Steve Pinker, Mary Norris, Mark Twain, Elmore Leonard, George Orwell, Matthew Butterick, William Strunk, E.B. White, Philip Corbett, Ernest Gowers, and the editorial staff of the world’s finest literary magazines and newspapers, among others. [#]_ 

.. [#] Proselint has not been endorsed by these individuals; we have merely implemented their words in code.

Our standard for inclusion of a new rule is that it should be accompanied by an appropriate citation from a recognized expert on language usage. Though we have no explicit criteria for what makes a citation appropriate, we have, in practice, given greater weight to works from well-established publishers and those widely cited as reliable sources of advice. The choice of which rules to implement is ultimately a question of feasibility of implementation, utility, and preference, and our guiding preference is to make Proselint as widely useful as possible with the minimum amount of customization. 

Though it has not arisen, in the case of unresolved conflicts between advice from multiple sources, our default is to exclude all forms of the advice, under the logic that it is unreasonable to hold users of Proselint to a higher standard than the experts, at least one of whom endorses the user's usage choice.

We aim to have excellent defaults without hampering adaptability to user's personal preferences, and thus designed Proselint so that it can be customized either by adding new rules or by excluding existing rules through a configuration file.

Examples of some rules
----------------------

Tables 1 and 2 list much of the advice that Proselint currently implements. The following examples are meant to give a taste of this advice:

#. Detecting the word "agendize", Proselint notes, "agendize is jargon, could you replace it with something more standard?" :cite:`garner2016garner`

#. In response to "In recent years, an increasing number of psychologists have...", Proselint notes, "Professional narcisissm. Talk about the subject, not its study." :cite:`pinker2015sense`

#. In response to "A group of starlings...", Proselint notes "The venery term is 'murmuration'"". :cite:`garner2016garner`

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


Code: Structure & Performance
=============================

Rule modules
------------

Proselint rules are organized into modules that reflect the structure of language advice found in usage guides :cite:`garner2016garner`. For example, Proselint includes a module ``terms`` that encourages expressive vocabulary by flagging use of unidiomatic and generic terms, with submodules for categories of terms found as entries in usage guides. For example, one such submodule, ``terms.venery``, pertains to *venery terms*, which arose from hunting tradition and describe groups of animals of a particular species — a "pride" of lions or an "unkindness" of ravens. Another such submodule, ``terms.denizen_labels``, pertains to *demonyms*, which are used to describe people from a particular place — *New Yorkers* (New York), *Mancunians* (Manchester), or *Novocastrians* (Newcastle).

Organizing rules into modules is useful for two reasons. First, it allows for a logical grouping of similar rules, which often require similar computational machinery to implement. Second, it allows users to include and exclude rules at a higher level of abstraction than that of an individual word or phrase. We note that people may wish to include and exclude linting rules at a level more finely grained than the submodule, and it is an open challenge how best to allow this customization while minimizing the pain of navigating, modifying, and comprehending the format for customization.

Rule templates
--------------

In general, a rule's implementation in code need only take in a string of text, apply logic identifying whether the rule has been violated, and then return a value identifying the violation in the correct format. These weak requirements, paired with Python's expressibility, allow detectors to be built for all computable usage and style requirements. However, it provides little help when creating new rules, which often follow similar logic.

To ease the implementation of new rules, we wrote functions that help to follow the protocol and provide the most common logical forms. These include checking for the existence of a given word, phrase, or pattern (``existence_check()``), for intra-document consistency in usage (``consistency_check()``), and for usage of preferred forms (``preferred_forms_check()``). 

For example, the following code implements a rule regarding the formatting of times using the ``existence check`` rule template. 

.. code-block:: python

    def check_midnight_noon(text):
        """Check the text."""
        err = "dates_times.am_pm.midnight_noon"
        msg = (u"12 a.m. and 12 p.m. are wrong and "
        "confusing. Use 'midnight' or 'noon'.")
        regex = "12 ?[ap]\.?m\.?"
        return existence_check(text, [regex], err, msg)

This function detects use of 12am or 12pm (or many other variants, including 12AM, 12 P.M, and 12aM) and suggests that the author use noon or midnight in its place.

Memoization
-----------

One of our goals is for Proselint to be efficient enough for use as a real-time linter while an author writes. Efficiency is increased by avoiding redundant computation, storing the results of expensive function calls from one run of the linter to the next, a technique called *memoization*. Consider, for example, that many of Proselint's checks can operate at the level of a paragraph and that most paragraphs do not change from moment to moment when a sizeable document is being edited. At the extreme, when a linter is run after each keystroke, this is true by definition. By running checks over paragraphs, recomputing only when the paragraph has changed (and otherwise returning the memoized result), it is possible to reduce the total amount of computation and thus improve the linter's running time. Proselint makes extensive use of memoization to improve its running time.


Using Proselint
===============

Installation
------------
Proselint is available on the Python Package Index and can be installed using pip:

.. code-block:: bash

   pip install Proselint

Alternatively, those wishing to develop Proselint can retrieve the Git repository from https://github.com/amperser/Proselint and then install the software using setuptools: 

.. code-block:: bash

   python setup.py develop


Command-line utility
--------------------

At its core, Proselint is a command-line utility that reads in a text file:

.. code-block:: bash

   proselint text.md

Running this command prints a list of suggestions to stdout, one per line. The GNU Error Message Formatting standard :cite:`stallman2016gnu` provides the base format for displaying these suggestions. Like many other linters, we specify further that the source of the error (the ``check_name``) be included separately from the message describing the error. Because this form is used by many linters, we call this the Standard Linting Format (``slf``). Each ``slf`` formatted suggestion has the form:

.. code-block:: bash

   text.md:<line>:<column>: <check_name> <message>

For example,

.. code-block:: bash

  text.md:0:10: uncomparables.misc Comparison of ... 
  an uncomparable: 'unique' can not be compared.

suggests that, at column 10 of line 0, the check ``uncomparables.misc`` detected an issue where the uncomparable adjective "unique" was compared, as in "very unique". The command-line utility can also print the list of suggestions in JSON using the ``--json`` flag. In this case, the output is considerably richer:

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
An effective way to promote adoption of best practices in writing through linters is to embed linters within the tools that people already use to write; this removes a barrier to adoption. Towards that aim, plugins for popular text editors, including Emacs, vim, Sublime Text, and Atom are available for Proselint. Some were created by us, some were contributed by others in the community.

Applications, realized and potential
====================================

As a proof of concept, we used Proselint to make contributions to several documents. This includes the White House's `Federal Source Code Policy <https://github.com/WhiteHouse/source-code-policy>`_; `The Open Logic Project <https://github.com/OpenLogicProject/OpenLogic>`_, a textbook on advanced logic; Infoactive's `Data + Design book <https://github.com/infoactive/data-design>`_; and many of the other papers that were submitted for potential contribution to `SciPy 2016 <https://github.com/scipy-conference/scipy_proceedings/tree/2016>`_. We note that  In addition, to evaluate Proselint's false-alarm rate, we developed a corpus of essays from well-edited magazines such as *Harper's Magazine*, *The New Yorker*, and *The Atlantic*(the list of articles can be found `here <https://github.com/amperser/proselint/tree/master/corpora>`). We then measured the lintscore, defined below. Because the essays included in our corpus were edited by a team of experts, we expect Proselint to remain mostly silent, commenting only on the rare error that slips through unnoticed by the editors or, more commonly, on the finer points of usage, about which experts may disagree. When run over v0.1.0 of our corpus, we achieved a lintscore of 98.8 (*k* = 2).


An analysis of potential applications
-------------------------------------

The most straightforward application of Proselint is for enforcement of usage and style guidelines in writing. This could include extending Proselint to enforce following a house style guide or an academic publisher's journal requirements.

A possible application of Proselint as a tool for language science is in tracking historical trends in usage. Corpora such as Google Books have been useful for measuring changes in the prevalence of words and phrases over several hundred years. Our tool, in providing a feature set for usage, can be used in a similar way. For example, one might study the prevalence of airlinese (including, for example, use of "momentarily" to mean "in a moment", as in the phrase "we are taking off momentarily") and its alignment with the rise of that industry. 

Another potential application of Proselint as a tool for language science is in stylometry and authorship identification; instead of using standard stylometric measures, which include word frequencies and syntactic structures, we can consider Proselint's rules as a feature set that can be used to identify authors. In a sense, this would allow us to identify authors based not on their language use, but on their language misuse.

The ability to identify authors also enables inverting and generalizing that process, using Proselint's output to obfuscate or encrypt messages by selectively introducing, changing, or removing usage choices. With moderate modifications and a protocol for establishing usage-based keys, Proselint could become a system for designing content-aware steganographic systems, allowing users to convey hidden messages in their choice of words and styles :cite:`bergmair2006content`. Encryption would require modifying the Proselint infrastructure to identify cases where more than one acceptable choice exists.

Finally, standard readability metrics are not defined in a way that would capture the kinds of suggestions that Proselint makes, focusing instead on reading ease rather than conventionality :cite:`flesch1948new`. Proselint could be used to create automated metrics for the readability, consistency, and stylishness of written language.

Existing tools
==============

We have collected a list of known tools for automated language checking. They include:
`1Checker <http://www.1checker.com/>`_, `AbiWord's grammar checker <http://www.abisource.com/>`_, `After the Deadline <https://openatd.wordpress.com/>`_, `Alex <http://alexjs.com/>`_, `Autocrit <https://www.autocrit.com/editor/>`_, `ClearEdits <http://www.clearwriter.com/clearedits.html>`_, `CorrectEnglish <http://www.correctenglish.com/>`_, `CKEditor <http://www.webspellchecker.net/>`_, `Editor <http://www.serenity-software.com/>`_, `The Editorium <http://www.editorium.com/ETKPlus2014.htm>`_, `EditorSoftware <http://www.editorsoftware.com/>`_, `Edminton <http://editminion.com/>`_, `Expresso <http://expresso-app.org/>`_, `Ghotit <http://www.ghotit.com/>`_, `Ginger <http://www.gingersoftware.com/>`_, `GNU Diction <https://www.gnu.org/software/diction/>`_, `GNU Style <http://archive09.linux.com/feature/56833>`_, `Grac <http://grac.sourceforge.net/>`_, `GrammarBase <http://www.grammarbase.com/>`_, `GrammarCheck <http://www.grammarcheck.net/>`_, `Grammar Check Anywhere <https://www.spellcheckanywhere.com/grammar_check/>`_, `Grammar Expert Plus <http://www.wintertree-software.com/app/gramxp/>`_, `GrammarianPro <http://linguisoft.com/gramerrorfeatures.html>`_, `Grammark <https://github.com/markfullmer/grammark>`_, `Grammarly <https://www.grammarly.com/>`_, `Grammar Slammer <http://englishplus.com/grammar/>`_, `Grammatica <http://grammatica-english.soft32.com/>`_, `Grammatik <https://en.wikipedia.org/wiki/Grammatik>`_, `Graviax <http://graviax-grammar-checker.soft112.com/>`_, `Hemmingway <http://www.hemingwayapp.com/desktop.html>`_, `ivanistheone's scripts <https://github.com/ivanistheone/writing_scripts>`_, `Language Tool <https://www.languagetool.org/>`_, `Matt Might's shell scripts <http://matt.might.net/articles/shell-scripts-for-passive-voice-weasel-words-duplicates/>`_, `Microsoft Word's grammar check <https://support.office.com/en-us/article/Check-spelling-and-grammar-cab319e8-17df-4b08-8c6b-b868dd2228d1>`_, `OnlineCorrection.com <http://www.onlinecorrection.com/>`_, `PaperRater <https://www.paperrater.com/>`_, `PerfectIt <http://www.intelligentediting.com/>`_, `ProWritingAid <https://prowritingaid.com/>`_, `Reverso <http://www.reverso.net/>`_, `RightWriter <http://www.right-writer.com/>`_, `Rousseau <https://github.com/GitbookIO/rousseau>`_, `SpellCheckPlus <http://spellcheckplus.com/>`_, `Stilus <http://www.mystilus.com/Main>`_, `Textanz <http://www.textanz.com/>`_, `Virtual Writing Tutor <http://virtualwritingtutor.com/>`_, `Wave <https://en.wikipedia.org/wiki/Apache_Wave>`_, `WhiteSmoke <http://www.whitesmoke.com/>`_, `WordPerfect <http://www.wordperfect.com/us/>`_, `WinProof <http://www.franklinhu.com/winproof.htm>`_, `WordRake <http://www.wordrake.com/>`_, `write-good <https://github.com/btford/write-good>`_, and `Writer's Workbench <http://www.emo.com/>`_.

Though an extensive analysis of these tools is beyond the scope of this paper, we note that these tools are varied in their approaches and coverage. Proselint differs from each tool in a variety of ways (e.g., focusing on grammar versus style, being open versus closed source, or extensible versus static). The greatest difference arises from our willingness to sacrifice coverage to maintain user trust via low false-positive rates as measured through the lintscore. 

Critique: normativity in prose styling
======================================

One critique of Proselint :cite:`hackernews2016` is a concern that introducing any kind of linter-like process to the act of writing prose diminishes the ability for authors to express themselves creatively. These arguments suggest that authors will find themselves limited by the linter's rules and that, as a result, this will have a shaping or homogenizing effect on prose.

To this critique, there are several possible responses. The first few of these apply in general, while the latter apply in the case of technical and scientific writing:

Our goal is not to homogenize text for the sake of uniformity (though perhaps there is value there, too), but rather to detect instances of language use that have been specifically identified by usage experts as being problematic. Creative use of language is not flagged by Proselint unless it has been identified as problematic. Novelty will continue to introduce new usages, and some of them will be poor and later pointed out as such by authors identified as trustworthy. If, however, one does not trust an usage guide's point of view, our strongest recommendation would be to turn off the modules associated with that guide.

Technical writing of all kinds is often characterized by consistent language use and precise terminology. Even if one views all writing as an inextricably creative endeavor, that creativity – in some cases – needs to be directed toward particular aims :cite:`bringhurst2004elements`. Software documentation, technical manuals, legal, and pedagogical writing all feature this need. The needs of each of these cases will not be well addressed by the same set of guidelines, but each will have a set of guidelines that it can benefit from following.

Science demands consistency to ensure that replication and clarity is possible. At the same time, scientists are in the business of expressing ideas that challenge even the greatest of minds. Their success depends upon their ability to accessibly and captivatingly convey worthwhile ideas that people wish to use in their own work. In cases where the ideas themselves are difficult to grasp, it is important to eradicate opacity from the prose because it conflicts with the idea's proliferation.

Future
======

We see a number of directions for future development of Proselint. 

Scalable, dynamic false-positive detection
------------------------------------------

Computing false-positive rates means identifying whether flags are hits or false alarms. Currently, detecting false positives requires manually evaluation; this scales poorly. Worse, the process must be repeated each time the linter is run. To address dynamic documents, it would be useful to detect which errors have already been flagged. With little modification, this ability would also allow people to persistently silence instances of flags identified as false alarms.

One approach to scaling false-positive detection divides the task into isolable chunks. Combining this with a process for rapidly evaluating those chunks makes checking for false positives easier across the board and would open the door to load-distribution mechanisms such as crowdsourcing, though it would require solving decision-theoretic problems for false-positive-rate sampling. This can be applied at various levels of organization: corpora, documents, and even rules across documents.

Context-sensitive rule application and machine learning
-------------------------------------------------------

Many rules may apply better to some kinds of documents than to others. For example, in most cases, "extendable" will be conventionally preferable to "extensible"; in software development, the opposite is likely to be true. Applying these rules without consideration of the context will systematically introduce false positives.

In the sense that a riskier rule is one with a higher false-positive rate, context-sensitive rules are necessarily riskier than non-context-sensitive rules. To see why, consider that if a rule were to introduce many false positives across all contexts, it would not be included in Proselint. For rules that do not produce many false positives across contexts, there is no reason to make them context specific. The only reason to include context-specific rule applications is if there are some contexts in which a rule produces higher false-positive rates than in other contexts. If those false-positive rates were low enough to not be excluded by the context insensitive version, their net false-positive rate would only be lower, meaning it would certainly be included in the basic Proselint rule set, excluding it from candidacy as a context-sensitive rule. Accordingly, introducing a rule that *should* be context sensitive, but without the appropriate context sensitivity, will guarantee an increased false-positive rate.

We can silence rules that are predicted to be irrelevant due to context. This allows inclusion of a greater variety of rules without introducing false positives. For example, consider Proselint's rule that states that, when specifying a decade, an apostrophe is unecessary: Eisenhower was president in the 50s, not the 50's. However, not all instances of "50's" are problematic. Consider, for example, the posessive form of artist "50 Cent". One can validly write about "50's manager" when referring to his manager without having made a usage error about decades. Thus Proselint's detector identifies whether a document's topic is 50 Cent. When the topic is not detected, the tool identifies "50's" as a usage error, but when it is detected, the the tool does not flag the usage as erroneous.

The 50 Cent topic detector was developed by hand in the fashion of expert knowledge systems research :cite:`jackson1986introduction`. Generalizing this ability will be crucial to safely growing Proselint's coverage of usage errors. Machine learning techniques for identifying the topic (or mixture of topics) that apply at any point in a document (e.g., topic models :cite:`blei2009topic`) will be needed. Once incorporated, generalizing this to hierarchical, nonparametric topic models will enable taking document sub-structure into account as a form of context :cite:`blei2010nested`.

Improved self-evaluation procedure with multiple corpora
--------------------------------------------------------

In our internal evaluations of Proselint, we calculate the empirical lintscore is manually on a static corpus of professionally edited documents. This process can be improved in a number of ways that will lead to different kinds of improvement in Proselint. In addition to boons from making evaluation less effortful, one major improvement would be to identify multiple corpora with different features. We currently have only one corpus, composed of professionally edited documents, which we assume will have few errors. This efficiently alerts us to false alarms that are introduced by the inclusion of new rules. However, it does a poor job of estimating performance on other metrics.

A corpus of relatively green documents are more likely to have true positives and, consequently, will improve our estimates of Proselint's positive utility. If these documents are modified in accordance with Proselint's suggestions, it will create new opportunities in the theory of linting. Lintscores are likely to decrease between drafts if advice is accepted and no new errors are introduced (there will be fewer true positives), but lower lintscores are generally worse. We need new metrics that track Proselint's success in improving documents.

Corpora of documents drawn from different content-based categories (technical papers, scientific articles, software documentation, fiction, journalism, &c.) will allow us to determine Proselint's performance in evaluating these specific fields. Given that certain rules may be relevant to some fields more than other, this will allow us to ensure that Proselint can be used by the widest possible group of individuals. This also will allow us to learn which rule-sets are relevant to which semantic contexts.

Different document formats (e.g, ``.rst``, ``.tex``, ``.md``, ``.html``, &c.) often rely on syntactical conventions that Proselint falsely identifies as errors. Similar concerns arise for documentation written as docstrings or code comments in a variety of programming languages. Corpora focusing on individual formats and languages will aid in identifying and filtering these errors, enabling development targeted at addressing these problems.

Stylometrics and machine learning
---------------------------------

The field of stylometrics has extensively studied the problem of identifying the true authors of documents. Many of these studies focus on the relative frequencies with which individual words are used, especially function words. For example, on the basis of the frequency of function words such as "to" and "by", Mosteller and Wallace :cite:`mosteller1963inference` inferred the authorship of twelve essays in the *Federalist Papers*. Proselint provides new measures that could be used to improve this kind of stylometric analysis. 

Several applications follow from authorship identification. One uses its ability to detect ghost-written documents, though this assumes that there is a ground-truth corpus with samples of the author's writing. This could have benefit for identifying academic dishonesty (e.g., purchasing and selling of ghost-written essays). On the other hand, someone who applies Proselint to their text may be able to *escape* identification by avoiding features that distinguish the author's writings. 

Unlike our current rules, these techniques are fundamentally statistical. Machine-learning techniques for inferring identity from sparse data will be particularly applicable. The errors Proselint finds are rare, and sparse measures pose difficultly for methods like those in :cite:`mosteller1963inference`. Furthermore, this endeavor will benefit from an approach that considers the cross product of authors and topics (in the vein of :cite:`rosen2004author`).

An unsolved problem: foreign languages
--------------------------------------

We have no immediate plans for extending Proselint to other languages. Addressing the problem of linting prose for style and usage errors in English (of both American and British varieties) is challenging enough for native speakers, and attempting to build rule-sets for languages in which we lack fluency would seem to be an exercise in folly. Attempting to manage a community around the correct use of a language we do not speak would be inappropriate. An open problem, then, is how to extend Proselint to become a universal linter for prose. 

Missing corpora
---------------

To evaluate Proselint's false-positive rate, we built a corpus of text from well-edited magazines likely to contain low rates of usage errors. In the course of assembling this corpus, we discovered a lacuna in the available linguistic corpora: there are no annotated corpora that provide false-positive rates for style and usage violations [#]_. The Proselint testing framework is an excellent opportunity to develop such a corpus. Unfortunately, because our current corpus derives from copyrighted work, it cannot be released as part of open-source software. Developing an open-source corpus of style and usage errors will be necessary if these tools are to be made available for :math:`\textsc{nlp}` research outside internal testing of Proselint.

.. [#] Editor :cite:`editor_compare` has built a corpus which compares the performance of various grammar checkers (not including Proselint). Their corpus consists of "real-world examples of grammatical mistakes and stylistic problems taken from published sources". A corpus made of errors will maximize true positives, but misestimates false-positive rates in real-world documents. Their corpus is not publicly available, and they do not provide a standard format for describing corpora annotated with false positives and negatives.

Contributing to Proselint
=========================

The primary avenue for contributing to Proselint is by contributing code to its GitHub repository, used to organize work on the project. In particular, we have developed an extensive set of Issues that range from trivial-to-fix bugs to lofty features whose addition are entire research projects in their own right. To merit inclusion in Proselint, contributed rules must be accompanied by a citation of an expert who endorses the rule. This is not because language experts are the only arbiters of language usage, but because our goal is explicitly to aggregate best practices as put forth by the experts.

A secondary avenue for contributing to Proselint is through discovery of false alarms: instances where Proselint flags well-formed idiomatic prose as containing a usage error. In this way, people with expertise in editing, language, and quality assurance can make a valuable contribution that directly improves the metric we use to gauge success.

Acknowledgments
===============

Work on Proselint was supported in part by the `Berkeley Center for Technology, Society and Policy`__ through the CTSP Fellows program, specifically as regards applying Proselint to the problem of improving governmental communications as laid out in the `Federal Plain Language Guidelines`__.

.. __: https://ctsp.berkeley.edu/

.. __: http://www.plainlanguage.gov/howto/guidelines/FederalPLGuidelines
