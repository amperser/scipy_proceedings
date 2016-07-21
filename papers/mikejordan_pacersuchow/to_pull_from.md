One intuition behind this rule can be found if you consider separately estimating the false positive rate of a rule-set and the success of a particular application of the rule-set to a document. The calculated false-positive rate as applied to a corpus can be thought of as the maximum likelihood estimate of the probability that a randomly selected instance of a flag in the corpus is a false positive. This perspective means that we can treat the corpus as an estimate of a generative model for linting quality in new documents without a manual analysis. This allows generalizing a score for new documents without needing to calculate the false positive rate for the individual document.

Suppose that each flag in a new document produces false positives with a Bernoulli distribution with probability equal to the estimated false positive rate from the corpus (:math:`\hat{\alpha}=\frac{\hat{F}}{\hat{T}+\hat{F}}`). If the new document generates :math:`N` flags, then the probability that every flag is correct is :math:`(1-\hat{\alpha})^N`. If this is multiplied by the number of true positives under this perfect case (i.e., :math:`T\equiv N`) we have

.. math::
    N(1-\hat{\alpha})^N

which is a generalized lintscore, with :math:`\hat{\alpha}` as the estimated :math:`\alpha` and :math:`k` is the total number of events which are presumed to be successes (:math:`k\equiv N`). This is equivalent to the expected score when you assign full credit in the case where all lints are true positives and 0 otherwise.

This score does not take into account false negatives or true negatives, and the reason it does not is worth mentioning as it illustrates one of the core problems with prose linting.

False negatives can be understood in terms of cases where a rule should have activated and flagged the text, but failed to do so. True negatives can be understood as those opportunities where a rule was applied and successfully did not raise an error. Both of these ideas are problematic when analyzing prose in a way that may not in other signal detection problems. Thus a full recall-precision curve analysis seems inappropriate in this domain.


:sc:`Problem 0`: Building off of a default
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In a tautological sense, every editor has a version of Proselint (and any other automated writing aid) already installed, it is merely installed with the null rule-set. That is, the set of rules that claim no substrings anywhere have any faults whatsoever; literally, anything goes. Any time one will attempt to convince someone to adopt a tool, that tool needs to demonstrate itself as better than this default.

If people's prose was littered with errors to an egregious degree this default would not suffice. But people are competent writers. Proselint and other writing aids aim to polish what is already fairly good prose. Thus, we can expect that any appropriate rule-set can expect to be invoked sparingly. 

Sparse use of the ruleset means that the positive statements are distinguished from the background of the null rule-set. Because positives are what distinguish a writing aid, focusing on the false positive and true positive ratios. Negative statements are the remnants of the null rule-set, meaning they are less indicative of the quality of the linter.

In short, all linters and all language tools will be missing most errors by virtue of the problem they are trying to solve. Given this, avoiding the pitfalls of a high false-positive rate will be the comparison that matters most for determining their value.

:sc:`Problem 1`: Magnitude of "potential activations"
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It is not clear how many chances there are for a rule to be activated when one considers analyzing prose. It could be at the sentence level or it could be at the word level, or it could be at the pairs of words level. If we are maximally generous, any subset of words could comprise a potential activation instance for a rule, meaning that the number of rule opportunities in the most liberal terms is the Bell number of the number of words in any document being analysed.

That means that without further specification, the number will grow extremely rapidly. If this occurs and the rule set is sparsely activated(it has specifically tailored rules in the manner of Proselint), this means that the true negative score will be near 1, because there were so many opportunities for rules to be applied and they were not. If this occurs and the rule set is densely activated, the recommendations in aggregate will be incomprehensible as they will be so densely packed as to be unable to represent a coherent claim about the totality of the text.


:sc:`Problem 2`: Arbitrariness of "potential activations"
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If on the other hand you were to come up with a criterion that limits the number of potential activations, you now have an arbitrary criterion (likely defined by your language theory itself) that determines what counts as a potential activation. If different language theories postulate a set of potential activations that is neither a subset nor a superset of your rules, those language theories would then be incommensurable [#]_.


.. [#] Note that this is not a problem for false positives because any rule that is not present in another theory can be treated as either a null result or a false positive by the theory lacking the rule. This stems from the fact that by default, all documents are already being analysed by the "null language theory" which states that there are no errors in any text. This gives a ground from which errors can be built up (since defining them in terms of the set of potential activations is so difficult) rather than winnowed down.

:sc:`Problem 3`: Infinitude/nonuniqueness of "potential activations"
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The same string (a sentence, for instance) can be analysed as being an error by two different theories for entirely different reasons. It is unclear whether two rules that identify the same text as problematic but differ in their justifications are in agreement or disagreement.

There are an infinite number of possible rule sets (in general), in the same way that there are an infinite number of possible strings. So, if we consider all possible rule sets for evaluating any finite bit of prose, there will always be an infinite number of potential interpretations. Because those interpretations could conflict with one another while agreeing in a set theoretic sense on which substrings are to be flagged, you cannot count on any agreement that is characterised only in terms of the strings to be uniquely identifiable and associated with any particular set of potential activations.

:sc:`Problem 4`: False negatives are undefined without a positive model
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Finally, false negatives lack meaning without some particular positive model to be contrasted against the model under consideration. A false negative states that a violation occurred that was not identified. But one cannot say that a violation occurred without specifying what violation was that occurred, meaning that a positive model for identifying which violations were possible in the first place is needed.

Our implicit comparison is to the null model. And the defining feature of the null-model is that it makes no positive statements at all. Given that, there are no potential positive statements that Proselint could miss. All negative statements are true negatives by fiat. For the least interesting reason possible, Proselint has a perfect false-negative rate. 


.. Proselint is precise. 

Assessing false positive rates
------------------------------

Unfortunately despite their cruciality, false positive rates pose quite a challenge as an assessment criterion.

Notably, a false positive is difficult (if not impossible) to identify without some kind of human intervention. 
Any automated system for determining whether some string of text is or is not an error is itself a normative theory of prose style as embodied in those determinations.
While it may not be a *linter* per se – for example, because of the speed or manner with which it is providing the statements – it is nonetheless equivalent to the normative role Proselint plays.
Thus, while we would be able to provide comparisons between the recommendations offered for the same text by different normative language theories, that would not give us a good measure of false positives as it matters in terms of establishing trust with users.

To build the kind of trust we are aiming at, we need to be precisely attuned to the linguistic intuitions of human writers themselves. 
There is no way of knowing that a linting rule activation was successful or unsuccessful without direct feedback.
This is why we have developed a corpus of writings from well-established publications and manually coded them to identify false and true positives. 
It is this corpus that we use to measure Proselint's lintscore. 

One of the biggest hindrances for adding new rules (at all) and more complicated and nuanced rules (in particular) stems from the difficulty of efficiently measuring how they affect our lintscore.
A key feature in growing Proselint's capabilities will be establishing some mechanism for more efficiently inferring false positives.

In the sense that a riskier rule is one with a higher false-positive rate, context-sensitive rules are necessarily riskier than non-context-sensitive rules. To see why, consider that if a rule were to introduce many false positives across all contexts, it would not be included in Proselint. For rules that do not produce many false positives across contexts, there is no reason to make them context specific. The only reason to include context-specific rule applications is if there are some contexts in which a rule produces higher false-positive rates than in other contexts. If those false-positive rates were low enough to not be excluded by the context insensitive version, their net false-positive rate would only be lower, meaning it would certainly be included in the basic Proselint rule set, excluding it from candidacy as a context-sensitive rule. Accordingly, introducing a rule that *should* be context sensitive, but without the appropriate context sensitivity, will guarantee an increased false-positive rate.


Scalable, dynamic false-positive detection
------------------------------------------

Computing false-positive rates means identifying whether flags are hits or false alarms. Currently, detecting false positives requires manual evaluation, which scales poorly. Worse, one must repeat the process each time the linter is run. To address dynamic documents, it is useful to detect which errors have already been flagged. With little modification, this would also allow users to persistently silence instances of flags identified as false alarms.

One approach to scaling false-positive detection divides the task into isolable chunks. Combining this with a process for rapidly evaluating those chunks makes checking for false positives easier across the board and would open the door to load-distribution mechanisms such as crowdsourcing, though it would require solving decision-theoretic problems for false-positive-rate sampling. This can be applied at various levels of organization: corpora, documents, and even rules across documents.

