# 2026 Vanderbilt BrainHack Project: Enlightening the Emotional Brain
## Preprocessing and quality check
### Why preprocess?
- Separating cortical response from noise and physiological confounds.
  - Although fNIRS is sensitive to cortical changes in oxygenated and deoxygenated hemoglobin, the recorded signal is not exclusively cerebral. Near-infrared light travels through the scalp and skull before reaching the cortex, so measurements contain a mixture of task-evoked neural hemodynamics, superficial blood-flow changes, systemic physiology, motion artifacts, instrumental noise, and spontaneous cerebral activity. Some confounding components may also be time-locked to the experimental task, causing them to resemble genuine cortical activation or obscure an underlying neural response. Consequently, careful preprocessing and statistical modeling—including signal-quality assessment, motion correction, short-separation regression, and nuisance regressors within a general linear model—are necessary to isolate the task-related cerebral response and reduce the risk of false-positive or false-negative conclusions.
  - Helpful readings:
    - [Tachtsidis, I., & Scholkmann, F. (2016). False positives and false negatives in functional near-infrared spectroscopy: issues, challenges, and the way forward. Neurophotonics, 3(3), 031405-031405.](https://www.spiedigitallibrary.org/journals/neurophotonics/volume-3/issue-3/031405/False-positives-and-false-negatives-in-functional-near-infrared-spectroscopy/10.1117/1.NPh.3.3.031405.short)
    - [Yücel, M. A., Lühmann, A. V., Scholkmann, F., Gervain, J., Dan, I., Ayaz, H., ... & Wolf, M. (2021). Best practices for fNIRS publications. Neurophotonics, 8(1), 012101-012101.](https://www.spiedigitallibrary.org/journals/neurophotonics/volume-8/issue-01/012101/Best-practices-for-fNIRS-publications/10.1117/1.NPh.8.1.012101.full)


### How are we currently doing it? 


#### Preprocessing for waveform averaging - adapted from MNE-NIRS analysis example [here](https://mne.tools/mne-nirs/stable/auto_examples/general/plot_15_waveform.html)

```mermaid
flowchart TD

    A["Native NIRx"] --> B["Rename triggers"]
    B --> C["Collapse 4 x 6-s sounds<br/>to 24-s blocks"]

    C --> D["Optical density"]
    D --> E["SCI quality control<br/>threshold = 0.50"]

    E --> F["Classify short and long channels"]
    F --> G["Drop entire S-D pair<br/>if either wavelength fails SCI"]

    G --> H["TDDR motion correction"]
    H --> I["Band-pass 0.01-1.5 Hz"]

    I --> J["Nearest short-channel regression<br/>OD space"]
    J --> K["Keep long channels"]

    K --> L["Convert to haemoglobin"]

    L --> M["Band-pass 0.01-0.09 Hz"]

    M --> N["Epoch with baseline -5 to 0 s"]


```

<br>

#### Preprocessing for GLM may differ, and is in the works, example can be found [here](https://mne.tools/mne-nirs/stable/auto_examples/general/plot_11_hrf_measured.html)

### How you can contribute:
  - #### **Task #06: Develop your own preprocessing pipeline for the current experiment, or refine our pipeline.**
    - What do you think of this preprocessing pipeline in general? Feedback is particularly appreciated from team members with signal processing and/or neuroimaging background.