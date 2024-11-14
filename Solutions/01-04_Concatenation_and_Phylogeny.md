Concatenation and Phylogeny
==============

Now, it's time to add up the phylogenetic signal in the selected alignments
and reconstruct a phylogeny with it. We will need to concatenate the individual
alignments into a single, concatenated alignment first.

To do that, let's first edit our alignments so all sequences originating from
the same organisms are actually named identically. Look at the Fasta headers
and identify how you could remove any sequence-specific text from the header, 
so you only keep what is common to all sequences from the same organism.

Did you notice that everything that comes after the pipe ("|") is gene-specific?
By removing any text matching that symbol and anything that comes after it, we
can get that job done:
~~~
$ for f in <TRIMMED_ALIGNMENTS>; do sed 's/|.*//' $f > $f.short; done
~~~

Make sure to replace <TRIMMED_ALIGNMENTS> by your actual trimmed alignment files.
For example, if your trimmed alignments have the suffix "trimal50", you would do:
~~~
$ for f in *.trimal50; do sed 's/|.*//' $f > $f.short; done
~~~

Now we have a set of alignments with identical names. We can concatenate them
in many ways, but here we will use the package Phykit, which includes several
functions to work with alignments and phylogenies.

Because of the specifiic software requirements, you will need to load the 
python 3.11 environment first:
~~~
$ python3.11
~~~

Now, you can run Phykit as follows:
~~~
$ phykit -h
~~~

We want to use the function "create_concatenation_matrix". Thus:
~~~
$ phykit create_concatenation_matrix -h
~~~

You see that you need to create first a file containing a list of all the
alignments to be concatenated. You can simply do:
~~~
$ ls *short > list_of_alignments.txt
$ phykit create_concatenation_matrix -a list_of_alignments.txt -p concatenated_alignment
~~~

Once we are done with Phykit, we return to the previous environment:
~~~
$ python2.7
~~~

Let's evaluate the results by analysing the occupancy matrix, which indicates
how many taxa contained each one of the selected gene markers. In order to
read this file in the terminal, you can do:
~~~
$ column -t -s $'\t' concatenated_alignment.occupancy | less -S
~~~

How well represented are the selected gene markers? Are there any genes that
were not found in a very large fraction of genomes?
> Gene markers are present in the majority of the studied organisms. Most are found in 95% or more of the organisms, with only one at 79.9%


Now, the final step is to reconstruct a tree using this superalignment. This 
is of course a very difficult process that consumes a lot of computational
resources. Reconstructing a tree of very distant sequences requires using 
probabilistic frameworks (maximum likelihood, Bayesian inference), a thorough
exploration of tree topologies, using complex evolution models, and running
intensive processes to evaluate the robustness of the tree. Due to the
limitations in this course, we will take a shortcut and run a very fast 
alternative. We will take this into consideration when evaluating our results.
~~~
$ FastTree -lg concatenated_alignment.fa > concatenated_alignment.fa.fasttreeLG
~~~

This process will take a few minutes. Use this time to think once again about
what your results should look like. What do you expect this tree will show?

Once it is ready, copy your tree to your device and visualise it using 
Figtree, as you did the day before. Remember to:
- Select "Midpoint root" for easier visualisation
- Play with font sizes both for tip labels and branch labels (supports)

What shape of the tree of life does your tree support? 
> This tree should show Eukaryotes outside of Bacteria and Archaea (all three domains are monophyletic. It is consistent with the classical three-domains tree of life, indicating that eukaryotes do not originate from within Archaea.
