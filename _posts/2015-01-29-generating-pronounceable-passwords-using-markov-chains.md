---
layout: post
title: Pronounceable Passwords Via Markov Chains
---

So, it turns out that your passwords probably shouldn't be easily guessable words. But something like `9CfAEPrqLW` isn't exactly easy to remember (note to self: change bank password immediately). It would be great if we had a password that was both random and easy to recall.

### Random Letters

The problem with picking random letters is that many letter combinations don't naturally appear in any words, mostly because they'd be impossible to pronounce. We need something that takes into account the fact that certain letters appear together more frequently, and in particular sequence.

### Enter Markov Chains

Markov chains are a pretty straightforward random generator concept: the probabilities for the next state are determined by the current one. If that sounds complicated, <a href="http://setosa.io/blog/2014/07/26/markov-chains/">here's a visual explanation</a>.

In our case, we want to pick the next letter based upon the current letters. For instance, we know that

    sh

is typically followed by a vowel, so we can randomly pick one of those. But how do we figure the probability for the next letter in

    terrom

?

At this point we make the observation that the probability is influenced more by the immediately preceding letters than by the earlier letters. So, it doesn't really matter that our word started with the letter `t`, but the fact that the letters `om` are the immediately preceding letters is very important.

So, we'll just use a set of probablities for every two letter combination (or three, or four, or whatever we think works best). We can easily parse through a list of English words to determine those numbers.

### One Last Wrinkle

Now we run our Markov generator and tell it to produce nine letters and it spits out

    terromatr

Hmm. While the letters `tr` often appear together, they don't usually appear at the end of a word. So, we need to adjust our probabilities when we generate the last couple letters. When we parse through our list of English words, we'll keep track of the probabilities for the penultimate letter and ultimate letter separately.

Using this modification, we run our generator again and get

    terromash

That's more like it! My new bank password is easy to remember because it looks like an actual word, and sounds vaguely delicous.
