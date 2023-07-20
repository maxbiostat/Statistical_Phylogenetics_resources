## Resources for learning Statistical Phylogenetics

Sometimes students ask me how to learn statistical phylogenetics, and are usually concerned about the 'phylo' part. These notes are my attempt to point people in the direction of good resources. 

#### Books

-  [``SS2003``](https://books.google.com.br/books?hl=en&lr=&id=uR8i2qetjSAC&oi=fnd&pg=PA1&dq=phylogenetics+semple+steel&ots=_axt0_fnAT&sig=Xnsk6k1l5jBgnRhBEX8dE76-qfE&redir_esc=y#v=onepage&q=phylogenetics%20semple%20steel&f=false) Semple, C., & Steel, M. (2003). **Phylogenetics** (Vol. 24). Oxford University Press. 
    * This is a book written by mathematicians for mathematicians. A true classic.
- [``F2004``](https://global.oup.com/ushe/product/inferring-phylogenies-9780878931774?cc=br&lang=en&#:~:text=Inferring%20Phylogenies%20explains%20clearly%20the,and%20how%20they%20are%20used.) Felsenstein, J., & Felenstein, J. (2004). **Inferring phylogenies** (Vol. 2, p. 664). Sunderland, MA: Sinauer associates.
    * Written by one of the greatest phylogeneticists of all time, this book offers a population geneticist's to statistical inference of phylogenies.
- [``Y2006``](http://abacus.gene.ucl.ac.uk/CME/) Yang, Z. (2006). **Computational molecular evolution**. OUP Oxford.
    * The first of [Ziheng Yang](http://abacus.gene.ucl.ac.uk/ziheng/)'s books on Statistical Phylogenetics, still a solid choice. 
- [``Y2014``](http://abacus.gene.ucl.ac.uk/MESA/) Yang, Z. (2014). **Molecular evolution: a statistical approach**. Oxford University Press.
    * An improvement on  ``Y2006``, with a more modern and more statistical approach to phylogenetics. A great, mostly up-to-date reference. Stronger focus on Bayesian methods.
- [``DB2015``](https://doi.org/10.1017/CBO9781139095112) Drummond, A. J., & Bouckaert, R. R. (2015). **Bayesian evolutionary analysis with BEAST**. Cambridge University Press.
    * This book focuses on time-calibrated phylogenies and Bayesian inference of such objects _via_ Markov chain Monte Carlo.
- [``S2016``](https://www.math.canterbury.ac.nz/~m.steel/Non_UC/files/research/book.pdf) Steel, M. (2016). **Phylogeny: discrete and random processes in evolution**. Society for Industrial and Applied Mathematics.
    * This monograph updates `SS2003` with a decade-and-a-half's worth of mathematical results. Particularly useful for studying phylogenetic networks. 

### Topics

- **What are trees and how many are there?**

If you're looking for a rigorous construction of trees, chapters 2 and 3 of ``SS2003`` present a construction from first principles. Section 1.3.1 of [Carvalho (2019)](https://era.ed.ac.uk/handle/1842/35510) and Chapter 2 of ``DB2015`` address time-calibrated phylogenies specifically. Chapter 3 in `F2004` has a nice review on many counting results for various types of trees (rooted, unrooted, labelled and completely ordered histories). More combinatorial results can be found in Chapter 2 of `S2016`. 

- **How to compute the phylogenetic likelihood?**

Given a tree `T` and an alignment of DNA[^1] sequences `D`, how do I compute the likelihood `L(D|T)`? Since most DNA evolution models are based on [continuous-time Markov chains](https://en.wikipedia.org/wiki/Continuous-time_Markov_chain) (CTMCs), we need to evaluate a bunch of matrix exponentials **and** marginalise over all internal nodes. This is hard.  It turns out that there is a dynamic programming solution, called [Felsenstein's pruning algorithm (FPA)](https://en.wikipedia.org/wiki/Felsenstein%27s_tree-pruning_algorithm), ([Felsenstein, 1973](https://doi.org/10.1093%2Fsysbio%2F22.3.240)) that cleverly re-uses calculations and runs in `O(n^2)` time, where `n` is the number of leaves (taxa). To compute gradients of the likelihood w.r.t. the branch (edge) lengths one can employ a similar strategy in `O(n)` time. A nice discussion of the pruning algorithm and the gradients can be found in [Ji et al (2020)]( https://doi.org/10.1093/molbev/msaa130). For a textbook presentation of the FPA, see Chapter 4 in `Y2014`. As a curiosity, the FPA finds applications in other things, such as predicting the results of tournaments ([Bettisworth & Stamatakis, 2021](https://www.biorxiv.org/content/10.1101/2021.06.24.449715v1.full)). 

- **What about the prior?** 

Of course there are many possible priors  `pi(T)` for the tree, but a very popular choice is the coalescent process. There are various books and survey articles on the Kingman Coalescent (and extensions) such as Wakeley’s 2006 book (“An introduction to Coalescent Theory”) or the 2005 book by Hein et al. ("Gene Genealogies, Variation and Evolution – A Primer in Coalescent Theory”).
[This](https://www.youtube.com/watch?v=0j0jW0stbB8) lecture by [Magnus Nordborg](https://www.oeaw.ac.at/gmi/research/research-groups/magnus-nordborg) is quite helpful, as is his 2003 [chapter](https://www.fc.up.pt/mestr_biodiv/aulas/coalescent.pdf). 
Chapter 27 of `F2004` discusses a range of strategies for calculating the coalescent density (as well as maximum likelihood inference, which is not relevant here). 
The coalescent is part of a family of "exchangeable" priors on trees, called proportional to distinguishable arrangements (PDA), which have nice probabilistic properties. See [Aldous (1996)](https://link.springer.com/chapter/10.1007/978-1-4612-0719-1_1) and [Zhu, Than & Wu (2015)](https://doi.org/10.1007/s00285-014-0817-4) for more details. 
For a very statistical perspective on the coalescent as a *prior measure* (including its regularisation properties or lack thereof), see Chapter 2 of [Carvalho (2019)](https://era.ed.ac.uk/handle/1842/35510). 

[Here](https://github.com/maxbiostat/toy_coalescent) is a repository with R and [BEAST](https://beast.community/) code demonstrating how to do inference under a simple coalescent with five taxa. 

### Acknowledgements

I thank [Mike Steel](https://www.math.canterbury.ac.nz/~m.steel/) for sharing good resources for the coalescent. Thanks are also due to my students for prompting me to think harder about how to organise learning materials for Statistical Phylogenetics.

[^1]: Or RNA or aminoacid or any discrete trait, really.
