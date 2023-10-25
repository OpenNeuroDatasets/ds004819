README
Information
===========

This project contains the data for the publication Paulk et al, "Local and distant cortical responses to single pulse intracranial stimulation in the human brain are differentially modulated by specific stimulation parameters".

It contains the raw and preprocessed (bipolarized and epoched) intracranial EEG (iEEG) data files for 52 participants (subjects) with intractable epilepsy implanted with intracranial electrodes for clinically indicated purposes. The data set involves the use of direct electrical stimulation to examine effects of stimulation in the brain.

Contact: Angelique C. Paulk (apaulk@mgh.harvard.edu)

If you use this data as a part of any publications, please use the following citation:

Paulk AC, Zelmann R, Crocker B, Widge AS, Dougherty DD, Eskandar EN, Weisholtz DS, Richardson RM, Cosgrove GR, Williams ZM, Cash SS (2022) Local and distant cortical responses to single pulse intracranial stimulation in the human brain are differentially modulated by specific stimulation parameters. Brain Stimul Available at: https://www.sciencedirect.com/science/article/pii/S1935861X22000456.

Task Description
----------------

This is a simple passive stimulation task in which participants were awake awake and were aware that they were being stimulated but were blind to the stimulation timing and parameters.
A trained electroencephalographer examined ongoing recordings for epileptiform activity and asked participants if they experienced any sensations. 

Dataset and Stimuli
----------------

This data is organized according to the Brain Imaging Data Structure specification, following the iEEG BIDS formatting (https://www.nature.com/articles/s41597-019-0105-7). A community-driven specification for organizing neurophysiology data along with its metadata. For more information on this data specification, see https://bids-specification.readthedocs.io/en/stable/

Each subject has their own folder (e.g., `sub-3t7p`) which contains the raw iEEG (both sEEG and ECoG) data for that subject,as well as the metadata needed to understand the raw data and event timing as well as an 'anat' folder for the preimplantation structural deidentified T1 MRI (preimp) and the postimplantation deidentified CT or MRI (postimp).

Stimuli
-------

Stimulation was controlled via a custom Cerestim API via MATLAB or a custom C++ code (https://github.com/Center-For-Neurotechnology/CereLAB).Waveforms of two different durations were used: .233 µs duration: 90 µs charge-balanced biphasic symmetrical pulses with an interphase interval of 53 µsec with between 5 and 100 trials with a median of 20 trials per stimulation site across the data set .and 2) 1053 µs (~1 msec) duration: 500 µs charge-balanced biphasic symmetrical pulses with an interphase interval of 53 µsec with between 10 and 26 trials per stimulation site with a median of 10 trials per site. .The interval at 53 ms was required as a hardware-limited minimum interval between square pulses with the CereStim stimulator. For varying Current Amplitude tests, multiple current amplitudes were applied with the short duration (233 µsec) bipolar stimulation at the following steps: 0.5 mA to 10 mA at 0.5 mA steps with a minimum of 10 trials per stimulation site. For train stimuli, each trial delivered a 400 ms train (90 ms charge-balanced biphasic symmetrical pulses with an interphase interval of 53 msec) with varying pulse frequencies (10-200 Hz) and amplitudes (0.5-10 mA).
 
Electrodes
----------
Participants underwent stereo-electroencephalography (sEEG) (n=52), with implantation of multi-contact depth electrodes, and a subset (n=3) implanted with either grid or strip electrodes (a.k.a. ECoG) to locate epileptogenic tissue in relation to essential cortex (Supplemental Table 1). Data with stimulation via the grid or strip electrodes were not included in the analyses here though we did examine the recordings from the sEEG and ECoG electrodes during sEEG stimulation. Depth electrodes (Ad-tech Medical, Racine WI, USA, or PMT, Chanhassen, MN, USA) with diameters 0.8–1.27 mm and 4-16 platinum/iridium-contacts 1-2.4 mm long with inter-contact spacing ranging from 4-10 mm (median 5 mm) were placed stereotactically, based on the clinical indications for seizure localization determined by a multidisciplinary clinical team independent of this research. Following implant, the preoperative T1-weighted MRI was aligned with a postoperative CT using volumetric image coregistration procedures and FreeSurfer scripts (http://surfer.nmr.mgh.harvard.edu). Electrode coordinates were manually determined from the CT in the patients’ native space and mapped using an electrode labeling algorithm (ELA;) that registered each contact to a standardized cortical map. 

Recordings
----------
The EEG data distributed here was recorded at 2000Hz, using a Blackrock recording system, split into two Neural Signal Processor (NSP1 and NSP2; 128 channels each) and a 16-bit A/D converter. Triggers were sent to each NSP to allow for synchronization between the systems. The signal was filtered in the recording system with a high-pass filter with a time constant of 1 second (cut-off frequency ~ 0.16Hz) and a low-pass filter with a cut-off frequency of 1000 Hz.

NOTE on the raw recordings
--------------------------
Each NSP is a separate device, requiring, with recordings, that we need to stop and start NSP1 (EEGBank1) separate from NSP2 (EEGBank2). This leads to jittered timing differences in the duration in the recordings between NSP1 and NSP2. The issue is that the Neural Signal Processors (NSPs) are two separate machines and can have some jitter or lag between one another in the recordings themselves.

The way to work with this data is to use the triggers in each NSP recording (saved in the analog input channels) to align the data correctly to each other. 
We also recommend getting the data into a trialed form, where each trial is -2 to +4 seconds (or some range of seconds) around the stimulation triggers which are saved in the 'sub-*NSP1_run-XX_events.tsv' file (for NSP1) and the 'sub-*NSP1_run-XX_events.tsv' file (for NSP2) with additional details and information regarding the stimulation parameters and stimulation onset and offset in the events file. These trigger times were then detected for NSP1 (with its own triggers) separate from NSP2 (with its own triggers) and then saved separately in each events file. The corresponding NSP1 events then match to the corresponding '*NSP1_run-XX_ieeg.eeg' data. 

Raw data
--------

Raw data is stored with the Brainvision data format. This can be read in to memory with the following tools:

* Python: The `pybv` package (https://github.com/bids-standard/pybv)
* Matlab: BrainVision analyzer (https://www.mathworks.com/products/connections/product_detail/brainvision-analyzer.html)

Ethics statement
----------------
All patients voluntarily participated after fully informed consent as monitored by the Partners Institutional Review Board covering Brigham and Women’s Hospital (BWH) and Massachusetts General Hospital (MGH). Participants were informed that participation in the stimulation tests would not alter their clinical treatment in any way, and that they could withdraw at any time without jeopardizing their clinical care. 

License
-------
This dataset (EEG and MRI data) is proprietary of the Massachusetts General Hospital and Brigham and Women's Hospital under the PDDL (Open Data Commons Public Domain Dedication and License) which is the License to assign public domain like permissions without giving up the copyright.


Acknowledgements
----------------
We would like to thank Giovanni Piantoni, Jean-Baptiste Eichenlaub, Erica Johnson, Gavin Belok, Mia Borzello, Kara Farnes, Dan Soper, Constantin Krempp, Jaquelin Dezha-Peralta, and Pariya Salami for help in data collection. We would like to especially thank the patients for participating in the study. 

Funding 
-------
 Support included NIH grants MH086400, DA026297, and EY017658 to ENE, MH109722, NS100548, and MH111872 to ASW, NS100548 to DDD, and ECOR, NINDS K24-NS088568 to SSC and Tiny Blue Dot Foundation to SSC, ACP, and RZ. A United States Department of Energy Computational Sciences Graduate Fellowship [DE-FG02-97ER25308] supported BC. Some of this research was sponsored by the U.S. Army Research Office and Defense Advanced Research Projects Agency (DARPA) under Cooperative Agreement Number W911NF-14-2-0045 issued by ARO contracting office in support of DARPA’s SUBNETS Program. The views and conclusions contained in this document are those of the authors and do not represent the official policies, either expressed or implied, of the funding sources. 


