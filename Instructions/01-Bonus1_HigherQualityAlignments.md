Higher Quality Alignments
==============

Due to the limitations of this tutorial, we have been taking
some methodological shortcuts. For example, for this exercise
we have been using an ultra-fast aligner, FAMSA. One may wonder
if other aligners would achieve the same conclusions, or if
perhaps differences in aligner algorithms may introduce enough
errors that the main findings cannot be replicated.

Assess whether you observe differences uusing different
aligners. Here, you can explore:
- MAFFT-LINSI. This is a specific algorithm within the common
alignment software MAFFT, which maximises accuracy by refining
a local alignment. It is best suited for one-domain proteins.
~~~
$ mafft-linsi -h
~~~
- MAFFT-EINSI. This is a different algorithm within the MAFFT
suite, which allows for large gaps within the sequence, and
therefore can accommodate proteins with multiple domains.
~~~
$ mafft-einsi -h
~~~

Explore the effects that these aligners have on the gene markers
used in this exercise. You can do the alignments as previously, 
or take them from the 'data' folder.

Do you observe any differences?

