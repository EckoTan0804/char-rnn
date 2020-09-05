# Character-Level RNN

In order to gain a better understanding on RNN, I implement a simple character-level RNN based on Andreij Karparthy's [blog post](http://karpathy.github.io/2015/05/21/rnn-effectiveness/) and his [implementation](https://gist.github.com/karpathy/d4dee566867f8291f086) as well as the Neural Network lecture I've taken in summer semester 2020 in KIT. 

The **training** of this RNN is quiet simple:

1. Give the RNN a huge chunk of text
2. Ask it to model the probability distribution of the next character in the sequence given a sequence of previous characters.

At **test** time, we feed a character into the RNN and get a distribution over what characters are likely to come next. We sample from this distribution, and feed it right back in to get the next letter. Repeat this process.

