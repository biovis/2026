---
layout: page
title: Bio+MedVis Challenge - Adaptive Molecular Dynamics Analysis
permalink: /biovisChallenges_vis/challenge_1/
---

# Analysis of conformational states in adaptive molecular dynamics simulations

Adaptive molecular dynamics (MD) simulation is a technique used to explore the vast and complex conformational space of proteins. Where traditional MD simulations may get "stuck" in local energy minima, failing to capture rare structural transitions, adaptive sampling overcomes this by running multiple shorter simulations in parallel. After each batch of simulations (called an epoch), the simulation data is analyzed on-the-fly, and new starting points (seeds) for the next round of simulations are adaptively selected based on specific metrics (e.g., distances, angles, mean deviation, etc.). This encourages the exploration of less-visited yet important regions of the protein's energy landscape. All simulations from all epochs are then studied to assess changes or transitions in the conformations and other properties of the simulated molecular system. One of the approaches used to aid with this analysis is Markov state model (MSM) analysis [1], which clusters the spatial conformations observed during the simulation into similar states and characterizes the transitions between them.

In this challenge dataset, the method is applied to assess the effects of the ongoing phase 3
therapeutics tramiprosate (TMP) and its metabolite 3-sulfopropanoic acid (SPA) on the disordered Aβ42 peptide involved in Alzheimer’s disease [2]. First, molecular dynamics trajectories were generated using adaptive sampling MDs. Then, using the VAMnets approach [3], ensembles of MSMs were learned for each molecular system (Aβ42, Aβ42 + TMP, and Aβ42 + SPA) using unsupervised machine learning to cluster conformations and analyze transitions between different conformational states.

The domain experts explored this data via the following series of static charts and a simple interactive visualization. Figure 1 illustrates the distribution of the simulations over time, where each row corresponds to one MD simulation, aligned based on the time of its starting frame. On the left, the color indicates their corresponding epochs, and on the right, the assigned conformation states. It provides an overview of the temporal coverage of the sampling.

<div style="width: 80%; margin: 0 auto;">
<div style="display:grid; grid-template-columns:repeat(auto-fit, minmax(280px, 1fr)); gap:1rem; align-items:start;">
    <figure style="margin:0;">
        <img src="{{site.baseurl}}/images/biovis-challenge/image5.png" alt="simulations over time" style="width:100%; height:auto;" />
    </figure>
    <figure style="margin:0;">
        <img src="{{site.baseurl}}/images/biovis-challenge/image4.png" alt="simulations over time" style="width:100%; height:auto;" />
    </figure>
</div>
<figcaption style="text-align: center;">
    Figure 1: Distribution of the simulations over time. Each row corresponds to one MD simulation. Left: colored by epochs. Right: colored by the assigned conformation states.
    </figcaption>
</div>

The trajectories can be concatenated by joining simulations from different epochs at respective time frames (seeds) into longer continuous trajectories, as illustrated in Figure 2.
<div style="width: 80%; margin: 0 auto;">
<div style="display:grid; grid-template-columns:repeat(auto-fit, minmax(280px, 1fr)); gap:1rem; align-items:start;">
    <figure style="margin:0;">
        <img src="{{site.baseurl}}/images/biovis-challenge/image1.png" alt="concatenated" style="width:100%; height:auto;" />
    </figure>
    <figure style="margin:0;">
        <img src="{{site.baseurl}}/images/biovis-challenge/image3.png" alt="concatenated" style="width:100%; height:auto;" />
    </figure>
</div>
<figcaption style="text-align: center;">
    Figure 2: Concatenated trajectories. Left: colored by epochs. Right: colored by the assigned conformation states.
    </figcaption>
</div>

The overall proportions of learned Markov states in the entire ensemble can then be assessed as shown in Figure 3. Here, the opacity encodes the number of trajectories at the corresponding time (X axis), the color indicates the assigned state, and the Y axis shows the proportion of trajectories with the given Markov state.

<div >
    <figure style="margin:0;">
        <img src="{{site.baseurl}}/images/biovis-challenge/image7.png" alt="concatenated" style="width:45%; height:auto;" />
    </figure>
    <figcaption style="text-align: center;">
    Figure 3: Top: Overall proportions of learned Markov states. Bottom: Total number of trajectories at the corresponding time (X axis).
    </figcaption>
</div>

Finally, the experts can interactively view the individual MD trajectories and observe how the molecular systems transition between individual states. This is done in a visualization (Figure 4) consisting of (a) a 3D view depicting the conformation of the molecule at a selected time point, (b) the conformation landscape view with a Markov state flow graph (here, each node corresponds to one identified state, the size of the node indicates the prevalence of the state in the entire ensemble, and the thickness of the edges indicates the transition probability) overlaid over the free energy projection (grayscale map), and (c) a timeline overview that indicates the currently selected timeframe and the state probability (each row corresponds to one state and the opacity indicates the state probability). The image below shows the simulation in the first frame, where the system is in state 0 (pink). During the interactive viewing of the trajectory, a point on the free energy landscape (b) would indicate the position of the current frame within the landscape.

Note that this last visualization (Figure 4) also includes data that are not part of this challenge. Namely, the free energy depicted in Figure 4 (b) is not provided. Furthermore, the state assignments are binary (i.e., each timeframe is assigned a single state rather than a probability of a state as indicated in Figure 4 (c)). However, the visualization can serve as an inspiration for the challenge submissions.

<div style="width: 60%; margin: 0 auto;">
<div style="display: flex; flex-direction: column; gap: 1rem;">
    <div style="display: flex; gap: 1rem;">
        <figure style="margin: 0; flex: 1;">
                    <img src="{{site.baseurl}}/images/biovis-challenge/image8.png" alt="3D" style="width: auto; height: 200px;" />
                <figcaption style="text-align: center;">(a)</figcaption>
                </figure>
                <figure style="margin: 0; flex: 1;">
                    <img src="{{site.baseurl}}/images/biovis-challenge/image6.png" alt="landscape" style="width: 100%; height: auto; object-fit: contain;" />               
                <figcaption style="text-align: center;">(b)</figcaption> 
                </figure>
    </div>
    <figure style="margin: 0;">
        <img src="{{site.baseurl}}/images/biovis-challenge/image2.png" alt="timeline" style="width: 80%; height: auto;" />
    <figcaption style="text-align: center;">(c)</figcaption>
    </figure>
</div>
<figcaption style="text-align: center;">
    Figure 4: Interactive visualization of a trajectory. (a) 3D view of the molecule conformation. (b) Confirmation landscape view with a Markov state flow graph overlaid over the free energy projection. (c) Timeline overview.
    </figcaption>
</div>


## Tasks

While the visualizations described above are very useful, they are limited to static summaries or interactive viewing of a single trajectory. However, the domain experts are interested in exploring the Markov states, conformations, and transition patterns across entire ensembles of trajectories and reasoning about the observed behavior. There is already a significant body of work on molecular dynamics visualization that can serve as an inspiration [4,5,6], but it does not fully address the needs of this analysis.

We thus challenge you to address one or multiple of the following tasks:

- **T1: Provide a better overview of the simulation ensembles.** This can include designing completely novel visualizations or proposing interactions to enhance existing visualizations. For example, consider how to improve an overview of Markov state transition patterns, transition rates, and conformation landscape in summary or over time. 
- **T2: Interactive grouping and comparison.** Support interactive exploration of the data. Instead of focusing on the interactive visualization of a single trajectory, focus on the analysis of transition patterns in groups of trajectories. For example, support grouping of trajectories (including concatenated trajectories) with similar behavior or temporal alignment of trajectories based on state transitions. Consider visualization and interaction methods to aid comparison of trajectories within and between clusters or even between different systems (e.g., simulations with TMP and simulations with SPA - see data description). So far, the experts have compared the data using statistical methods and side-by-side comparison of static figures. Can this be improved? 
- **T3: Support reasoning.** Which conformational changes are responsible for Markov state assignment? Which frame, or rather multiple frames, are most representative of a Markov state? Which amino acid residues are interacting (i.e., in close proximity) with each other or with other molecules (i.e., TPM, SPA) in different Markov states? Where are those interactions happening? Incorporate additional measures, such as residue interactions or root-mean square deviation (RMSD) of atomic positions, and connect abstract and spatial representations to support reasoning about state assignments and behavior of the molecules.
 
Note that while some of the tasks involve the design of an interactive visualization system, we also welcome submissions with a smaller scope, such as sketches of novel visualizations and prototypes that do not have to be fully developed.

## Data
The data for the challenge comes from a study assessing the effects of drug candidates on disordered biomolecules [2], consisting of simulations of three systems:
- Free Aβ42 peptide - ZS-ab2  
- Aβ42 peptide with tramiprosate (TPM) - ZS-ab3  
- Aβ42 peptide with 3-sulfopropanoic acid (SPA) - ZS-ab4 

#### Trajectories
The full data can be found at: [https://data.ciirc.cvut.cz/public/projects/2023CoVAMPnet/](https://data.ciirc.cvut.cz/public/projects/2023CoVAMPnet/)

From this data, you will need the folder `trajectories`, which contains the simulated trajectories. The remaining folders are not necessary for the challenge. In the `trajectories` folder, you will find three subfolders, each for one of the simulated systems. Each system was simulated over 16 epochs, and each epoch consisted of 20 simulations lasting up to 2000 frames (some simulations stopped early and are thus shorter). Each system folder contains the PDB file defining the structure of the molecules and simulation folders with [.xtc](https://manual.gromacs.org/archive/5.0.4/online/xtc.html) file encoding the MD trajectory (the format is widely supported in visualization and analysis tools such as VMD, MDAnalysis, and MDTraj). The simulation folder names adhere to the following convention:
`e<epochID>s<simulationID>_e<startEpochID>s<stratSimulationID>p0f<startFrameID>`  
where `startEpochID`, `stratSimulationID`, and `startFrameID` indicate the simulation and frame at which the new simulation starts.

#### State assignments
In addition to the trajectories, you will need state assignments. While these can be extracted from the full data, we provide a preprocessed version for easier matching with trajectories here: [https://gitlab.fi.muni.cz/visitlab/bio-medvis-challenge-2026/](https://gitlab.fi.muni.cz/visitlab/bio-medvis-challenge-2026/)

This repository contains three folders, one for each system. In each folder, you will find several files. Most importantly, the state assignments can be found in the files `zsabX_statesY.txt`, where `X` denotes the system and `Y=2,3,` or `4` represents the number of states in the Markov state model parametrization (in each parametrization, the conformations were clustered in 2,3, or 4 states, respectively). The format is the following:  
`Name_of_the_simulation : <list_of_states_for_each_frame>`  
For example:  
`e10s5_e5s11p0f1123: 0,0,0,0,0,0,0,0,0,0,0,0,2,0,0,0,2,2,2,0,0,0,2,2,2,2,2,2,0,2,2,2,0,2,2,...`  
means that the first 12 frames in the trajectory from simulation 5 in epoch 10 are assigned Markov state 0, the next one has Markov state 2, the next three have Markov state 0, the next three have Markov state 2, etc.

The remaining files contain the following information:
- zsabX_names.txt - list of simulated trajectories 
- zsabX_order.txt - simulations ordered in time; each row has the following format:  
`timestep_of_simulation_start : name_of_the_simulation` 
- zsabX_concatenated.txt - concatenated trajectories; each paragraph contains a list of simulations concatenated into a single trajectory, where each row denotes the simulation and its respective timeframes used in the concatenated trajectory in the format:  
`timestep_start - timestep_end : name_of_the_simulation`  
For example:  
`0-1759:	e1s4_0`  
`0-1226:	e5s6_e1s4p0f1759`  
`0+:		e15s11_e5s6p0f1226`  
means that the concatenated trajectory consists of the first 1759 frames of simulation e1s4_0, followed by the first 1226 frames of simulation e5s6_e1s4p0f1759, and finally by all frames of simulation e15s11_e5s6p0f1226. Note that the chaining can also be derived from the names of the simulation folders.
    
The implementation of the system used to obtain this data, along with some of the visualizations, can be found here: [https://github.com/KoubaPetr/CoVAMPnet/](https://github.com/KoubaPetr/CoVAMPnet/)

## Acknowledgment
This challenge was prepared in collaboration with researchers from  Loschmidt Laboratories, Department of Experimental Biology and RECETOX, Faculty of Science, Masaryk University, and Czech Institute of Informatics, Robotics and Cybernetics, Czech Technical University in Prague, who kindly provided the data and expertise.

## Related Work
[1] Scherer, M. K., Trendelkamp-Schroer, B., Paul, F., Pérez-Hernández, G., Hoffmann, M., Plattner, N., ... & Noé, F. (2015). PyEMMA 2: A software package for estimation, validation, and analysis of Markov models. *Journal of chemical theory and computation*, 11(11), 5525-5542. [https://doi.org/10.1021/acs.jctc.5b00743](https://doi.org/10.1021/acs.jctc.5b00743)

[2] Marques, Sérgio M., et al. CoVAMPnet: comparative Markov state analysis for studying effects of drug candidates on disordered biomolecules. *JACS Au*, 2024, 4.6: 2228-2245. [https://doi.org/10.1021/jacsau.4c00182](https://doi.org/10.1021/jacsau.4c00182)

[3] Mardt, A.; Pasquali, L.; Wu, H.; Noé, F. VAMPnets for Deep Learning of Molecular Kinetics. *Nat. Commun* 2018, 9 (1), 5. [https://doi.org/10.1038/s41467-017-02388-1](https://doi.org/10.1038/s41467-017-02388-1)

[4] Ulbrich, P., Waldner, M., Furmanová, K., Marques, S. M., Bednář, D., Kozlíková, B., & Byška, J. (2022). sMolBoxes: Dataflow model for molecular dynamics exploration. *IEEE Transactions on Visualization and Computer Graphics*, 29(1), 581-590. [https://doi.org/10.1109/TVCG.2022.3209411](https://doi.org/10.1109/TVCG.2022.3209411)

[5] Belghit, Hayet, Mariano Spivak, Manuel Dauchez, Marc Baaden, and Jessica Jonquet-Prevoteau. "From complex data to clear insights: visualizing molecular dynamics trajectories." *Frontiers in Bioinformatics* 4 (2024): 1356659. [https://doi.org/10.1016/j.jmb.2018.09.004](https://doi.org/10.1016/j.jmb.2018.09.004)

[6] Kozlíková, B., Krone, M., Falk, M., Lindow, N., Baaden, M., Baum, D., ... & Hege, H. C. (2017, December). Visualization of biomolecular structures: State of the art revisited. In *Computer Graphics Forum* (Vol. 36, No. 8, pp. 178-204). [https://doi.org/10.1111/cgf.13072](https://doi.org/10.1111/cgf.13072)


## Questions?

Please feel free to send any questions to: [biovis_challenge@ieeevis.org](mailto:biovis_challenge@ieeevis.org).

Chairs of the Bio+MedVis Challenge @ IEEE VIS 2026:

-   [Katarina Furmanova](https://www.muni.cz/en/people/374538-katarina-furmanova), Masaryk University, Czech Republic
-   [Daniel Haehn](https://danielhaehn.com/), University of Massachusetts Boston, USA
-   [Robert Krueger](https://kruegert.github.io/), New York University, USA

<!--
### Sunday, November 2, 2025, 9:00 AM - 12:30 PM (CET)

### Keynote Talk

<figure class="speaker-photo" style="width: min(35vw, 13em);">
    <img src="https://sbruckner.github.io/assets/img/StefanBruckner-800.webp" alt="Stefan Bruckner" />
    <figcaption>Stefan Bruckner</figcaption>
</figure>

**From Rendering to Reasoning: Evolving Visualization for Life Sciences**  
_[Stefan Bruckner](https://sbruckner.github.io/), Professor, Chair of Visual Analytics, University of Rostock, Germany._

**Talk Abstract:** In the past decades, visualization in the life sciences has matured from a focus on making images to a deeper mission of making sense. In this talk, I examine this evolution through the lens of human-computer collaboration: how we moved from raw rendering, to interpretable visual representation, to interactive co-exploration, and finally to reasoning and communication at scale. Along this trajectory, visualization has expanded its role from a technical enabler of data display to an intellectual partner in discovery and decision-making. The talk highlights key milestones, examples, and open challenges that illustrate how visualization increasingly serves as a medium for shared reasoning between humans, data, and intelligent systems.

## Program

[View the program and submissions here]({{site.baseurl}}/program_ieee/).


## Challenges

-   [Redesign Challenge](#redesign-challenge-redesign-an-existing-visualization)
-   [3D Microscopy Imaging Challenge](#3d-microscopy-imaging-challenge-from-a-raw-imaging-volume-to-biological-findings)
-   [Submission](#submission)

## Redesign Challenge: Redesign an Existing Visualization

### Background and Data Description

<p style="float: right; width: 30%; margin-left: 1em;">
<img src="{{site.baseurl}}/images/biovis-challenge/biomedvis2025-graphic.avif" alt="Bio+MedVis Teaser" style="width: 100%">
</p>

With 1 in 3 people affected, neurological conditions are the leading cause of
illness and disability worldwide, per the World Health Organization \[1\]. Early
detection and diagnosis of such conditions that include Alzheimer’s or
Parkinson’s disease are key to treatment and improved patient outcomes.
Acquisition methods alongside standard imaging methods such as magnetic
resonance imaging (MRI), are essential to support clinical researchers and
point-of-care medical staff. Such methods are often capable of detecting subtle
biochemical changes marking neurological abnormalities unidentifiable in medical
imaging.

**Magnetic resonance spectroscopy (MRS)** is one such acquisition method,
allowing for non-invasive assessment of tissue biochemistry that is essential
for tumor and radiotherapy studies in addition to early detection of other
neurodegenerative disorders.

While magnetic resonance imaging (MRI) produces a stack of high-resolution
anatomical images, MRS trades spatial for chemical information to produce a
spectral graph of localized concentrations of biochemical compounds known as
metabolites. Metabolites are indicated as one or multiple peaks of varying
signal intensities on the spectral graph, arranged by resonance frequency due to
the properties of the atomic nucleus used for the study. Generally speaking,
every metabolite can be identified by its **chemical shift**, i.e., its
difference in resonance frequency relative to a particular reference metabolite.

While hydrogen (1H) MRS is common, phosphorus (31P) is particularly useful in
cases where clinicians are interested in questions related to cellular
metabolism and oxidative stress, which are markers for a range of
neuropathological conditions \[3\]. Although these technologies have been
available for several years, technological advances are yielding new
opportunities to explore the metabolic changes in brain development and aging,
which in turn could yield new therapeutic approaches.

Illustrated below in **Fig. 1**, 31P-MRS is captured per-voxel with a structural
MR image that provides essential context for the location of each spectral
voxel. Following acquisition, model fitting and spectral quantification in
standard analysis tools results in a single spectral output graph containing
approximately 10 or fewer spectral peaks. Visualization standard practice for
this data is often limited to drawing the spectral graph, and the learning curve
to interpreting such data is steep – even in a successful acquisition, spectral
peaks can be difficult to identify and meaningful relationships are difficult to
understand. It is additionally important to clearly communicate the presence of
possible error or outliers to help researchers and clinicians understand whether
these issues arise from problems with data acquisition and processing, or if, in
the case of outliers, further exploration is meaningful. These challenges are
largely unmet in current clinical tools, and within the visualization community
research has mainly focused on 1H-MRS with different clinical considerations
\[6,7\]. It is difficult for researchers to learn to interpret these data, let
alone to interactively compare relative biochemical concentrations between
patients or at different times to understand metabolic changes or oxidative
stress.

<figure>
    <img src="{{site.baseurl}}/images/biovis-challenge/acel14005-fig-0003-m.avif" alt="31P-MRS Spectral Output" />
    <figcaption>
        <strong>Fig. 1</strong>. 31P-MRS spectral output in lower-right image, which is from the visual cortex region of the brain as shown in (a). Image from [4]. 
    </figcaption>
</figure>

### Redesign Challenge Task

For this redesign task, we challenge participants to propose an alternative
visualization approach that better enables clinicians and MRS researchers to
explore, analyze, and/or communicate these data in a more facile manner, for
instance to answer questions like:

-   How to more easily **identify** metabolites within a spectrum?
-   How to **assess the quality of a spectrum,** e.g., according to peak shape(s)?
-   How to **compare** peaks in a spectrum within and across subjects? These peaks are usually measured in terms of their amplitudes, or the area-under-the-peak.
-   How to **identify, compare and summarize ratio values** (often with phosphocreatine as the base comparison) between peaks in an intuitive way?

Submissions should consider visualization theory and principles. Most essential
to this challenge is the exploration of creative, novel ideas for this data and
associated tasks—as such, **sketching and prototyping as well as fully
interactive solutions are welcome**\!

### Data and Documentation

<figure>
    <img src="{{site.baseurl}}/images/biovis-challenge/fig2.png" alt="Spectral Output" />
    <figcaption>
        <strong>Fig. 2</strong>. Rendering of one spectral output from the provided dataset. Peaks indicate metabolites in the sample. Important chemical shifts for metabolites of interest (as noted in below Table) are marked with vertical grey bars, and are based on the chemical shift table presented by Deelchand et al. [8].
    </figcaption>
</figure>

#### Example Dataset

The provided dataset includes 18 spectral outputs, one of which is illustrated
in Fig 2\. Each peak in this figure corresponds to a metabolite, for example,
phosphocreatine is the tall peak centered at approximately 0.0 parts per
million. The below table lists the more commonly-assessed metabolites and their
chemical shifts. Note that some metabolites have multiple peaks, e.g., DPG:

<figure>
    <img src="{{site.baseurl}}/images/biovis-challenge/metabolite_chemicalshifts_table.png" alt="Metabolite table" />
</figure>

For a detailed table of other metabolites and their chemical shifts, we refer to Deelchand et al. [8].

#### Data Description

The processed dataset for the redesign challenge is available for download at
the [BioMed+Vis 2025 Redesign Challenge
GitLab](https://git.app.uib.no/biomedvis2025/31p-mrs-redesign/-/tree/main/data?ref_type=heads).

The dataset we provide includes **18 pre-processed spectra**. The spectra are
split into two csv files:

-   `spectra.csv`: Each spectrum is a 2048 x 1 vector that represents the measured amplitude of a given metabolite at a given chemical shift for a single subject. There are 18 vectors for a total array size of 2048 x 18. These vectors represent the spectra for 9 individuals, all at the same voxel position with samples at two time points. The arrangement is such that `spectra[:,0]` and `spectra[:,1]` belong to **Subject00** at **t0** and **t1** respectively, `spectra[:,2]` and `spectra[:,3]`belong to **Subject01** at **t0** and **t1**, etc.
-   `chemical_shifts.csv`: All spectra from spectra.csv align with this 2048 x 1 vector that indicates the chemical shift (x-axis in Fig. 2). The chemical shifts of metabolites are usually referenced to Phosphocreatine (PCr) as an internal standard at 0.0 ppm.

For a bit more background on 31P-MRS, \[9\] and \[10\] provide a friendly
orientation to this kind of data. To see some of the types of work from the
visualization community for this kind of data, \[6\] and \[7\] are useful
starting points.

The full dataset for those interested in a (much) deeper dive is available here:
[31P MRS Participants 1-10](https://data.mendeley.com/datasets/3r7kmfmpyj/1)
\[4\].

### References and Further Resources on 31P-MRS

\[1\] World Health Organization. _Over 1 in 3 people affected by neurological conditions, the leading cause of illness and disability worldwide (2024)_.

\[2\] S. Ulmer, M. Backens, and F. J. Ahlhelm. Basic principles and clinical applications of magnetic resonance spectroscopy in neuroradiology. Journal of Computer Assisted Tomography, 40(1):1–13, 2016\. doi: 10.1097/RCT.0000000000000322

\[3\] M. Van Der Graaf. In vivo magnetic resonance spectroscopy: Basic methodology and clinical applications. European Biophysics Journal, 39(4):527–540 (2010). Doi: 10.1002/9780470882221

\[4\] Fear, E. J., Torkelsen, F. H., Zamboni, E., Chen, K. J., Scott, M., Jeffery, G., ... & Kennerley, A. J. (2023). Use of 31P magnetisation transfer magnetic resonance spectroscopy to measure ATP changes after 670 nm transcranial photobiomodulation in older adults. _Aging Cell_, _22_(11), e14005. **Data:** Fear, Elizabeth; Kennerley, Aneurin (2023), “31P MRS MT Participants 1-10”, Mendeley Data, V1, doi: 10.17632/3r7kmfmpyj.1

\[5\] Jett, S., Boneu, C., Zarate, C., Carlton, C., Kodancha, V., Nerattini, M., ... & Mosconi, L. (2023). Systematic review of 31P-magnetic resonance spectroscopy studies of brain high energy phosphates and membrane phospholipids in aging and Alzheimer's disease. _Frontiers in Aging Neuroscience_, _15_, 1183228\.

\[6\] Nunes, M., Laruelo, A., Ken, S., Laprie, A., & Bühler, K. (2014, September). A Survey on Visualizing Magnetic Resonance Spectroscopy Data. In _VCBM_ (pp. 21-30).

\[7\] Garrison, L., Vašíček, J., Craven, A. R., Grüner, R., Smit, N. N., & Bruckner, S. (2020). Interactive visual exploration of metabolite ratios in MR spectroscopy studies. _Computers & Graphics_, _92_, 1-12. Accompanying github repository and tool: [https://github.com/lauragarrison87/spectramosaic-public](https://github.com/lauragarrison87/spectramosaic-public) .

\[8\] Deelchand, D. K., Nguyen, T. M., Zhu, X. H., Mochel, F., & Henry, P. G. (2015). Quantification of in vivo 31P NMR brain spectra using LCModel. _NMR in Biomedicine_, _28_(6), 633-641.

\[9\] [MRS Hub](https://mrshub.org/software_visualization/): Compiled list of MRS quantification and visualization software

\[10\] [Why Phosphorus? Questions and answers in MRI](https://mriquestions.com/why-phosphorus.html)

## 3D Microscopy Imaging Challenge: From a RAW imaging volume to biological findings

<figure>
    <img src="{{site.baseurl}}/images/biovis-challenge/lin-wang-coy.png" alt="Multiplexed 3D atlas" />
    <figcaption>
        <strong>Fig.</strong> Lin, Wang, Coy et al., 2023, <strong>Multiplexed
        3D atlas of state transitions and immune interactions in colorectal
        cancer</strong>, <em>Cell</em>, 186, 363-381.<br>Adapted by Clarence Yapp, 2024.
    </figcaption>
</figure>

<div style="display: flex; justify-content: center">
<iframe width="560" height="315"
src="https://www.youtube.com/embed/8TLydpm07Vo?si=MmytUlNvhlYkAlWc"
title="YouTube video player" frameborder="0" allow="accelerometer; autoplay;
clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

### Biological Background and Data Description

Highly multiplexed tissue imaging methods, such as Cyclic Immunofluorescence
(CycIF), which allow for the analysis of over 30 biomarkers on a single tissue
section, are essential tools for scientists to investigate the subcellular
complexities of cancer \[1\]. Indeed, CyCIF has been instrumental in revealing
immune-tumor interactions and the progression of melanoma at single-cell
precision \[2\]. More recently, researchers have extended these techniques to
image volumes, allowing for an even more comprehensive analysis of the diverse
_cell types_ and _states_ within the tumor microenvironment and their _spatial
interactions_ \[3\]. These volumes enable cancer biologists and pathologists to
explore hypotheses derived from 2D tissue images with enhanced detail and rigor,
facilitating deeper insights into cellular dynamics within the tumor
microenvironment. This approach allows them to examine the location and extent
of specific cell-cell interactions within a given volume. However, identifying,
visualizing, and analyzing these intricate interactions across volumes is a
challenging task, both computationally and visually. The focus of this BioMedVis
Challenge, therefore, is to develop algorithms and visualization techniques that
help experts search for and identify such cell-cell interactions, as indicated
by the presence of cells expressing certain biomarkers.

### Challenge Task

The starting Jupyter notebook presents several combinations of biomarkers that
represent known cell-cell interactions. We demonstrate how specific cells can be
determined based on the presence of these biomarkers. It is your task to
identify and visualize where such interactions occur within the tissue, both
globally and locally.

Participants must thus:

1. Develop an algorithm for identifying ROIs where cells expressing specific combinations of markers exist within the tissue volume.
2. Visualizing these ROIs at a global scale, helping experts assess the extent to which such interactions occur and the broad morphological regions in which these interactions are occurring.
3. Allow users to dig into specific ROIs at the cellular level.

In doing so, participants may choose to augment existing volumetric
visualization techniques or propose peripheral abstract visualizations. When
visualizing the volume, they may choose to identify view configurations of the
following form:

-   Camera:
    -   Zoom Level
-   Volume Settings:
    -   Translation (X, Y, Z)
    -   Rotation (X, Y, Z)
-   Channels:
    -   Selection, Color, and Value Range

### Data and Documentation

The data volume included in this challenge represents a 194x5508x10908 volume of
cancerous tissue belonging to a patient suffering from metastatic melanoma.
Scientists have identified “immune niches” in this tissue, which contain
specific interactions between immune cells of different types and states.

Also provided is a Jupyter Notebook (link/details), which includes a sample
dataset and some notable cell-cell interactions. This notebook uses Vitessce,
which participants are welcome to build on, though they may also develop their
own visualization/visual analytics systems or build on other systems.

Jupyter notebook: [BioMedVis Challenge 2025.ipynb](https://colab.research.google.com/drive/1hMXNI3dbIM4JTnQ69fgVrsvO3Jq0ZPDo?usp=sharing)

**UPDATE 7/16/25: **
The dataset for the 3D Microscopy Imaging Challenge is now available at: s3://lsp-public-data/biomedvis-challenge-2025

AWS Bucket:
s3://lsp-public-data/biomedvis-challenge-2025/ or
[https://lsp-public-data.s3.amazonaws.com/biomedvis-challenge-2025/](https://lsp-public-data.s3.amazonaws.com/biomedvis-challenge-2025/)

Access Instructions: We recommend accessing the data directly in Zarr format, as demonstrated in the [Notebook](https://colab.research.google.com/drive/1hMXNI3dbIM4JTnQ69fgVrsvO3Jq0ZPDo?usp=sharing)

Alternatively, you can browse and download files via the AWS CLI:

```
aws s3 ls s3://lsp-public-data/biomedvis-challenge-2025/
aws s3 cp s3://lsp-public-data/biomedvis-challenge-2025/README.md .
```

or using [Cyberduck](https://zenodo.org/records/10223574).

### References

\[1\] Lin JR, Fallahi-Sichani M, Chen JY, Sorger PK. Cyclic Immunofluorescence (CycIF), A Highly Multiplexed Method for Single-cell Imaging. Curr Protoc Chem Biol. 2016 Dec 7;8(4):251-264. doi: [10.1002/cpch.14](https://doi.org/10.1002/cpch.14). PMID: 27925668; PMCID: PMC5233430.

\[2\] Ajit J. Nirmal, Zoltan Maliga, Tuulia Vallius, Brian Quattrochi, Alyce A. Chen, Connor A. Jacobson, Roxanne J. Pelletier, Clarence Yapp, Raquel Arias-Camison, Yu-An Chen, Christine G. Lian, George F. Murphy, Sandro Santagata, Peter K. Sorger; The Spatial Landscape of Progression and Immunoediting in Primary Melanoma at Single-Cell Resolution. _Cancer Discov_ 1 June 2022; 12 (6): 1518–1541. doi: [10.1158/2159-8290.CD-21-1357](https://doi.org/10.1158/2159-8290.CD-21-1357)

\[3\] Yapp C, Nirmal AJ, Zhou F, Maliga Z, Tefft JB, Llopis PM, Murphy GF, Lian CG, Danuser G, Santagata S, Sorger PK; Human Tumour Atlas Network. Multiplexed 3D Analysis of Immune States and Niches in Human Tissue. bioRxiv \[Preprint\]. 2024 Mar 28:2023.11.10.566670. doi: [10.1101/2023.11.10.566670](https://doi.org/10.1101/2023.11.10.566670). PMID: 38014052; PMCID: PMC10680601.

## Submission

Submissions for either the redesign or the main challenge will be considered for
talk or poster presentations. Please send a two-page PDF abstract with up to 5
additional figures to PCS:
[new.precisionconference.com/submissions](http://new.precisionconference.com/submissions).
Your submission should use the [VGTC conference two-column format](https://tc.computer.org/vgtc/publications/conference).
Your submission should include:

-   a thorough **description and justification** of your visualization (and analysis) techniques–_use the space to describe your approach, and keep background and data detail descriptions to a minimum._
-   at least one or more **images** of your visualization
-   **_Highly encouraged_**: **a video or screencast** to explain your visualization approach (should not exceed five minutes)\!

Selected submissions will be invited for talk presentations during the
Bio+MedVis session at the [IEEE VIS 2025](https://ieeevis.org/year/2025/welcome)
conference.

### Evaluation of Submissions

All submissions will be evaluated by at least two reviewers, coming from the
challenge chairs and selected domain experts. All accepted submissions will be
published in the conference proceedings.

Strong, creative submissions have the potential for recognition with an **Award
of Merit** or an **Award of Excellence**.

Awards, at the discretion of evaluators, may be given according to the primary
author’s status as a **_Student_** (BSc/MSc) or **_Researcher/Professional_**
(PhD and up). In the case of many submissions, Challenge organizers may further
subdivide these status categories to better weigh the contribution against the
experience of the submitters.

## Important dates

-   Submission (<span style="color:red">extended</span>): August 22, 2025 [Anywhere On Earth](https://time.is/Anywhere_on_Earth)
-   Notification: September 5, 2025
-   Camera-ready version: September 26, 2025
-   Bio+MedVis Challenge event: November 2, 2025
-->

