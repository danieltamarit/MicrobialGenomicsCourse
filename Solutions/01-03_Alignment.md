ALIGNMENT
==============

In order to use this dataset to reconstruct a phylogenomic tree, you will need to:
- Align each marker separately
- Treat each alignment as deemed appropriate (e.g. remove gappy sites)
- Concatenate aliignments into a superalignment
- Reconstruct a phylogeny 

Go to the folder where you copied the study's Fasta files. Let's start by aligning
them using a fast aligner: 'famsa'. Check out how to run it by doing:
~~~
$ famsa -h
~~~

The help instructions clarify that this software just requires two arguments, the
first one being the input file (raw, unaligned sequences), and the second being the
name you wish to give the output file, which will contain the alignment. It is good
practice to name the output file just like the input file, but adding a suffix that
indicates the treatment that the input file has received. Here, for example, you can
name the output file "<input_file>.famsa".

This aligner should take only about 1 second per Fasta file. In order to run this
software on all of your files, you can run a 'for' loop:
~~~
$ for f in *fasta; do famsa $f $f.famsa; done
~~~

You should now have a number of additional files in your folder, containing the 
aligned sequences of the gene markers. Now, make sure that these files indeed 
contain alignments. If you read them with 'less', what signs do you observe that
the raw sequences have been aligned?

In order to visualise these alignments, you can read them with the parser tool ALAN.
Run (make sure to replace "< ALIGNMENT >" with the actual alignment file you want to 
visualise:
~~~
$ ~/data/phylogenomics/tools/alan_dt <ALIGNMENT>
~~~

What do you observe? Do these alignments look OK? (for example, do you see clear,
well-aligned columns? Are there many columns that represent mostly gaps?
> These alignments should indeed contain many columns that are clearly conserved (i.e. similar amino acids in the column).
> However, they also contain many positions that are extremely gappy. Very often these will accumulate in N- and C-termini.

Often, some sequence positions can be very difficult to align (e.g. protein domains
that evolve very fast, or that have suffered many insertions or deletions). Aligners
can make mistakes in these positions, and misalign columns, often by separating
homologous positions into multiple columns and placing together non-homologous
positions in the same column (often in the context of very gappy sequence regions).
And of course, this kind of errors can dramatically affect the detection of
phylogenetic signal by tree-reconstruction tools.

One way to avoid feeding misaligned positions to phylogenetic software is to
remove gappy alignment sites. Here, we can do that using trimAl. Again, check out
how to run it by doing:
~~~
$ trimal -h
~~~

Now, run trimAl for all computed alignments, in order to remove all sites that
are formed by over 50% of gaps. Make sure your command worked by looking at the
alignments, both using 'less' and using 'alan_dt'.
~~~
# The correct syntax to run trimAl could be:
$ for f in *.famsa; do trimal -in $f -out $f.tr05 -gt 0.5; done
~~~
