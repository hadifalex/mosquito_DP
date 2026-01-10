# Generating audible signal from inaudible distortion products

- This repo is accompanying our recent preprint ["Distortion rules: audibility creation in the mosquito ear"](https://www.biorxiv.org/content/10.1101/2025.09.05.674403v1).
- A licence will be added upon publication.

This repository contains the full analysis and modelling used of how mechanical stimuli translate to auditory neuronal responses.


## How do disease-transmitting mosquitoes find their mates?

It is well established that mosquitoes rely almost exclusively on auditory cues for mate seeking with the males taking the role of the seeker.
A particularly intriguing gap in our knowledge is the modality mismatch between the frequencies that the female mosquitoes produce and those that the male mosquitoes' auditory neurons can capture.
The system is further complicated by the mate seeking taking place within large, noisy, male-dominated swarms (up to ~1000 males).

Mosquitoes seemingly solve two simultaneous issues:
- They are able to register and identify particularly weak signals (female wingbeat) in a remarkably noisy environment (swarms)
- They are able to bypass a mismatch of sensory modalities (frequency domain of their antenna vs that of their auditory neurons)
- Behaviourally, male *Anopheles* mosquitoes only respond to the female tone when in flight, suggesting that an acoustic interaction of both conspecifics is needed for audibility to occur.

## Introduction

Male mosquito ears were stimulated and the motion of the antenna was synchronously recorded along with the auditory nerve response to the stimulus.
The mechanical recordings were performed using laser Doppler vibrometry (LDV) whereas the nerve responses were recorded using electrophysiological techniques.

Two types of stimuli are presented:
- **one-tone stimuli $f_1$:** representing either an idle male with a flying female passing by, or a single male in flight.
- **two-tone stimuli $f_1$ and $f_2$:** representing a pair flying together.

The $f_1$ stimulus scans from 100-1000 Hz, encapsualtes the ecologically relevant frequencies for a given temperature (300-500 Hz).
The $f_2$ stimulus is fixed at 540 Hz, which is the male flight tone frequency.

This allows us to create an input/output database across a large span of frequencies that go beyond the ecologically relevant frequencies to test mechanistic properties
of their auditory system. 

![alt text](image.png)
> **Fig.1:** Basic experimental concept. A) Experimental setup. Stimulus via electrostatic actuators. Mechanical motion recorded via LDV. Neuronal response recorded via electrophysiology. B) Each recording channel is recorded for all stimulus frequencies. C) FFT of recordings reveal the prominence of distortion products (DPs) which are not random but generate structure.


## How do we best assess and analyse the recordings?

### Understanding bulk structure of data

The envelope of the flagellar and nerve recordings was extracted using a SNIP background estimator.

![alt text](image-2.png)
> **Fig.2:** The results show that the flagellar mechanics (black) are perfectly in line with a resonant peak of a damped harmonic oscillator.
> Similarly, the nerve response spans around 100-400 Hz, perfectly in line with known literature. The two novel, state-dependent auditory regions are highlighted in light blue and light red backgrounds.

The surprise comes with the auditory regions being sensitive to the antenna's mechanical state and amplitude of self-sustained oscillations.
Their presence appears to dramatically amplify and isolate the ecologically relevant frequencies (~350 Hz) whereas in the absence of them, an entirely novel auditory region is revealed
around 800 Hz. 

The classification between each of the three mechanical states (no sso, weak sso and strong sso) was done using principal component analysis (PCA) on the envelopes of free-fluctuating flagella.

The cummulative explained variance shows that we need about 2-3 dimensional PCA bases to sufficiently explain the variance observed.

![alt text](image-4.png)
> **Fig.3** The presence of a continuum shows that an animal can, in principle, smoothly transition from one mechanical state to the other.

### Creation of spectral mosaics

To better understand the bulk effects, we look at the spectral domain. FFTs of each response to a stimulus is aggregated and combined into a spectral "mosaic" as shown in Fig.1.


![alt text](image-1.png)
> **Fig.4:** The difficulty of those mosaics is extracting resulting distortion product families which manifest as "straight lines". The 3D mosaic is dimensionally reduced, digitised, and then a custom, physics-based algorithm is identifying and extracting these lines for both one-tone (top) and two-tone (bottom) mosaics.


The algorithnm is able to identify and extract from specific regions of interest if some frequency ranges are considered neurologically irrelevant:

![alt text](image-3.png)
> **Fig.5:** ROI-dependent feature extraction of DP families for a given mosaic.

### Stronger responses from DP-based signals

![alt text](image-5.png)
> **Fig.6:** DP-based decomposition reveals that animals exhibiting strong SSOs, have a 50% boost in nerve response in the quadratic DP family (yellow) hinting at a hidden, or SSO-specific neuronal population. 

### Multi-species sensitivity analysis

Distortion products have a clear auditory advantage over pure tones, a reason could be the mechanistic encoding of neuronal information. To understand whether such a feature is a general feature of mosquitoes, two more species were recruited to understand the relationship between sensitivity and neuronal advantage.

![alt text](image-6.png)
> **Fig.7:** Overall, distortion products appear to be far more sensitive to external stimuli than any pure-tone counterpart, with Anopheles being able to recruit 50% larger compound action potentials at times smaller flagellar displacements.

The clustering was performed using a gaussian mixture model for each of the three mechanical states.



## What are the limitations of this work?

As PCA has shown, the eigenbasis creates a continuous loop across all states. It is difficult to create true categories across three states, with the "weak SSO" being a large band rather than a true unique state. 

The natural SSO frequency can also change by as much as 100 Hz, meaning that the resulting DPs may also shift the position of DP family "peaks" as seen in Fig.2 and Fig.6 (pink band).

Temperature is a powerful determinant that affects flagellar resonant frequency, SSO frequency, wingbeat frequency. Although temperature was kept constant, it is difficult to control to within 1C.
