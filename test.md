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

If you’re like me, (or anyone who has ever used anvi’o’s glorious interactive interface *without* Meren or Tom sitting right next to them), then you’ve probably found yourself at some point wondering if these different views you’re exploring actually mean what you’ve convinced yourself they mean. Sure there are some pretty safe ones that you can rationalize to yourself with some confidence, like “Mean coverage” or “Mean coverage Q2Q3” for example. But even those that seem relatively straightforward, like “Relative abundance”, can be pretty tricky. (Relative to what? All samples? All splits?) And don’t even get me started on “Detection”! (Meren’s taken quite a bit of heat for this term’s ambiguity, and rightfully so, hehe.)

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


**Abundance** 
-	mean coverage of a split divided by overall sample mean coverage -
Abundance for a split is constrained to within one sample. In a sense this view is telling you that those splits with larger abundance values are more represented in that sample (i.e. recruited more reads) than those splits with smaller abundance values. And it does this by providing the ratio of that split’s mean coverage to that sample’s overall mean coverage incorporating all contigs. So if your abundance value is 2, that split’s mean coverage is twice that of the mean for all contigs in that sample.

**Relative abundance**
-	proportion of reads recruited to a split out of the total reads recruited to that split across all samples
Relative abundance considers one split across all samples. This will tell you in which sample a particular split recruited the most reads. Since it is normalized to the total number of reads recruited to split across all samples, values from all samples for a given split will always sum to 1. 

**Max-normalized ratio**
-	proportion of reads recruited to a split out of the maximum number of reads recruited to that split in any sample
This also considers one split across all samples. But in this case the value is normalized to the single maximum value for that split (as opposed to the sum as in relative abundance). Because of this the sample containing the split that contributed the max value will always equal 1, and the value for that split in the other samples will be the fraction of that max.

**Mean coverage**
-	average depth of coverage across split
Add up the coverage of each nucleotide in a split, and divide by the length of the split. 

**Mean overage Q2Q3**
-	average depth of coverage across split excluding nucleotide positions with coverage values falling outside of the interquartile range for that split
Calculated the same as mean coverage, except only incorporating those nucleotide coverage values that fall within 2nd and 3rd quartiles of the distribution of nucleotide coverages for that split. This can help smooth out the mean coverage visualization by removing nucleotide coverage values from the equation that may be outliers due to non-specific mapping. 

**Coverage STD**
-	the standard deviation of coverage values for a given split
This is constrained to an individual split in an individual sample, and represents the standard deviation of the nucleotide coverage values in that split. 

**Detection**
-	the proportion of that split that is covered at least 1X 
Detection gives you an idea of how much of the split actually recruited reads to it. The utility of this is most clearly demonstrated with the following figure. Samples 1 and 2 may have the same mean coverage (say ~50x). However, Sample_1’s detection would be 1 (as all nucleotides in the split are covered by at least one read), while Sample_2’s detection would be ~0.5. From the main interactive interface, mean coverage would appear to be consistent between these splits. But the detection view would show you at a glance that something funny is going on that probably needs a closer look. 

<div class="centerimg">
<a href="https://github.com/AstrobioMike/Misc/blob/master/detection_example.pdf"><img src="https://github.com/AstrobioMike/Misc/blob/master/detection_example.pdf" width="80%" /></a>
</div>

**Variability** 
-	single-nucleotide variants per kilobase
This gives you a view of SNV density of each split. This can give you an idea of how much variability there is in the reads that successfully recruit to that split. If resolving closely related populations of organisms is something you’re interested in, be sure to check out this and this. 

---

The capabilities of anvi’o are constantly expanding, but the heart of the interactive interface lies with facilitating the manual curation of metagenomic bins. All of these views utilizing different metrics are here to help in that effort of identifying which contigs/splits likely originate from a similar source. It’s certainly a good idea to take a peek at multiple views when refining your bins, so be sure to take advantage of them!
