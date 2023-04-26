## Resources for learning Statistical Phylogenetics

Sometimes students ask me how to learn statistical phylogenetics, and are usually concerned about the 'phylo' part. These notes are my attempt to point people in the direction of good resources. 

#### Books


-  [``SS2003``](https://books.google.com.br/books?hl=en&lr=&id=uR8i2qetjSAC&oi=fnd&pg=PA1&dq=phylogenetics+semple+steel&ots=_axt0_fnAT&sig=Xnsk6k1l5jBgnRhBEX8dE76-qfE&redir_esc=y#v=onepage&q=phylogenetics%20semple%20steel&f=false) Semple, C., & Steel, M. (2003). Phylogenetics (Vol. 24). Oxford University Press. 
    * This is a book written by mathematicians for mathematicians. A true classic.
- [``Y2006``]() 
- [``Y2014``]() 
- [``DB2015``](https://doi.org/10.1017/CBO9781139095112) Drummond, A. J., & Bouckaert, R. R. (2015). Bayesian evolutionary analysis with BEAST. Cambridge University Press.
    * This book focuses on time-calibrated phylogenies and Bayesian inference of such objects _via_ Markov chain Monte Carlo.
- 

### Specific topics

- **What are trees?**

If you're looking for a rigorous construction of trees, chapters 2 and 3 of ``SS2003`` present a construction from first principles. Section 1.3.1 of [Carvalho (2019)](https://era.ed.ac.uk/handle/1842/35510) and Chapter 2 of ``DB2015`` address time-calibrated phylogenies specifically.

- **How to compute the phylogenetic likelihood?**

Given a tree `T` and an alignment of DNA[^1] sequences `D`, how do I compute the likelihood `L(D|T)`? Since most DNA evolution models are based on [continuous-time Markov chains](https://en.wikipedia.org/wiki/Continuous-time_Markov_chain) (CTMCs), we need to evaluate a bunch of matrix exponentials **and** marginalise over all internal nodes. This is hard.  It turns out that there is a dynamic programming solution, called [Felsenstein's pruning algorithm (FPA)](https://en.wikipedia.org/wiki/Felsenstein%27s_tree-pruning_algorithm), ([Felsenstein, 1973](https://doi.org/10.1093%2Fsysbio%2F22.3.240)) that cleverly re-uses calculations and runs in `O(n^2)` time, where `n` is the number of leaves (taxa). To compute gradients of the likelihood w.r.t. the branch (edge) lengths one can employ a similar strategy in `O(n)` time. A nice discussion of the pruning algorithm and the gradients can be found in [Ji et al (2020)]( https://doi.org/10.1093/molbev/msaa130). For a textbook presentation of FPA, see Chapter 4 in `Y2014` . 


[^1]: Or RNA or aminoacid or any discrete trait, really.
