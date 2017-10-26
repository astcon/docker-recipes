This is a container library for the Event Horizon Telescope (EHT).  The directory "bin/" contains convenience scripts that make Docker easier to use.  The following directories container Dockerfiles for building container images that are used in processing EHT data.

- difx: the DiFX 2.5.1 package for correlating EHT observations.

- aips: the National Radio Astronomy Observatory (NRAO) Astronomical Image Processing System (AIPS) for interactive calibration and editing of radio interferometric data.  To make Kazu Akiyama's AIPS pipeline work, both 31DEC16 and 31DEC17 are included in this image.

- hops: the Haystack Observatory Postprocessing System (HOPS) for processing data generated by a MkIII, MkIV, or DiFX VLBI correlator.

- eat: the EHT Analysis Toolkit (EAT), together with AIPS, HOPS, and useful python packages for analysis EHT data.

- eat-notebook: the EAT image with Jupyter Notebook support.

- eat-lab: the EAT image with Jupyter Lab support
