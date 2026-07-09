---
layout: page
title: Program BioVis@ISMB
permalink: /program_ismb/
back_title: ISMB
back_url: ismb
---

# BioVis@ISMB 2026 Program

{{ site.ismb_cosi_date }}

## Invited Speakers

### The Visual Genome: An attempt to classify multi-omics visualization

<figure class="speaker-photo">
    <img src="{{ site.baseurl }}/images/speakers/jean_fan.jpg" alt="Jean Fan" />
    <figcaption>Jean Fan</figcaption>
</figure>

[Jean Fan](https://jean.fan/), Johns Hopkins University, USA

**Abstract:**
Advances in high-throughput spatial transcriptomics (ST) technologies enable
high-throughput molecular profiling of cells while maintaining their spatial
organization within tissues. Such high-throughput ST data demand new
computational analyses and visualization approaches to identify and highlight
genes that spatially change in their expression patterns between conditions,
such as in diseased versus healthy tissues. In this talk, I will provide an
overview of the latest ST computational analysis methods developed by my lab. In
particular, to facilitate spatial molecular comparisons across structurally
matched tissue sections from replicates, case-control settings, and within and
across technologies, we previously develop STalign to align ST datasets in a
manner that accounts for partially matched tissue sections and other local
non-linear distortions using diffeomorphic metric mapping. Likewise, to enhance
the scalability of ST data analysis, we developed a rasterization preprocessing
framework called SEraster that aggregates cellular information into spatial
pixels. More recently, we developed STcompare to integrate STalign and SEraster
into a statistical framework for comparative analysis of ST data by testing for
and visualizing differences in spatial correlation and spatial fold-change
across structurally matched locations while robustly controls for false
positives even in the presence of spatial autocorrelation common in ST data.
Alternatively, to facilitate spatial molecular comparisons across structurally
unmatched tissues, we previously developed CRAWDAD, Cell-type Relationship
Analysis Workflow Done Across Distances, to quantify and visualize cell-type
spatial relationships across multiple length scales. We have applied CRAWDAD to
compare cell-type spatial organizations across samples as well as across
functional tissue units within samples. Overall, we anticipate that such
computational methods for analyzing and visualizing trends in ST data will
contribute to important biological insights regarding spatial molecular changes
across comparative axes of interest.

**Speaker Bio:**
Jean Fan is an associate professor of Biomedical Engineering in the Center for
Computational Biology at Johns Hopkins University. Her research team, the
JEFworks lab, is interested in understanding the molecular and
spatial-contextual factors shaping cellular identity and heterogeneity. She
develops new open-source computational software for analyzing spatially-resolved
multi-omic and imaging data that can be tailored and applied to diverse cancer
types and biological systems. Dr. Fan is also the founder, director, and lead
software developer for the non-profit organization CuSTEMized, which provides
personalized STEM picture storybooks to encourage young girls to see themselves
as scientists. She also serves as a Genomics section editor for PLoS
Computational Biology. The impact of Dr. Fan’s work has been recognized by
several awards and honors, including the Forbes 30 Under 30, the Nature Research
Award for Inspiring Science, the NSF CAREER Award, and the Presidential Early
Career Award for Scientists and Engineers (PECASE).

### Healthy skepticism in AI: a BioVis research agenda

<figure class="speaker-photo">
    <img src="{{ site.baseurl }}/images/speakers/liz_marai.avif" alt="Liz Marai" />
    <figcaption>Liz Marai</figcaption>
</figure>

[Liz Marai](https://www.evl.uic.edu/marai/home/index.html), University of Illinois Chicago, USA

**Abstract:**
Data visualization for Artificial intelligence (AI) research has historically
focused on enhancing trust through visual explanations of AI, under the
assumption that humans are critical users and unlikely adopters of AI. It is
becoming clear that, in reality, human trust-levels in AI span a wide range,
from critical to nearly blind acceptance. This talk will describe my group’s
work in developing AI-powered computational oncology models, with a focus on the
benefits and risks of AI solutions. I will then argue that the data
visualization field should support both trust and healthy skepticism in AI
solutions, while also being especially equipped to make AI models better
colleagues to the human.

**Speaker bio:**
Liz Marai is a professor of Computer Science, and a designated University of
Illinois Scholar. Marai's research has been recognized by multiple prestigious
awards, including a Test of Time Award, an NSF CAREER Award and several
multi-site NSF and NIH awards as a lead investigator. She is the director of the
UIC Institute for Health Data Science Research, and a chartered member of the US
National Institutes of Health study section on clinical informatics and digital
health. She has co-authored scientific open-source software adopted from Ghana
to Canada, and she is an inventor whose ideas have been embedded into a medical
instrument.

## Program

{% include_relative program_ismb_timetable.html %}
