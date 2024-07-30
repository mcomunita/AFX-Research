<div align="center">

<img src="./assets/logo-transp-small.png" width="280">

# ToneTwist AFx Dataset

#### _A collection of dry/wet pairs for audio effects research_

[Marco Comunità](https://mcomunita.github.io/)<sup>1</sup>, [Christian J. Steinmetz](http://Christiansteinmetz.com)<sup>1</sup>, [Joshua D. Reiss](http://www.eecs.qmul.ac.uk/~josh/)<sup>1</sup>

<sup>1</sup> Centre for Digital Music, Queen Mary University of London, UK<br>

</div>

---
## References

If you make use of ToneTwist AFx Dataset, please cite the following publication:

```BibTex
@article{comunita2024,
  title={},
  author={},
  booktitle={},
  pages={},
  year={2024},
  organization={IEEE}
}
```

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
---
- [Dry Inputs](#dry-inputs)
- [Wet Outputs](#wet-outputs)
- [External Data](#external-data)
- [Contributions](#contributions)
- [Analog](#analog)
- [Analog Parametric](#analog-parametric)
- [Digital](#digital)
- [Digital Parametric](#digital-parametric)
- [Sources](#sources)
<!-- END doctoc generated TOC please keep comment here to allow auto update -->

---
## Dry Inputs

Dry inputs are a selection of clean guitar and bass recordings from several sources:

- [IDMT-SMT-GUITAR](https://www.idmt.fraunhofer.de/en/publications/datasets/guitar.html) - dataset 2 (7:23 min)
- [IDMT-SMT-GUITAR](https://www.idmt.fraunhofer.de/en/publications/datasets/guitar.html) - dataset 4 - Career SG (6:08 min)
- [IDMT-SMT-GUITAR](https://www.idmt.fraunhofer.de/en/publications/datasets/guitar.html) - dataset 4 - Ibanez 2820 (5:14 min)
- [IDMT-SMT-Bass-Single-Track](https://www.idmt.fraunhofer.de/en/publications/datasets/bass_lines.html) - (5:58 min)
- [NAM: Neural Amp Modeler](https://github.com/sdatkinson/neural-amp-modeler?tab=readme-ov-file#download-audio-files) - (3:11 min)
- Private Guitar Data - (5:19 min)
- YouTube Bass Recordings - (10:09 min)

Pre-processing:

- All:
  - synchronization markers (2 impulses) added at start and end of every file
- IDMT-SMT-GUITAR - dataset 2:
  - peak normalized to -6dBFS
- NAM:
  - no pre-processing
- Others:
  - peak normalized to -0.1dBFS
  - signal multiplied by random number every 5 seconds (uniform distribution [0.1, 1.0] = [-20dB, 0dB])

---
## Wet Outputs

We organize data into 4 categories:

- [Analog](https://github.com/mcomunita/tonetwist-afx-dataset?tab=readme-ov-file#analog)
- [Analog Parametric](https://github.com/mcomunita/tonetwist-afx-dataset?tab=readme-ov-file#analog-parametric)
- [Digital](https://github.com/mcomunita/tonetwist-afx-dataset?tab=readme-ov-file#digital)
- [Digital Parametric](https://github.com/mcomunita/tonetwist-afx-dataset?tab=readme-ov-file#digital-parametric)

Where _Parametric_ means that the number of sampled controls combinations is sufficient to develop/train a parametric model.

---
## External Data

This repo contains also links to external sources (i.e., data recorded by others for scientific publication purposes or personal projects). In these cases the dry inputs will be different from the ones described above and will have a separate link for download.

The reasons to include and re-publish external sources here are several:
- completeness: we wanted to gather all the amazing work that's been done by the audio effects research community in one place.
- accessibility: by storing all data on a reliable platform (zenodo) that's going to be always accessible.
- consistency: we did not simply link someone else's work, we took care of verifying, pre-processing (where necessary), renaming, reorganizing - so that you can use any data in this repo straight away (no need to write a new dataset class every time).

Attributions to the original authors are included in this repo and references to publication, code, webpage, etc., are included in a README file.

If you find your work published here and you are not happy, feel free to contact us.

---
## Controls

Controls are expressed in a range from 0 to 10, corresponding to the positions shown below. If you are contributing to this dataset please follow this convention.

<img src="./assets/knob.png" width="150">

---
## Contributions

We invite anyone to contribute to this repo by recording and publishing more data.

### Recording

We assume you are knowleageable enough to know how to do it properly and we do not aim to verify new contributions, but here's some tips:
- together with the dry inputs we included an Audacity project that can be used to set input/output levels and record everything in 1 step (see README file included with the data for further details)
- always use an insulated and filtered PSU (e.g., [https://www.thomann.de/gb/harley_benton_powerplant_iso_5_pro.htm](https://www.thomann.de/gb/harley_benton_powerplant_iso_5_pro.htm)) to prevent excessive noise and hum, especially if you are recording high gain effects.
- before recording, make sure there is no clipping happening anywhere in the chain.
- make sure you are not driving an effect too much (i.e., unrealistically high output from your audio interface into the effect)
- as well as not enough (i.e., unrealistically low output from your audio interface into the effect)
- after recording, crop all files to the same exact length (to the sample level) as the dry inputs
- also, verify that dry inputs and wet outputs are perfectly synchronized using the markers at the start and end of each file (checking the end allows you to verify there's been no data loss during recording)
- save wet outputs with the same format as dry inputs (wav - 48kHz - 32bit floating point)

### Naming and Folder Structure

Please use the same naming convention and folder structure used across the whole dataset (look at 1 internal and 1 external source for guidance).

```
FxBrand-FxName
│   ├── test
│   │   ├── C(ontrolLetter)1(Control)V(alue)1_C(ontrolLetter)2(Control)V(alue)1_C(ontrolLetter)3(Control)V(alue)1
│   │   │   ├── C1V1_C2V1_C3V1.test-file1-name.target.wav
│   │   │   ├── C1V1_C2V1_C3V1.test-file2-name.target.wav
│   │   │   │ ...
│   │   │   └── C1V1_C2V1_C3V1.test-filek-name.target.wav
│   │   ├── C1V2_C2V2_C3V2
│   │   │ ...
│   │   └── C1Vn_C2Vn_C3Vn
│   │── trainval
│   │   ├── C1V1_C2V1_C3V1
│   │   │   ├── C1V1_C2V1_C3V1.trainval-file1-name.target.wav
│   │   │   ├── C1V1_C2V1_C3V1.trainval-file2-name.target.wav
│   │   │   │ ...
│   │   │   └── C1V1_C2V1_C3V1.trainval-filem-name.target.wav
│   │   ├── C1V2_C2V2_C3V2
│   │   │ ...
│   │   └── C1Vn_C2Vn_C3Vn
└── └── README.md
```

Example of dry multiple files sources:

<img src="./assets/folder-structure-dry-internal-example.png" width="500">

Example of wet multiple files sources:

<img src="./assets/folder-structure-wet-internal-example.png" width="640">

Example of dry/wet single file sources:

<img src="./assets/folder-structure-external-example.png" width="500">


### ReadMe
Example of README file for internal source: [README-internal-example](https://github.com/mcomunita/tonetwist-afx-dataset/blob/master/assets/README-internal-example.md)

Example of README file for external source: [README-external-example](https://github.com/mcomunita/tonetwist-afx-dataset/blob/master/assets/README-external-example.md)


### Publishing
- Please publish your data on zenodo and include all necessary info (again, take a look at 1 external and 1 internal source for guidance).
- If you use the dry inputs provided here you will be considered as an internal source. Once the data is published on zenodo (don't include the dry files), please submit a PR with the link.
- If you use different dry inputs you will be considered as an external source. Once the data is published on zenodo (include dry and wet files), please submit PR with the link and an external reference.

---
## Analog

### Dry Inputs with markers
- [https://zenodo.org/uploads/10455730](https://zenodo.org/uploads/10455730)

### Amplifier/Preamp
- [Blackstar HT1 - Channel: Overdrive](https://zenodo.org/uploads/10794425) - [1]
- [Blackstar HT5 Metal - Channel: Overdrive](https://zenodo.org/uploads/10796501) - [2] 
- [Engl Retro Tube 50 - Channel: Drive](https://zenodo.org/uploads/10796525) - [2]
- [Fender Blues Jr](https://zenodo.org/uploads/10797977) - [3]
- [Ibanez TSA15 - Channel: Crunch](https://zenodo.org/uploads/10796536) - [2]
- [MesaBoogie 550 - Channel: Clean](https://zenodo.org/uploads/10796557) - [2]
- [MesaBoogie 550 - Channel: Crunch](https://zenodo.org/uploads/10796819) - [2]
- [MesaBoogie 550 - Channel: Burn](https://zenodo.org/uploads/10796547) - [2]
- [MesaBoogie Mark V - Channel: Clean](https://zenodo.org/uploads/10796829) - [2]
- [MesaBoogie Mark V - Channel: Crunch](https://zenodo.org/uploads/10796841) - [2]
- [MesaBoogie Mark V - Channel: Extreme](https://zenodo.org/uploads/10796864) - [2]
- [Universal Audio 6176 Vintage Channel Strip - 610B Mic Preamp](https://zenodo.org/uploads/10798111) - [4]
 
### Chorus
- [Landlord Brewers Droop Chorus](https://zenodo.org/uploads/10796408)

### Compressor/Limiter
- [Ampeg Optocomp](https://zenodo.org/uploads/10465454)
- [Flamma Analog Comp](https://zenodo.org/uploads/10794703)
- [Yuer Dyna Compressor](https://zenodo.org/uploads/10796426) (similar to Ross Compressor)
- [Universal Audio 6176 Vintage Channel Strip - 1176LN Limiter](https://zenodo.org/uploads/10798151) - [4]

### Distortion
- [DIY Electro Harmonix Big Muff](https://zenodo.org/uploads/10797916) - [3]
- [Electro Harmonix Big Muff](https://zenodo.org/uploads/10891515) - [1]
- [Electro Harmonix Metal Muff](https://zenodo.org/uploads/10794659)
- [Harley Benton Big Fur](https://zenodo.org/uploads/10794737) (similar to Electro Harmonix Big Muff)
- [Harley Benton Drop Kick](https://zenodo.org/uploads/10794776) (similar to Suhr Riot)
- [Harley Benton Plexicon](https://zenodo.org/uploads/10796359)
- [Harley Benton Rodent](https://zenodo.org/uploads/10796378) (similar to Proco Rat)

### Fuzz
- [Harley Benton Fuzzy Logic](https://zenodo.org/uploads/10796322) (similar to Fuzz Face Germanium)
- [Harley Benton Silly Fuzz](https://zenodo.org/uploads/10796394) (similar to Fuzz Face Silicon)

### Overdrive
- [DIY Klon Centaur](https://zenodo.org/uploads/10797932) - [3]
- [Fulltone Full Drive 2](https://zenodo.org/uploads/10794615)
- [Ibanez TS9](https://zenodo.org/uploads/10797988) - [3]
- [Harley Benton Green Tint](https://zenodo.org/uploads/10796333) (similar to Ibanez Tube Screamer)

### Tremolo
- [Mooer Trelicopter](https://zenodo.org/uploads/10796416)

---
## Analog Parametric

### Amplifier/Preamp
- [Marshall JVM410H - Channel: OD1](https://zenodo.org/uploads/10892012) - [5]

---
## Digital

### Dry Inputs
- [https://zenodo.org/uploads/10901426](https://zenodo.org/uploads/10901426)

### Compressor/Limiter
- [Amplitube DComp](https://zenodo.org/uploads/10901328) (emulation of MXR Dyna Comp)
- [Amplitube Fender Comp](https://zenodo.org/uploads/10901340) (emulation of Fender Cyber-Twin compressor)

### Fuzz
- [Arturia Rev Spring 636 - Germanium Preamp/Fuzz](https://zenodo.org/uploads/10901350) (emulation of Grampian 636 Spring Reverb)
- [Custom Dynamic Fuzz](https://zenodo.org/uploads/10901357)

---
## Digital Parametric

### Dry Inputs with markers
- [https://zenodo.org/uploads/10455730](https://zenodo.org/uploads/10455730)

### Distortion
- [Multidrive Pedal Pro M-Distortion](https://zenodo.org/uploads/10901455) (emulation of Boss Metal Zone)

### Fuzz
- [Multidrive Pedal Pro F-Fuzz](https://zenodo.org/uploads/10901450) (emulation of Fuzz Face Germanium)

### Overdrive
- [Multidrive Pedal Pro 808-Scream](https://zenodo.org/uploads/10901401) (emulation of Ibanez Tube Screamer 808)
- [Multidrive Pedal Pro B-Drive](https://zenodo.org/uploads/10901417) (emulation of Boss Blues Driver)


---
## Sources

[1] - [https://github.com/Alec-Wright/Automated-GuitarAmpModelling](https://github.com/Alec-Wright/Automated-GuitarAmpModelling)\
[2] - [https://github.com/TSchmitzULG/NeuralNetwork_Comparison/tree/master](https://github.com/TSchmitzULG/NeuralNetwork_Comparison/tree/master)\
[3] - [https://github.com/GuitarML](https://github.com/GuitarML)\
[4] - [https://github.com/mchijmma/DL-AFx](https://github.com/mchijmma/DL-AFx)\
[5] - [https://github.com/stepanmk/grey-box-amp](https://github.com/stepanmk/grey-box-amp)
