Recoding
==============

In deep-evolution phylogenomics, we want to maximise the analysis focus on deep evolutionary
signal. In other words, as some genes and positions evolve relatively fast, they may have 
accumulated too many substitutions to be adequate for deep phylogenomics. There are several
techniques that allow mitigating this effect. First, we need to focus our analyses on genes
that evolve relatively slow. Then, we may want to evaluate the effect of fast-evolving sites.
Here, we will test the alignment treatment known as Recoding.

Alignment recoding in phylogenomics is a technique used to transform amino acid sequence 
alignments to mitigate biases such as compositional heterogeneity or saturation, that can 
mislead phylogenetic inference. By recoding sequences, for example, through Dayhoff coding 
(grouping amino acids based on biochemical properties) or through Susko-Roger coding (grouping
amino acids to minimise the probability of saturation), this approach reduces the impact of 
convergent evolution or site-specific evolutionary constraints. The recoding process minimizes 
instances where unrelated species appear similar due to parallel evolution rather than shared 
ancestry, thereby enhancing the robustness of phylogenetic analyses.

Here, we will use recode our concatenated alignment to 4 categories of amino acids in order
to minimise chances for saturation (SR4). You can do that using Phykit and the amino acid
categories in the 'data' folder:
~~~
$ python3.11
$ phykit recode -c ~/data/phylogenomics/tools/S_and_R-4.txt <ALIGNMENT> > <ALIGNMENT>.sr4
$ python 2.7
~~~

Visualise your alignment. Does it make sense?

Once your alignment has been recoded, you can reconstruct a phylogeny. Since your alignment
is not encoded by amino acids anymore, protein substitution matrices don't apply. Here, you
can use a 'nucleotide' algorithm instead:
~~~
$ FastTree -nt -gtr <RECODEDALIGNMENT>
~~~
> In this case, recoding seems to suggest that Eukaryotes originated from within Asgard archaea. Most likely, our ancestor was an Asgard archaeon belonging to the group Heimdallarchaeia. 

What differences do you observe in your results?
