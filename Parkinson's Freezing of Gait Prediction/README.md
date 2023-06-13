# Dataset Description
This competition dataset comprises lower-back 3D accelerometer data from subjects exhibiting freezing of gait episodes, a disabling symptom that is common among people with Parkinson's disease. Freezing of gait (FOG) negatively impacts walking abilities and impinges locomotion and independence.

Your objective is to detect the start and stop of each freezing episode and the occurrence in these series of three types of freezing of gait events: Start Hesitation, Turn, and Walking.

# The Datasets
The data series include three datasets, collected under distinct circumstances:

The tDCS FOG (tdcsfog) dataset, comprising data series collected in the lab, as subjects completed a FOG-provoking protocol.
The DeFOG (defog) dataset, comprising data series collected in the subject's home, as subjects completed a FOG-provoking protocol
The Daily Living (daily) dataset, comprising one week of continuous 24/7 recordings from sixty-five subjects. Forty-five subjects exhibit FOG symptoms and also have series in the defog dataset, while the other twenty subjects do not exhibit FOG symptoms and do not have series elsewhere in the data.
Trials from the tdcsfog and defog datasets were videotaped and annotated by expert reviewers documented the freezing of gait episodes. That is, the start, end and type of each episode were marked by the experts. Series in the daily dataset are unannotated. You will be detecting FOG episodes for the tdcsfog and defog series. You may wish to apply unsupervised or semi-supervised methods to the series in the daily dataset to support your detection modelling.

See this page for more on these datasets as well as video examples of freezing of gait events: Additional Data Documentation.

# File and Field Descriptions
train/ Folder containing the data series in the training set within three subfolders: tdcsfog/, defog/, and notype/. Series in the notype folder are from the defog dataset but lack event-type annotations. The fields present in these series vary by folder.
Time An integer timestep. Series from the tdcsfog dataset are recorded at 128Hz (128 timesteps per second), while series from the defog and daily series are recorded at 100Hz (100 timesteps per second).
AccV, AccML, and AccAP Acceleration from a lower-back sensor on three axes: V - vertical, ML - mediolateral, AP - anteroposterior. Data is in units of m/s^2 for tdcsfog/ and g for defog/ and notype/.
StartHesitation, Turn, Walking Indicator variables for the occurrence of each of the event types.
Event Indicator variable for the occurrence of any FOG-type event. Present only in the notype series, which lack type-level annotations.
Valid There were cases during the video annotation that were hard for the annotator to decide if there was an Akinetic (i.e., essentially no movement) FoG or the subject stopped voluntarily. Only event annotations where the series is marked true should be considered as unambiguous.
Task Series were only annotated where this value is true. Portions marked false should be considered unannotated.
Note that the Valid and Task fields are only present in the defog dataset. They are not relevant for the tdcsfog data.

test/ Only the Time, AccV, AccML, and AccAP fields are provided for the test series. See the Evaluation for details on how the hidden Valid and Task annotations affect scoring.

unlabeled/ Folder containing the unannotated data series from the daily dataset, one series per subject. Forty-five of the subjects also have series in the defog dataset, some in the training split and some in the test split. Accelerometer data has units of g.

tdcsfog_metadata.csv Identifies each series in the tdcsfog dataset by a unique Subject, Visit, Test, Medication condition.

Visit Lab visits consist of a baseline assessment, two post-treatment assessments for different treatment stages, and one follow-up assessment.
Test Which of three test types was performed, with 3 the most challenging.
Medication Subjects may have been either off or on anti-parkinsonian medication during the recording.
defog_metadata.csv Identifies each series in the defog dataset by a unique Subject, Visit, Medication condition.

daily_metadata.csv Each series in the daily dataset is identified by the Subject id. This file also contains the time of day the recording began.

subjects.csv Metadata for each Subject in the study, including their Age and Sex as well as:

Visit Only available for subjects in the daily and defog datasets.
YearsSinceDx Years since Parkinson's diagnosis.
UPDRSIIIOn/UPDRSIIIOff Unified Parkinson's Disease Rating Scale score during on/off medication respectively.
NFOGQ Self-report FoG questionnaire score. See:
https://pubmed.ncbi.nlm.nih.gov/19660949/
events.csv Metadata for each FoG event in all data series. The event times agree with the labels in the data series.

Id The data series the event occured in.
Init Time (s) the event began.
Completion Time (s) the event ended.
Type Whether StartHesitation, Turn, or Walking.
Kinetic Whether the event was kinetic (1) and involved movement, or akinetic (0) and static.
tasks.csv Task metadata for series in the defog dataset. (Not relevant for the series in the tdcsfog or daily datasets.)

Id The data series where the task was measured.
Begin Time (s) the task began.
End Time (s) the task ended.
Task One of seven tasks types in the DeFOG protocol, described on this page.
sample_submission.csv A submission file in the correct format. Please see the Evaluation page for more details.

# Data Splits
Please note that this is a Code Competition, in which the actual test set is hidden. In this public version, we give some sample data drawn from the training set to help you author your solutions. When your submission is scored, this example test data will be replaced with the full test set.

The test set contains about 250 data series. The series from the tdcsfog and defog are in a proportion similar to that of the training set. These series have subjects that are entirely distinct from those in the training set. This also holds true for the public / private test split. (In other words, the train / public test / private test splits were formed by grouping on subjects and stratifying on datasets.)

Most, but not all, subjects in the defog test set have unannotated series in the daily dataset.

All of the series in the daily dataset are in the public version of the data. There are no additional unannotated series in the hidden dataset.

The tdcsfog_metadata.csv, defog_metadata.csv, and subjects.csv files in the hidden version of the data contain additional entries for the test set series. The hidden versions of these files are supersets of the public versions.

The events.csv, tasks.csv, and daily_metadata.csv files are the same in both the public and hidden datasets.

# Data Source:
https://www.kaggle.com/competitions/tlvmc-parkinsons-freezing-gait-prediction/data
