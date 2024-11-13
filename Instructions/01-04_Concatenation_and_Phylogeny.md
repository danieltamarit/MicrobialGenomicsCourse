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

Now, we have a set of alignments with identical names. We can concatenate them
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
$ phykit create_concatenation_matrix -h
~~~


Once we are done with Phykit, we return to the previous environment:
~~~
$ python2.7
~~~
