---
layout: post
title: De Bruijn Sequences for Rhythm Generation
---

After trying Euclidian Sequences, I had a look at some different methods of generating rhythmical sequences. I wanted to find something elegant, with a minimum of parameters, that might also be intuitive for control. I decided to make use of triggering events via binary means, and after a little research found a nice idea in the "De Bruijn Sequences".

De Bruijn sequence require just 2 parameters, k, which will describe the possible alphabet states (for binary this is simply 2), and then the parameter n will detemine all of the possible subsequences.
The nice thing about the sequence is that once the binary string has been generated, you can splice a subsequence of length n at any of the indicies to generate a new pattern, with the number of events occuring further along in the string.

{% highlight python %}
  de_bruijn(k, n)
      ## De Bruijn sequence for alphabet k
      ## and subsequences of length n.
 
 >>> de_bruijn(2, 2)
 '0011'
 >>> de_bruijn(2, 3)
 '00010111'
 >>> de_bruijn(2, 4)
 '0000100110101111'
 >>> de_bruijn(2, 5)
 '00000100011001010011101011011111'
 {% endhighlight %}

I then implemented this within MaxMSP and triggered MIDI notes in an Ensoniq EPS 16+ running a sample set of TR-606 sounds and recorded this on a casseete tape for thick tape saturation. When you set up a couple of these generators each at a different MIDI note value you can get some interesting results.
