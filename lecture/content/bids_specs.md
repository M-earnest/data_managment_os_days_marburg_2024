# BIDS (Brain Imaging Data Structure)

## Intro

The Brain Imaging Data Structure (BIDS) is a simple and intuitive way to organize and describe data.

###  Motivation

- Lack of consensus (or a standard) leads to misunderstandings and time wasted on rearranging data or rewriting scripts expecting certain structure
- scientific projects especially in the neuroscience are necessarily complex, being organized and providing proper documentation and meta information is a key factor
- 
- Early stage resaearchers have a distinct adavantage of not being bogged down by their already exiting backlogs






FAIR

- integrate: - https://bids-specification.readthedocs.io/en/stable/introduction.html

F - findable:

I - interoperable:

R - reusable:

### The core specification


Requirement levels:

EQUIRED: Data cannot be be interpreted without this information (or the ambiguity is unacceptably high)
RECOMMENDED: Interpretation/utility would be dramatically improved with this information
OPTIONAL: Users and/or tools might find it useful to have this information


Modalities:
- passive neuroimaging techniques are organized by their own labels: eg, meg and ieeg
- active neuroimaging techniques are organized by the respective category of brain data recorded, e.g for MRI: T1w, bold or dwi etc.


... 

How best to break down the basic list here?

https://bids-specification.readthedocs.io/en/stable/common-principles.html



### Folder structure
Within BIDS folders have to be structured and named in a specific way. The hierarchy is as follows:

- **project**
    - code
    - derivatives
    - phenotype
    - sourcedata
    - stimuli
    - subject
        - session
            - datatype

The **project** folder has not to be named in a specific manner, but it should be descriptive.
#### code
Here you can store any code
#### phenotype
Here you can store spearated into individual files any participant level measurements (e.g. responses from questionnaires)
#### sourcedata
Here you can store data before harmonization, reconstruction and/or file format conversion
#### stimuli
Self-explanatory, but here you can store your stimuli
#### subject
There should be one subject folder for each participant. Naming of subject folders has to be as follows:

`sub-*particpant label*`

exchange *participant label* with a label that is unique for each participant in your dataset (can be numbers and/or letters)
#### session
You only need this, if there are multiple sessions. A participant does not leave the scanner/headset during a session.

Sessions are named as follows:
`ses-*session label*`

exchange *session label* with a label that is unique (can be numbers and/or letters)
#### datatype 
This folder shows the modality of the acquired data, like EEG data (`eeg`), behavioral data (`beh`), fMRI data (`func`) or much more. You can find a list of modalities and their naming conventions [here](https://bids-website.readthedocs.io/en/latest/getting_started/folders_and_files/folders.html)
### derivatives
Derivatives are 

- processed data:
      - fundamentally different to the source data and therefore is likely to differ in datatypes from the original (e.g. masks and segmentations).
- preprocessed data:
      - fundamentally similar to source data (e.g removing of artifacts etc.)

There are several ways to organize them within your folder structure. For more information have a look [here](https://bids-website.readthedocs.io/en/latest/getting_started/folders_and_files/derivatives.html)
### metadata
There are two important file types to store metadata:
#### JSON files
- **J**ava**S**cript **O**bject **N**otation
- they are text-based and consist of key-value pairs with the option for nesting and arrays
##### Editing
- *Visual Studio Code* (VS Code) is best for editing json files locally
##### Programming
**Python**
- there is a built-in library to read (`json.load()`) and write (`json.dump`) JSON files
**R**
- You can use the **jsonlite** package and read (`fromJSON()`) and write (`writeLines`) JSON files
#### TSV files
- **t**ab-**s**eparated **v**alues
- organized as tables
- columns: fields
- rows: data points
##### descriptions.tsv
- it is optional but recommended
- documents processing steps in derivative dataset

**columns**
- `desc_id`
      - unique labels that are used within the dataset
      - sub-001_task-listening_desc-preproc_eeg.edf: here `desc-preproc` would be a desc_id, but within the column you would just write: `preproc`
- `description`
      - free-form text
      - describes desc_id labels
      - has to appear second
    
##### Programming
**Python**
- you will need the **Pandas** library (`pd`).
- you can read (`pd.read_csv(your_tsv, delimiter = '\t)`) and write (`your_dataframe.to_csv(name, sep = 't')`) tsv files
**R**
- you can easily use `read.table()` und `write.table()`
For more information have a look [here](https://bids-website.readthedocs.io/en/latest/getting_started/folders_and_files/metadata.html)

### practical example: BIDS extensions

As you've seen BIDS is split into modality agnostic files, i.e.


    dataset_description.json
    README[.md|.rst|.txt]
    CITATION.cff
    CHANGES
    LICENSE

and modality specific files, which are dependent on the specifics of the hard- and software necessary. This necessarily influences how and which metadata is required or expected to be shared. In the following we will explore to modality specific examples.


#### MNE BIDS

- https://mne.tools/mne-bids/stable/auto_examples/convert_mne_sample.html#sphx-glr-auto-examples-convert-mne-sample-py



#### MRI?

- https://reproducibility.stanford.edu/bids-tutorial-series-part-2a/
