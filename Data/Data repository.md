## Repository links:

- [Main task](https://vanderbilt365-my.sharepoint.com/:f:/g/personal/haiping_huang_vanderbilt_edu/IgBjPMmzTecrTpcg2R41_R7HAXiVJ9OVwvokkb8lJo58rRk?e=rgrgG9)
- [Resting state](https://vanderbilt365-my.sharepoint.com/:f:/g/personal/haiping_huang_vanderbilt_edu/IgAPmP_Gzj0HTI71VW9jF0qZAQRTcyC4IObzB1USQ_91TNA?e=R2JNcY)
- [Mesh (digitized object)](https://vanderbilt365-my.sharepoint.com/:f:/g/personal/haiping_huang_vanderbilt_edu/IgCcFO1ZM24QQ7hXgy4C2fDQAaldcm64un7yAAWXytMsNA4?e=EcfHeE)

Note:
 - Subject IDs are linked across these files.
 - Some participants do not have mesh files due to technical issues during the scan.

## Triggers:

### Resting state: 
- 1 Participant pressed 'Enter' to start the scan. 
- 2 Scanning ended automatically after 6 minutes.

### Main task:
- Condition Presentation Triggers
  - 1 (Pleasant): Starts the presentation of a pleasant stimulus.
  - 2 (Neutral): Starts the presentation of a neutral stimulus.
  - 3 (Unpleasant): Starts the presentation of an unpleasant stimulus.

- Inter-Block Interval (IBI) Triggers
  - 4 (IBI - _P_start): Marks the start of the rest/silent interval before a new group of four pleasant sounds.
  - 5 (IBI - _P_end): Marks the end of this rest/silent interval.
  - 6 (IBI - _N_start): Marks the start of the rest/silent interval before a new group of four neutral sounds.
  - 7 (IBI - _N_end): Marks the end of this rest/silent interval.
  - 8 (IBI_UP_start): Marks the start of the rest/silent interval before a new group of four unpleasant sounds.
  - 9 (IBI_UP_end): Marks the end of this rest/silent interval.

- Engagement Task Triggers
  - 10 (Engage_text_P): Displays the engagement text asking about whether the participant felt pleasant during the sound block.
  - 11 (Engage_text_N): Displays the engagement text asking about whether the participant felt neutral during the sound block.
  - 12 (Engage_text_UP): Displays the engagement text asking about whether the participant felt unpleasant during the sound block.
  - 13 (Engage_text_end): Marks the end of the engagement text display and response window.
  - 15 (Button_press): Logs a physical button press event during the response window of engagement prompt.

- Experiment Control Triggers
  - 14 (End_experiment): Marks the official conclusion of the experimental session.


**License:** [CC BY 4.0](../LICENSE-DATA.md)