# Dataset Description
The goal of this competition is to identify which direction neutrinos detected by the IceCube neutrino observatory came from. When detection events can be localized quickly enough, traditional telescopes are recruited to investigate short-lived neutrino sources such as supernovae or gamma ray bursts. Because the sky is huge better localization will not only associate neutrinos with sources but also to help partner observatories limit their search space. With an average of three thousand events per second to process, it's difficult to keep up with the stream of data using traditional methods. Your challenge in this competition is to quickly and accurately process a large number of events.

This competition uses a hidden test set. When your submitted notebook is scored the actual test data (including a full length sample submission) will be made available to your notebook. Expect to see roughly one million events in the hidden test set, split between multiple batches.

# Files
[train/test]_meta.parquet

batch_id (int): the ID of the batch the event was placed into.
event_id (int): the event ID.
[first/last]_pulse_index (int): index of the first/last row in the features dataframe belonging to this event.
[azimuth/zenith] (float32): the [azimuth/zenith] angle in radians of the neutrino. A value between 0 and 2*pi for the azimuth and 0 and pi for zenith. The target columns. Not provided for the test set. The direction vector represented by zenith and azimuth points to where the neutrino came from.
NB: Other quantities regarding the event, such as the interaction point in x, y, z (vertex position), the neutrino energy, or the interaction type and kinematics are not included in the dataset.
[train/test]/batch_[n].parquet Each batch contains tens of thousands of events. Each event may contain thousands of pulses, each of which is the digitized output from a photomultiplier tube and occupies one row.

event_id (int): the event ID. Saved as the index column in parquet.
time (int): the time of the pulse in nanoseconds in the current event time window. The absolute time of a pulse has no relevance, and only the relative time with respect to other pulses within an event is of relevance.
sensor_id (int): the ID of which of the 5160 IceCube photomultiplier sensors recorded this pulse.
charge (float32): An estimate of the amount of light in the pulse, in units of photoelectrons (p.e.). A physical photon does not exactly result in a measurement of 1 p.e. but rather can take values spread around 1 p.e. As an example, a pulse with charge 2.7 p.e. could quite likely be the result of two or three photons hitting the photomultiplier tube around the same time. This data has float16 precision but is stored as float32 due to limitations of the version of pyarrow the data was prepared with.
auxiliary (bool): If True, the pulse was not fully digitized, is of lower quality, and was more likely to originate from noise. If False, then this pulse was contributed to the trigger decision and the pulse was fully digitized.
sample_submission.parquet An example submission with the correct columns and properly ordered event IDs. The sample submission is provided in the parquet format so it can be read quickly but your final submission must be a csv.

sensor_geometry.csv The x, y, and z positions for each of the 5160 IceCube sensors. The row index corresponds to the sensor_idx feature of pulses. The x, y, and z coordinates are in units of meters, with the origin at the center of the IceCube detector. The coordinate system is right-handed, and the z-axis points upwards when standing at the South Pole. You can convert from these coordinates to azimuth and zenith with the following formulas (here the vector (x,y,z) is normalized):

x = cos(azimuth) * sin(zenith)
y = sin(azimuth) * sin(zenith)
z = cos(zenith)

# Example Event
The following image shows a visual representation of the features of an IceCube event in the dataset. The colorful dots represent sensors that logged at least one pulse in the event. The size of the dots corresponds to the total charge of all pulses while the color indicates the time of the first pulse.
The left panel shows only pulses with auxiliary==False, and the right panel with auxiliary==True. The small, gray points indicate the positions of all 5160 IceCube sensors. The red arrow shows the true neutrino direction of that event, i.e. the regression target.

![pic](https://github.com/EslamFouadd/Data-Reporter-Project/assets/77150715/f04eb4a5-dc59-4c99-b115-1d74b7aba10d)
