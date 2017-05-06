---
layout: post
title: "Just what exactly do all those view options in the anvi’o interactive interface actually mean??"
excerpt: "Mike Lee demystifies the view options"
modified: 2017-05-06
categories: [anvio]
comments: true
authors: [mike]
---

<div class="centerimg">
<a href="https://github.com/AstrobioMike/Misc/blob/master/views.pdf"><img src="https://github.com/AstrobioMike/Misc/blob/master/views.pdf" width="80%" /></a>
</div>

If you’re like me, (or anyone who has ever used anvi’o’s glorious interactive interface without Meren or Tom sitting right next to them), then you’ve probably found yourself at some point wondering if these different views you’re exploring actually mean what you’ve convinced yourself they mean. Sure there are some pretty safe ones that you can rationalize to yourself with some confidence, like “Mean coverage” or “Mean coverage Q2Q3” for example. But even those that seem relatively benign, like “Relative abundance”, can be pretty tricky. (Relative to what? All samples? All splits?) And don’t even get me started on “Detection”! (Meren’s taken quite a bit of heat for this term’s ambiguity, and rightfully so, hehe.)

I’ve certainly sent my fair share of emails to the team asking to clarify a view I thought I had pinned down, and it turned out I was slightly (or completely) wrong. So last time I was in the same city as Meren I made sure he went over these with me, several times, in painstakingly repetitive detail for him I’m sure :). But I convinced him it was worth his time to do so by saying I’d make a blog post about it to hopefully help others too. So first here’s a quick reference table, and after that I’ll try to highlight some of the nuances in more detail and give examples where each can be particularly useful.

|View|Value|
|:---|:---|
|*Abundance*|mean coverage of a split divided by overall sample mean coverage|
|*Relative abundance*|# of reads recruited to a split divided by total reads recruited to that split across all samples|
|*Max-normalized ratio*|# of reads recruited to a split divided by the maximum number of reads recruited to that split in any sample|
|*Mean coverage*|average depth of coverage across split|
|*Mean coverage Q2Q3*|average depth of coverage excluding nucleotide positions with coverages in the 1st and 4th quartiles|
|*Detection*|proportion of nucleotides in a split that are covered at least 1X|
|*Coverage STD*|standard deviation of coverage for a given split|
|*Variability*|SNVs per kb|

|File Name|Content and Purpose|
|:---|:---|
|*genes.hmm.gz*|A gzip of concatenated HMM profiles.|
|*genes.txt*|A TAB-delimited file containing three columns; gene name, accession number, and source of HMM profiles listed in genes.hmm.gz.|
|*kind.txt*|A flat text file which contains a single word identifying what type of profile the directory contains. If this word is 'singlecopy', the profile is used to calculate percent completeness and contamination. Otherwise it will only be used to visualize contigs with HMM hits without being utilized to estimate completeness.|
|*reference.txt*|A file containing source information for this profile to cite it properly.|
|*target.txt*|A file containing the target alphabet and context. See [this](https://github.com/meren/anvio/pull/402) for more details. For this particular collection the target will be `AA:GENE` (because it was prepared using amino acid alignments, and we want them to be searched within gene calls stored in contigs databases), however, the the target term could be any combination of `AA`, `DNA`, or `RNA` for the alphabet part, and `GENE` or `CONTIG` for the context part (well, except `AA:CONTIG`, because we can't translate contigs).|


Examples of each file can be found [here](https://github.com/meren/anvio/tree/master/anvio/data/hmm/Campbell_et_al), and if you'd like to jump right in using the archaeal single-copy gene collection by [Rinke et al.](http://www.nature.com/nature/journal/v499/n7459/full/nature12352.html), please help yourself to the directory located [here]({{ site.url }}/files/Rinke_archaeal_HMM.tar.gz).

The following figure compares the completeness and contamination estimates for 5 archaeal and 3 bacterial genomes I pulled from [IMG](https://img.jgi.doe.gov/){:target="_blank"}. For each genome, the figure displays the estimations based on the default bacterial single-copy gene collections distributed with anvi'o, and Rinke et al.'s archaeal gene collection I added to my contigs database:

<div class="centerimg">
<a href="{{ site.url }}/images/anvio/2016-05-21-archaeal-single-copy-genes/archaea-anvio.png"><img src="{{ site.url }}/images/anvio/2016-05-21-archaeal-single-copy-genes/archaea-anvio.png" width="80%" /></a>
</div>

Not all that surprisingly, percent completeness estimates for the archaeal bins are rather poor when they are based on HMM profiles for bacterial single-copy genes. In contrast, when the archaeal profile is used, they are much more accurately evaluated.

---

If you are anything like me and many other fortunate researcher out there, you have already realized that not only is anvi'o incredibly user-friendly, which of course is nice, but also it can be an extremely powerful tool. This is largely due to it being designed with an underlying framework that can be easily manipulated (in small part exemplified here) and built upon. To be sure, while most of us are still barely scratching the surface as far as leveraging anvi'o's full potential, the team is busy adding more and more exceedingly wonderful functionality - definitely check out the[ CPR hunting]({% post_url miscellaneous/2016-04-17-predicting-CPR-Genomes %}){:target="_blank"} and [pangenomics]({% post_url anvio/2016-11-08-pangenomics-v2 %}){:target="_blank"} posts if you haven't yet!
