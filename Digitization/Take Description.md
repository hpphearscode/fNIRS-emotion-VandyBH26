# 2026 Vanderbilt BrainHack Project: Enlightening the Emotional Brain

## Digitization and Co-registration

### Why do we perform co-registration?

- In many fNIRS studies, people make optode-anatomy associations based on a standardized template, such as the MNI space.
- But everyone's head differs in size, shape, etc. 
    - Even when using the same cap, the same optodes may be covering different, adjacent brain regions.
    - This problem is more severe if the cap size does not align with one's head circumference. This is quite common in fNIRS studies. Many labs have 2-3 caps ready to go, but very often participants' head sizes go beyond the size range. Unlike EEG, it is usually very costly to have many fNIRS caps of different sizes set-up at the same time.
- Therefore, to make appropriate interpretations, we should know how much the optodes on a given participant's head deviate from the underlying anatomy, based on a standardized template. You could also think of this process as normalizing the coordinates. 

### How are we currently doing it?

- We are currently using [Structure Sensor III](https://structure.io/?gad_source=1&gad_campaignid=22794124010&gbraid=0AAAAA9c7Ky4hqyHtVNQJ-jQBlpQJvrkzU&gclid=CjwKCAjw7p_UBhBlEiwAhpIs75k6WOIF8CXM4O9HWXP_G1X0QeqBqN_Y8tBVCj1J-EYpxG_nrf1HQxoCMYIQAvD_BwE). It is a 3D body scanner built for healthcare professionals. It projects an invisible infrared dot pattern onto objects and uses synchronized cameras to measure how the pattern warps. The output file format is currently .obj.
- We are currently using the [FieldTrip toolbox](https://www.fieldtriptoolbox.org/) for co-registration.


Fieldtrip workflow 
Read in the .obj file
Label fiducials, Nz, Lpa, Rpa, Iz, Cz (if available)
Label, and populate optodes on the participant's head
Co-register to MNI space.

### How you can contribute:

You may find .obj files [here](https://github.com/hpphearscode/fNIRS-emotion-VandyBH26/tree/main/Digitization/Sensor%20Output)

<p align="center">
<img
  align="center"
  width="300"
  alt="The international 10–20 electrode placement system"
  src="../Assets/the-10-20-system-with-percentages.gif"
/>
<br>
image source: Shriram, R., Sundhararajan, M., & Daimiwal, N. (2013). EEG based cognitive workload assessment for maximum efficiency. Int. Organ. Sci. Res. IOSR, 7, 34-38.
</p>




- Locating Cz and Iz after capping is challenging, especially on participants with thicker hair. Nz, Lpa, Rpa are easiest as they are usually not covered by the cap of hair. Iz is slightly easier than Cz because often times it is prominent enough to identify in the mesh. But Cz is especially hard.
    - **Challenge #1: Develop code to estimate Cz location for each participant**.
    - FieldTrip has pieces of code that may aid this process. An alternative I have not investigated is [Cedalion](http://cedalion.tools/) in python.
    - We proivde Structure Sensor and fNIRS cap at the BrainHack event to help you experiment.
- Manually label optodes can be tedious. Given that spatial relationship among optodes exist in NIRx recording files and can be extracted. We also have a 2D montage 10-20 layout.
    - **Challenge #2: Develop code to automate optode lablling.**

