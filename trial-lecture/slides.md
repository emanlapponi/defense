---
marp: true
title: End-to-end systems in Natural Language Processing
description: Trial lecture
theme: default
paginate: true
size: 16:9
---
<!--- _class: invert --->
<!--- _paginate: false --->
# End-to-end systems in Natural Language Processing
## 👩🏻‍🔬 🧠 ![width:60px](figures/elmo.png) From feature extraction to Sesame Street
> **Emanuele Lapponi**
> Language Technology Group
> Institute for Informatics
> University of Oslo
> `@emanlapponi`

---
## 🤔 from-what-end-to-what-end NLP systems?

- Depends where you are starting from! Text? Speech? A picture, maybe?

- For non-research examples, you need not look further than your phone!

![bg right vertical](figures/translate.png)
![bg right vertical](figures/kindly.png)
![bg right vertical](figures/predictive.png)

---
# ⚗️ End-to-end NLP experimental setups

- Typically going from text to some specific task, e.g.:
    - Question answering `(question,text) -> offsets`
    - Sentiment analysis `text -> sentiment`
    - Named entity recognition `text -> (label,offsets)`

- Today: NLP from 2012 to 2019, with Negation scope resolution 

---
# 🕵🏻‍♂️ 🔎 Negation Scope Resolution (NSR)

> Given a sentence and a negation cue (**not**, -**less**, **without**), which tokens are negated?

- If **{** he was **}** in the hospital and yet **not** **[** on the staff **]** he could only have been a house-surgeon or a house-physician.

- ... and **no** **[** one could have escaped our notice **]**.

---
# Negation Scope Resolution (NSR)

A natural* fit for sequence labeling

```txt
...
and     O
no      CUE
one     NEGATED
could   NEGATED
have    NEGATED
escaped NEGATED
our     NEGATED
notice  NEGATED
.
```

<!--- _footer: '* Arguably, deep semantic parsing is an even _more_ natural fit 🤔' --->

---
<!--- _class: invert --->
<!--- _paginate: false --->

## <!--- fit ---> 2012

![bg blur:8px](figures/collider.png)

---

# 👩🏻‍🔬 UiO2: Sequence-Labeling Negation with Dependency Features
> ###### Lapponi et al., 2012

- A Highly (over?) engineered system
- Uses the most fashionable tool of the time: CRFs
- But everyone has CRFs! What matters most here (and,  arguably, in NLP in general) is representation.

---

# Ye olde NLP pipeline

![width:10000px](figures/uio2-pipeline.png)

---

# What's a word?

A bunch of symbols: we decide what those symbols are, for instance:
- token `notice`
- part-of-speech disambiguated: `notice-NOUN`
- the backward trigram: `notice-our-escaped`
- might help to know that it's a direct object:`notice-dobj`

---

# What's a negated word?

The same as a normal word, but also:
- a right/left distance from a negation cue: `5`
- in a syntax (dependency) tree, a shortest path: `3`
- and a very specific symbol to represent it: `UP-dobj-DOWN-nsubj-DOWN-dep`
- Very, very sparse

![bg right 90%](figures/notice-tree.png)

---

# Then, give the matrix to the model

Without diving into the specific, for intuition's sake:
![width:600px](figures/crf.png)

### Ah ha! One more thing

Since the transitions have an effect on the model, experiment with more labels:
`[O, CUE, N, S]` - counterintuitive, but does the trick

---
<!--- _paginate: false --->

## <!--- fit ---> 2013

![bg blur:8px](figures/wrecking-ball.jpg)

