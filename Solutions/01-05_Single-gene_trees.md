Single-gene trees
==============

It is always good to double-check one's data to make sure that every 
step has been performed correctly. In today's lecture, we discussed 
how important it is to consider sequences that have followed the same
evolutionary history. Typically, one should reconstruct trees for 
every single gene marker used in a concatenation study, and make sure
that these trees are a priori compatible with each other. Often, lack
of signal will prevent us from identifying the same exact tree, but
we want to at least confirm that there are no clearly different 
histories included in our data.

Here, you should run a phylogenetic reconstruction for every gene
marker in this dataset. To reduce the amount of waiting times and
resources, do this only for the first five gene markers using FastTree
like you did earlier, and take the rest from the appropriate 'data' folder.

For each gene marker, summarise the results in a matrix, where:
- Every row is a gene marker
- Columns indicate whether:
  - Eukaryotes are monophyletic
  - Archaea are monophyletic
  - Bacteria are monophyletic
  - Is the tree consistent with the two-domains hypothesis
  - Is the tree consistent with the three-domains hypothesis

You can do this by visualising the trees in Figtree as before. One
possible alternative could be to visualise the trees faster, in your
terminal. To do this, it would be helpful to first root the tree
in midpoint position. Do it using a custom script in the 'tools'
folder:
~~~
$ python ~/data/phylogenomics/tools/midpoint_root.py <TREE_IN> <TREE_OUT>
~~~

Now, you can use the 'newick utils', a package of tree visualisation
and editing tools. To view your tree in the terminal, you can run:
~~~
$ nw_display -w 150 <TREE> | less
~~~

Note that the '-w' parameter adjusts the width of the tree to your
screen. Feel free to play around with that number, so the tree is 
appropriately fitted. If you make it too large, some leaf names will
go over the screen limit, resulting in every printed line becoming a
double line (visible as most of your tree being empty at every second
line).

> We will do this exercise together.
> These results should show that at least one of the markers, COG0012, has a different pattern than the rest. Here, eukaryotic sequences are much more similar to bacterial sequences than to archaeal sequences.
> The rest generally show that eukaryotic sequences are nested within Archaea. The exact position may not be conserved, given the long evolutionary distances and the low phylogenetic signal present in single genes.
