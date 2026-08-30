# 2026 Vanderbilt BrainHack Project: Enlightening the Emotional Brain

## Analysis
### Experiment description: 
- Participants of normal hearing were comfortably seated in a sound attenuating booth. They listened to sounds from the International Affective Digitized Sound Corpus. These sounds include animal noises (e.g., cats meowing), human social noises (e.g., weeping), bodily noises (e.g., coughing), environmental sounds (e.g., traffic noises), and music (e.g., acoustic guitars). Each participant listened to 60 six-second sound clips, which consist of 20 pleasant sounds, 20 unpleasant sounds, and 20 neutral sounds. Sound clips were presented in a blocked-design, where each block had four clips of sounds of the same valence (e.g., all four sounds are pleasant). Between blocks, there was 30 second of silence. A question asking 'Did the sounds make you feel pleasant/unpleasant/neither pleasant or unpleasan' was presented after the end of the fourth sound clip, and participants used the 'Enter' button to indicate 'YES'. No action would indicate 'NO'. Sound clips were randomized within blocks, and order of sound blocks were randomized for each participant. The question was used to keep participants engaged in listening and encourage active appraisal. 
- Prior to listening to emotional sound in the main task, we obtained a six minute resting state recording. 

### Hypothesis: 
- Relative to neutral sounds, both unpleasant and pleasant sound would elicit greater auditory region activation.
- Similarly, we also expect the prefrontal cortex to show stronger activation to both unpleasant and pleasant sounds, relative to neutral sounds.
- We also have some exploratory hypothesis for resting state recordings. There is some, although messy, evidence that asymmetry in the PFC may be an indicator of personality, and perhaps also predictive how one may respond to emotional stimuli.
  - Some interesting readings: 
    - Balconi, M., Grippa, E., & Vanutelli, M. E. (2015). Resting lateralized activity predicts the cortical response and appraisal of emotions: an fNIRS study. Social cognitive and affective neuroscience, 10(12), 1607-1614. (Experiment show PFC asymmetry at rest may predict emotion perception at task)
    - Harmon-Jones, E., Gable, P. A., & Peterson, C. K. (2010). The role of asymmetric frontal cortical activity in emotion-related phenomena: A review and update. Biological psychology, 84(3), 451-462. (A review)



### Experiment design schematic

<p align="center">
  <img
    width="100%"
    alt="Auditory emotion fNIRS experimental block design"
    src="Assets/brainhack-experiment-schematic.svg"
  />
</p>

Trigger information:
Trigger	Event description
- #1	Onset of a pleasant IADS sound
- #2	Onset of a neutral IADS sound
- #3	Onset of an unpleasant IADS sound
- #4	Start of the inter-block interval (IBI) for the pleasant condition
- #5	End of the inter-block interval for the pleasant condition
- #6	Start of the IBI for the neutral condition
- #7	End of the IBI for the neutral condition
- #8	Start of the IBI for the unpleasant condition
- #9	End of the IBI for the unpleasant condition
- #10	Presentation of the engagement prompt asking about whether the sound made the participant feel pleasant
- #11	Presentation of the engagement prompt asking about whether the sound made the participant feel neutral
- #12	Presentation of the engagement prompt asking about whether the sound made the participant feel unpleasant
- #13	End of the engagement prompt and response window
- #14	End of the experiment
- #15	Participant button press during the engagement response window

## How are we currently doing it?

- We currently plan to analyze the data in at least two ways and compare their pros and cons. The scripts are still work in progress.
  - Waveform average
  - GLM

## How you can contribute:
- **Issue #07: Develop code to incoporate individualized channel-anatomy match (from co-registration) in analysis pipeline.**
- **Issue #08: Develop script to compare analysis with and without short channel regression.**
- **Issue #09: Evaluate the pros and cons of doing waveform averaging vs. GLM for the current task.**
- **Issue #10: Explore effective connectivity b/w auditory and prefrontal regions. (Given that we don't have a lot of data, this could just be an action plan).**
- **Issue #11: Calculate Lateralized Index Response for resting state recording**

## MNE-NIRS examples:
- [Waveform averaging](https://mne.tools/mne-nirs/stable/auto_examples/general/plot_15_waveform.html)
- [GLM](https://mne.tools/mne-nirs/stable/auto_examples/general/plot_11_hrf_measured.html)
- [Granger causlity](https://mne.tools/mne-connectivity/dev/auto_examples/granger_causality.html)