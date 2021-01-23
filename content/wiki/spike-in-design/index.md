---
title: "Considerations for designing calibration spike-ins"
authors: ["Michael McLaren"]
tags: [
  "spike-ins",
  "experimental design",
]
categories: []
date: 2020-12-03
lastmod: 2021-01-23
draft: true
---

*Status: Partial draft.*

Adding a cellular or DNA spike-in at a fixed or known concentration to each sample prior to community sequencing can be used to obtain calibrated estimates of the fold changes in absolute abundance across samples of all sequenced taxa.
This post lists some relevant considerations for designing spike-ins for this purpose.

See also a recent review (Harrison et al., 2020; doi:10.1111/1755-0998.13247) with more considerations and references to various studies that have used spike-ins.

## Cellular vs DNA spike-ins

The consideration here is similar to that for deciding between cellular and DNA mocks.
DNA spike-ins may be easier to construct and work with, but do not allow calibration to account for bias due to DNA extraction.
DNA spike-ins additionally do not allow accounting for marker-gene copy-number variation.

## The spike-in concentration

The concentration of the spike-in should be tuned based on the range of input sample concentrations.
The goal is that the (biased) relative abundances of the spike-in and native taxa can be simultaneously well-quantified in the sequencing data.
If the spike-in concentration is too low, then the randomness inherent in extraction, PCR, and sequencing may lead to few or no reads assigned to the spike-in and it will be impossible to precisely measure the spike-in relative abundance.
If the spike-in concentration is too high, then sequencing effort will be wasted on the spike-in and we will miss or be unable to precisely quantify low-frequency native taxa.

For example, if we are doing a bacterial 16S amplicon experiment, and we expect our samples to vary in bacterial concentration by up to an order of magnitude, then we might aim for the spike-in taxa to constitute between 3% and 30% of the reads in a sample.
Achieving this goal requires that we can first form some idea of the range of expected bacterial concentration in our samples, which can be hard to know a priori and may require measuring input concentrations for a set of samples (perhaps via plating, cytometry, or qPCR).

A complication is that there will typically be bias between the spike-in and the native taxa.
For example, the taxa in the Zymo spike-in have been fixed and stored in DNA/RNA Shield.
This preparation might make them easier to lyse and thus yield more DNA per cell than the native taxa.
Or, the spike-in taxa might have a larger than average number of 16S copies.
Either of these facts would increase the fraction of 16S reads coming from the spike-in taxa relative to native taxa for a given spike-in concentration.

The following approach may be effective for determining the appropriate spike-in concentration for a 16S experiment while accounting for spike-in/native bias that arises from storage, extraction, and copy-number variation.
Perform the chosen extraction protocol on the spike-in and on a range of natural samples and measure the 16S concentration via qPCR.
(Just relative DNA concentration estimates are needed.)
Dividing the measured 16S concentrations for the spike-in by those of the native samples gives an estimate of the ratio of 16S reads if the spike-in were used in that concentration.
Since this estimate is based on the number of 16S copies post DNA extraction, it naturally accounts for bias due to DNA extraction and 16S copy-number variation mentioned above, in a way that quantification based on cytometry would not.

The spike-in concentration need not be the same in all samples, as long as we know how it varies across them.
So, if we have two sample types, one of which has a lower bacterial concentration, we can use a diluted (or lower volume) spike-in for that sample type.
Alternatively, if we want to allow for having a wide range (e.g. 30-100 fold) of input concentrations without needing (or being able to) predict which are the higher and lower samples, we could measure each microbiome sample in duplicate, with one duplicate getting a low-concentration spike-in and the other a high-concentration spike-in.

## Choice of strains

Spike-in strains should be distinct from taxa that can plausibly be found in your samples, and must be measurable by your sequencing method.
So for a 16S amplicon experiment, these taxa should be amplifiable by your chosen primers and have distinct amplicon sequences from taxa that might naturally appear in your samples.

**Commercial spike-ins:**
[Zymo](https://www.zymoresearch.com/collections/zymobiomics-microbial-community-standards) now offers commercial cellular spike-ins in two concentrations designed for studies of human gut microbiomes or gut-associated taxa.
