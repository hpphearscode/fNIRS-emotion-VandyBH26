# 2026 Vanderbilt BrainHack Project: Enlightening the Emotional Brain
<h2 align="center">Overview</h2>

<img
  align="left"
  width="300"
  alt="Illustration of emotional sound processing in the brain"
  src="./Assets/logo.png"
/>


This project will develop an open-source pipeline for analyzing functional
near-infrared spectroscopy (fNIRS) data. We will investigate how pleasant and
unpleasant sounds modulate activity in auditory and prefrontal brain regions.

During Vanderbilt BrainHack 2026, contributors will help us:

- Develop or refine a workflow to register individualized fNIRS optode coordinates to standardized MNI space.
- Develop or refine a preprocessing pipeline for NIRS signal in the current task.
- Develop or refine statistical analysis and visualization scripts for task-evoked response.
- Explore the feasibility of effective connectivity analyses between prefrontal and auditory regions using fNIRS recordings.

<br clear="left">


<h2 align="center">Project Significance</h2>

### **TL&DR**: A dynamic emotional experience is universal for everyday life. Yet, hearing loss may disrupt our emotion perception of sounds. Importantly, improved audibility through the use of hearing aids and cochlear implants do not fully alleviate this disruption. The current project is a first step in the journey to investigate the neural representation of disrupted auditory emotion perception. The outcome of the project will help us understand potential compensatory 

Everyday sounds carry rich emotional meaning: birdsong on a morning walk, a newborn’s coo, a favorite piece of music, or the impatient honk of a driver during rush hour. Our emotional responses to sound—the pleasure😁, comfort😌, excitement🤩, or irritation😡 we feel—are an important part of everyday life and well-being[1]. 

However, behavioral studies in our lab suggest that hearing loss may dampen/compress these responses: our participants with hearing loss rated pleasant sounds as less pleasant, unpleasant sounds as less unpleasant. Importantly, current hearing devices, such as hearing aids and cochlear implants do not fully restore them. The neural representation of hearing loss induced compression in emotional response to sound is currently unclear, especially when aided [2,3].

Prior neuroimaging studies guided our experimental design[5,6]. We suspect that compressed emotional response is reflected in the prefrontal cortex, auditory cortex, and perhaps the connectivity between the two.

Helpful reads:
1. Picou, E. M., & Buono, G. H. (2018). Emotional responses to pleasant sounds are related to social disconnectedness and loneliness independent of hearing loss. Trends in Hearing, 22, 2331216518813243.
2. Picou, E. M., Rakita, L., Buono, G. H., & Moore, T. M. (2021). Effects of increasing the overall level or fitting hearing aids on emotional responses to sounds. Trends in hearing, 25, 2]z3312165211049938.
3. Tawdrous, M. M., D'Onofrio, K. L., Gifford, R., & Picou, E. M. (2022). Emotional responses to non-speech sounds for hearing-aid and bimodal cochlear-implant listeners. Trends in Hearing, 26, 23312165221083091.
4. Satpute, A. B., Kang, J., Bickart, K. C., Yardley, H., Wager, T. D., & Barrett, L. F. (2015). Involvement of sensory regions in affective experience: a meta-analysis. Frontiers in psychology, 6, 1860.
5. Plichta, M. M., Gerdes, A. B., Alpers, G. W., Harnisch, W., Brill, S., Wieser, M. J., & Fallgatter, A. J. (2011). Auditory cortex activation is modulated by emotion: a functional near-infrared spectroscopy (fNIRS) study. Neuroimage, 55(3), 1200-1207.
6. Husain, F. T., Carpenter-Thompson, J. R., & Schmidt, S. A. (2014). The effect of mild-to-moderate hearing loss on auditory and emotion processing networks. Frontiers in systems neuroscience, 8, 10.
7. Ferrari, M., & Quaresima, V. (2012). A brief review on the history of human functional near-infrared spectroscopy (fNIRS) development and fields of application. Neuroimage, 63(2), 921-935.






<h2 align="center">The Current Experiment</h2>

Participants of normal hearing comfortably seated in a sound attenuating booth, listened to sounds from the International Affective Digitized Sound Corpus. Each participant listened to 60 six-second sound clips, which consist of 20 pleasant sounds, 20 unpleasant sounds, and 20 neutral sounds. Sound clips were presented in a blocked-design, where each block had four clips of sounds of the same valence (e.g., all four sounds are pleasant). Between blocks, there was 30 second of silence. A question asking 'Did the sounds make you feel pleasant/unpleasant/neither pleasant or unpleasan' was presented after the end of the fourth sound clip, and participants used the 'Enter' button to indicate 'YES'. No action would indicate 'NO'. Sound clips were randomized within blocks, and order of sound blocks were randomized for each participant. The question was used to keep participants engaged in listening and encourage active appraisal. 

Our hypothesis: 
- Relative to neutral sounds, both unpleasant and pleasant sound would elicit greater auditory region acitivities. Due to penetration limits of near infra-red light, our auditory ROIs are secondary auditory cortices. 
- Similarly, we also expect the prefrontal cortex to show stronger activation to both unpleasant and pleasant sounds, relative to neutral sounds.



<h2 align="center">Contributing</h2>

- Review the open issues and choose a task.
- Comment on the issue to let us know that you would like to work on it.
- Fork this repository to your GitHub account.
- Create a new branch with a descriptive name.
- Make and test your changes.
- Commit and push your changes to your fork.
- Submit a Pull Request to this repository.
- Link the Pull Request to the corresponding issue.

<h2 align="center">Open Issues</h2>

- Issue #0: Self Introduction
- Issues #1 - #5: See [Digitization](https://github.com/hpphearscode/fNIRS-emotion-VandyBH26/tree/main/Digitization)
- Issue #6: See [Preprocessing](https://github.com/hpphearscode/fNIRS-emotion-VandyBH26/tree/main/Preprocessing)
- Issues #7 - #10: See [Analysis](https://github.com/hpphearscode/fNIRS-emotion-VandyBH26/tree/main/Analysis)

<br>


<h2 align="center">Credit to Collaborators</h2>
All contributors will be prominently listed on the project’s primary repository documentation. Outstanding contributions that alter or improve the underlying methodology will be offered formal co-authorship on future academic abstracts or manuscript updates, as appropriate and in accordance with standard scientific authorship and contribution practices.