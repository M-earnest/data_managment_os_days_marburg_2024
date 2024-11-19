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

### raw

### derivatives


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