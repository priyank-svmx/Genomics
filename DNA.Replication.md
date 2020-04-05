# DNA Replication

## The Process

- At first glance, a computer scientist might not imagine that these details have any computational relevance
- To mimic the process in the above figure algorithmically, we only need to take a _string representing the genome and return a copy of it_
- Yet if we take the time to review the ***underlying biological process***, we will be rewarded with ***new algorithmic insights*** into analyzing replication
  
 > Replication begins in a `genomic region` called the `replication origin` (denoted `ori`) and is carried out by `molecular copy` machines called `DNA polymerases`

<hr/>

## Locating Ori

- ***Locating ori*** presents an important task not only for understanding how cells replicate but also for various biomedical problems
  - For example, some gene therapy methods use genetically engineered mini-genomes, which are called viral vectors because they are able to penetrate cell walls (just like real viruses
  - ***Viral vectors*** carrying artificial genes have been used in agriculture, such as to engineer frost-resistant tomatoes and pesticide-resistant corn
  - In 1990, gene therapy was first successfully performed on humans when it saved the life of a four-year-old girl suffering from Severe Combined Immunodeficiency Disorder; the girl had been so vulnerable to infections that she was forced to live in a sterile environment.

> The idea of gene therapy is to intentionally infect a patient who lacks a crucial gene with a `viral vector` containing an `artificial gene` that encodes a `therapeutic protein`. Once inside the cell, the `vector replicates` and eventually produces many copies of the `therapeutic protein`, which in turn treats the patient’s disease
> To ensure that the `vector` actually replicates inside the cell, biologists must know where `ori` is in the `vector’s genome` and ensure that the `genetic manipulations` that they perform ***do not affect it***

## Finding Ori

- In the following problem, we assume that a `genome` has a single `ori` and is represented as a `DNA string`, or a `string of nucleotides` from the `four-letter alphabet {A, C, G, T}`.

`Finding Origin of Replication Problem:

Input: A DNA string Genome.
Output: The location of ori in Genome.
STOP and Think: Does the Finding Origin of Replication Problem represent a clearly stated computational problem? (On "STOP and Think" questions, we encourage you to interact with other learners in the discussion forum below.)`

## NOT a well defined Computational Task

> Although the Finding `ori` Problem  does not present a well-defined computational problem
> Biologists would immediately plan an experiment to locate `ori`: for example, they might delete various `short segments` from the `genome` in an effort to find a segment whose deletion stops replication
> `Computer scientists`, on the other hand, would shake their heads and demand more information before they can even start thinking about the problem

## DnaA boxes

- Research has shown that the region of the bacterial `genome` encoding `ori` is typically a `few hundred nucleotides` long
- Our plan is to begin with a bacterium in which `ori` is known, and _then determine what makes this genomic region special_ in order to design a `computational approach` for finding ori in other bacteria

 > Indeed, we know that the `initiation` of replication is mediated by `DnaA`, _a protein_ that binds to a **short segment** within the `ori` known as a ***DnaA box***

- Think of the _`DnaA box`_ as a message within the `DNA` sequence telling the DnaA protein: _“bind here!”_

### The question is how to find this hidden message _without knowing what it looks like_ in advance — can you find it? In other words, can you find something that _stands out_ in `ori` ?__

``Hidden Message Problem: Find a “hidden message” in the replication origin

Input: A string Text (representing the replication origin of a genome).
Output: A hidden message in Text``

## Counting Words

> Key is observing how natural process is occuring !!

- Operating under the assumption that `DNA` is a `language` of its `own`
  - We can find any surprisingly _frequent_ "words" within the `ori` of Vibrio cholerae
  - We have added reason to look for frequent words in the `ori` because for various biological processes, `certain nucleotide` strings often appear `surprisingly often` in small regions of the `genome`
  - This is often because **certain proteins can only bind to DNA if a specific string of nucleotides is present**, and if there are more occurrences of the string, then it is more likely that `binding` will successfully occur
  - It is also less likely that a mutation will disrupt the binding process

> For example, `ACTAT` is a surprisingly frequent substring of `ACAACTATGCATACTATCGGGAACTATCCT`

- We will use the term `k-mer` to refer to a `string` of length `k` and define `Count(Text, Pattern)` as the number of times that a `k-mer` Pattern appears as a `substring` of Text
  - Following the above example,
      `Count(ACAACTATGCATACTATCGGGAACTATCCT, ACTAT) = 3`

## To Compute

- To compute `Count(Text, Pattern)`, our plan is to _“slide a window”_ down Text, checking whether each `k-mer` `substring` of Text matches `Pattern`
- We will therefore refer to the `k-mer` starting at position `i` of Text as `Text(i, k)`
- In this case, Text begins at position `0` and ends at position `|Text| − 1`
- `|Text|` denotes the number of symbols in Text
  - For example, if `Text = GACCATACTG`, then `Text(4, 3) = ATA`
  - Note that the last k-mer of Text begins at position |Text| − k, e.g., the last 3-mer of GACCATACTG starts at position 10 − 3 = 7

```PatternCount(Text, Pattern)
        count ← 0
        for i ← 0 to |Text| − |Pattern|
            if Text(i, |Pattern|) = Pattern
                count ← count + 1
  return count```
