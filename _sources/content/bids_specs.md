# BIDS (Brain Imaging Data Structure)

##  Motivation

The Brain Imaging Data Structure (BIDS) is a simple and intuitive way to organize and describe data.

Neuroimaging experiments produce complex datasets that are often organized inconsistently, even within the same lab. This lack of standardization can lead to misunderstandings, wasted time, and inefficiencies in data reuse and collaboration. Below, we outline the benefits of adopting a standardized approach, specifically the Brain Imaging Data Structure (BIDS)

- scientific projects especially in the neuroscience are necessarily complex, being organized and providing proper documentation and meta information is a key factor
- Early stage resaearchers have a distinct adavantage of not being bogged down by their already exiting backlogs

### BIDS adavantages:

### 1. Interoperability with Software:
- a growing number of data analysis tools and apps support BIDS-formatted datasets
- adopting BIDS enhances compatibility and facilitates analysis workflows

### 2. Facilitates Public Data Sharing:
- public databases such as OpenNeuro.org require BIDS-compliant datasets.
- journals increasingly require public sharing of datasets; using BIDS minimizes the effort and time required for curation and publication.

### 3. Validation Tools:
- ools like the BIDS Validator check dataset integrity and help identify missing or incorrect data entries.

### 4. Alignment with FAIR Principles
The adoption of BIDS aligns with the FAIR principles, enhancing the scientific impact of neuroimaging datasets:
```
    F - Findable:
        BIDS encourages consistent naming conventions and metadata organization, making datasets easy to locate and index, whether within a lab or on public repositories.
    A - Accessible:
        Structured datasets, with rich metadata, are easily accessible to both humans and machines, increasing usability across tools and platforms.
    I - Interoperable:
        By adhering to universal standards, BIDS ensures compatibility with a wide range of software and computational workflows, promoting cross-disciplinary collaboration.
    R - Reusable:
        Detailed metadata and standardization ensure datasets can be reused effectively, whether for replication, secondary analysis, or integration into meta-analyses.
```


### The core specification


Requirement levels:

REQUIRED: Data cannot be be interpreted without this information (or the ambiguity is unacceptably high)
RECOMMENDED: Interpretation/utility would be dramatically improved with this information
OPTIONAL: Users and/or tools might find it useful to have this information


Modalities:
- passive neuroimaging techniques are organized by their own labels: eg, meg and ieeg
- active neuroimaging techniques are organized by the respective category of brain data recorded, e.g for MRI: T1w, bold or dwi etc.


### Folder structure
Within BIDS folders have to be structured and named in a specific way. The hierarchy is as follows:

```
- project/
    - code/
    - derivatives/
    - phenotype/
    - sourcedata/
    - stimuli/
    - subject/
        - session/
            - datatype/
```



The **project** folder has not to be named in a specific manner, but it should be descriptive.

**code**
Here you can store any code
*phenotype*
Here you can store spearated into individual files any participant level measurements (e.g. responses from questionnaires)

*sourcedata*
Here you can store data before harmonization, reconstruction and/or file format conversion
*stimuli*
Self-explanatory, but here you can store your stimuli

```
subject/:
      - There should be one subject folder for each participant. Naming of subject folders has to be as follows:
            sub-particpant label
            exchange participant label with a label that is unique for each participant in your dataset (can be numbers and/or letters)

      session/
            You only need this, if there are multiple sessions. A participant does not leave the scanner/headset during a session.
            Sessions are named as follows:
            ses-session label
            exchange `session label` with a label that is unique (can be numbers and/or letters)

            datatype/
                  This folder shows the modality of the acquired data, like EEG data (`eeg`), behavioral data (`beh`), fMRI data (`func`) or much more. You can find a list of modalities and their naming conventions [here](https://bids-website.readthedocs.io/en/latest/getting_started/folders_and_files/folders.html)

```


An example from the BIDS Specification would look something like this



## derivatives
Derivatives are 

- processed data:
      - fundamentally different to the source data and therefore is likely to differ in datatypes from the original (e.g. masks and segmentations).
- preprocessed data:
      - fundamentally similar to source data (e.g removing of artifacts etc.)


There are several ways to organize them within your folder structure. For more information have a look [here](https://bids-website.readthedocs.io/en/latest/getting_started/folders_and_files/derivatives.html)


## Required Files


These files are essential for understanding and interpreting the dataset. Without them, the dataset would be incomplete or ambiguous.

1. Dataset-Level Files:
- dataset_description.json: Describes the dataset, including its name, version, and authors. Essential for dataset identification and interpretation.
- participants.tsv: Contains demographic or other participant-level information (e.g., age, sex, group).
- sub-<label> directories: Each participant's data must be organized under a directory named with their unique identifier.

2. Modality-Specific Data Files:
- Imaging data files (e.g., sub-<label>/anat/sub-<label>_T1w.nii.gz): The actual neuroimaging data (e.g., T1-weighted anatomical images, functional MRI, etc.).
- Sidecar JSON files (e.g., sub-<label>/anat/sub-<label>_T1w.json): Provide metadata for the associated imaging files, such as acquisition parameters and scanner details.

3. Task-Specific Files (if functional data is included):
- task-<label>_bold.nii.gz: The BOLD fMRI time series.
- task-<label>_events.tsv: The timing and nature of stimuli presented during the task.


Files Required in BIDS and Their Requirement Levels

The Brain Imaging Data Structure (BIDS) specification categorizes its files into REQUIRED, RECOMMENDED, and OPTIONAL, depending on their importance for data interpretation and utility. Here's a breakdown:


## RECOMMENDED Files

But really, please provide them!

These files significantly enhance the interpretability and utility of the dataset but are not strictly necessary, they are mostly for human readers and help others understand what they see.

1. Additional Dataset-Level Metadata:
        README: General information about the dataset, such as study purpose or known issues.
        CHANGES: Version history of the dataset, useful for tracking updates.

2. Additional Participant Information:
        participants.json: Describes the columns in participants.tsv, such as units or definitions for demographic fields.

3. Additional Imaging Metadata:
        Field maps (fmap/): Useful for correcting distortions in functional or diffusion MRI data.
        Additional anatomical modalities (e.g., T2-weighted images, sub-<label>_T2w.nii.gz).


## Metadata


### dataset_description.json:
```
      Purpose: A structured JSON file containing essential metadata to identify and describe the dataset.
      Required Fields:
      Name: The title or name of the dataset.
      BIDSVersion: The version of the BIDS specification used.
      Authors: A list of individuals responsible for the dataset.
      Funding (optional): Information about the funding sources for the study.
      DatasetDOI (optional): The DOI or other persistent identifier for the dataset if published.
      Importance:
      Acts as a reference document for dataset context.
      Facilitates proper citation and acknowledgment.

```

### participants.tsv:
```
        Purpose: A tab-separated values (TSV) file containing participant-level information.
        Required Columns:
            participant_id: Unique identifier for each participant.
            Optional but recommended fields include age, sex, and group (e.g., control or experimental).
        Importance:
            Allows researchers to understand the demographic distribution of participants.
            Provides key grouping variables for analysis (e.g., age groups or experimental conditions).
```

### sub-<label> directories:
```
        Purpose: Each participant’s data is stored in its own directory, named with their unique identifier (e.g., sub-001).
        Structure:
            Organized hierarchically to separate anatomical, functional, and other modalities.
            Ensures clarity and avoids ambiguity in data association.
```

## BIDS extensions

As you've seen BIDS is split into modality agnostic files, i.e.


    dataset_description.json
    README[.md|.rst|.txt]
    CITATION.cff
    CHANGES
    LICENSE

and modality specific files, which are dependent on the specifics of the hard- and software necessary. This necessarily influences how and which metadata is required or expected to be shared. In the following we will explore to modality specific examples.

### BIDS Conversion tools 



#### MNE BIDS

- https://mne.tools/mne-bids/stable/auto_examples/convert_mne_sample.html#sphx-glr-auto-examples-convert-mne-sample-py



#### MRI?

- https://reproducibility.stanford.edu/bids-tutorial-series-part-2a/
