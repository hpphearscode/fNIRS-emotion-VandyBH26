# 2026 Vanderbilt BrainHack Project: Enlightening the Emotional Brain

### Current task flow for quality check and preprocessing

Our current workflow is adapted from MNE-NIRS analysis example [here](https://mne.tools/mne-nirs/stable/auto_examples/general/plot_15_waveform.html)

- Data Cleaning & Quality Check: 
  - Check annotations/trigger events.
  - Convert raw light intensity values to optical density values. This procedure removes baseline variations in light levels and scales the data linearly so that subsequent application of the modified Beer-Lambert law can accurately yield relative hemoglobin concentrations (HbO / HbR) 
  - Inspection of data quality. Evaluate bad channels using Scalp Coupling Index (SCI) and generate histogram showing counts of bad channels. A SCI cutoff of 0.5-0.7 is often used in the literature.
  - Exclude bad channels.
- Signal Preprocessing & Visualization:
  - Remove motion artefacts. Example [here](https://mne.tools/mne-nirs/stable/auto_examples/general/plot_21_artifacts.html)
  - Convert optical density values to hemoglobin values, using the modified Beer-Lambert Law.
  - Remove heart rate low-frequency non-physiological drifts. 
  - If using GLM, we apply short-channel regression. A full GLM example can be found [here](https://mne.tools/mne-nirs/stable/auto_examples/general/plot_11_hrf_measured.html)

  How you can contribute:
  - What do you think of this preprocessing pipeline in general? Feedback is particularly appreciated from team members with signal processing and/or neuroimaging background. 
  - Develope your own preprocessing pipeline for the current experiment, or refine our pipeline. [Issue #]()
