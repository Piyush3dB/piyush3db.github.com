---
layout: post
title:  "Draft test: Welcome to Jekyll!"
date:   2017-04-01 16:25:13 +0100
categories: jekyll update
---

Vanilla RNN:

1. Matrix-Matrix multiplies
  input = (BxV) with weights=(HxV), output = (BxH)
  input = (BxH) with weights=(HxH), output = (BxH)
  (input = (Bx(V+H)), output = (BxhH))
2. 1 pointwise tanh range limiter
3. 2B+1 pointwise add for linear transformations
   2B batch-wise broadcast at the feedforward nodes
   1 for the previous+input fuse




LSTM Cell:

Set V = H

then the two feedforward nodes can be combined with the add node they feed into to give a single mat-mat multiplication

1. Feedforward linear transformations
   Size 4HxV matrix-matrix multiply for i2h
   Size 4HxH matrix-matrix multiply for p2h
   2 size Bx4H pointwise add for i2h and p2h bias

  input = (BxV) with weights=(4HxV), output = (Bx4H)
  input = (BxH) with weights=(4HxH), output = (Bx4H)
  (input = (Bx(V+H)), output = (Bx4H))
2. 3 pointwise sigmoid for coefficient calculation (size BxH)
3. 2 pointwise tanh range limiters (size BxH)
4. 2 pointwise add for linear transformations
   1 for the input+previous fuse (size BxH)
   1 for the hidden+state fuse (size BxH)
5. 2 pointwise mul for the filters (size BxH)


GRU Cell:

1. Matrix-Matrix multiplies
  input = (BxV) with weights=(4HxV), output = (Bx4H)
  input = (BxH) with weights=(4HxH), output = (Bx4H)
  (input = (Bx(V+H)), output = (Bx4H))
2. 3 pointwise sigmoid for coefficient calculation
3. 2 pointwise tanh for range limiters
4. 9 pointwise add for linear transformations
   8 batch-wise broadcast at the feedforward nodes
   1 for the hidden+state fuse
5. 2 pointwise mul for the filters




<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    TeX: {
      equationNumbers: {
        autoNumber: "AMS"
      }
    },
    tex2jax: {
      inlineMath: [ ['$','$'], ['\(', '\)'] ],
      displayMath: [ ['$$','$$'] ],
      processEscapes: true,
    }
  });
</script>
<script type="text/javascript"
        src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>


Let's test some inline math $x$, $y$, $x_1$, $y_1$.

Now a inline math with special character: $|\psi\rangle$, $x'$, $x^\*$.


1:

Test a display math:
$$
   |\psi_1\rangle = a|0\rangle + b|1\rangle
$$
Is it O.K.?


2:

Test a display math with equation number:
\begin{equation}
   |\psi_1\rangle = a|0\rangle + b|1\rangle
\end{equation}
Is it O.K.?


3:

Test a display math with equation number:
$$
  \begin{align}
    |\psi_1\rangle &= a|0\rangle + b|1\rangle \\
                   &= c|0\rangle + d|1\rangle
  \end{align}
$$
Is it O.K.?




| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |




5:

Test a display math with equation number:
\begin{align}
    |\psi_1\rangle = a|0\rangle + b|1\rangle
\end{align}
Is it O.K.?


6:

And test a display math without equaltion number:
\begin{align\*}
    |\psi_1\rangle &= a|0\rangle + b|1\rangle \\\\
    |\psi_2\rangle &= c|0\rangle + d|1\rangle
\end{align\*}
Is it O.K.?




Group                     | Domain          | First Appearance
------------------------- | --------------- | ----------------
ShinRa                    | Mako Reactors   | FFVII
Moogles                   | MogNet          | FFIII
Vana'diel Chocobo Society | Chocobo Raising | FFXI:TOAU




You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
