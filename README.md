
## **Higgs Boson Classification**


### **Problem Statement**

- The task is to classify whether **signal or background**

![logo](https://github.com/sureshmecad/Higgs-Boson-Decay-TMLC/blob/main/image/Higgs.JPG)

In particle physics, Higgs Boson to tau-tau decay signals are notoriously difficult to identify due to the presence of severe background noise generated by other decaying particles. This approach uses neural networks to classify events as signals or background noise.

**Keywords:** Machine Learning, Binary Classification

### **Introduction**
Discovery of the Higgs boson was announced at CERN in July 2012. High-energy physicists now are on a quest to measure its characteristics, such as the Higgs decay modes, and determine if it fits the current model of nature.

ATLAS is a particle physics experiment installed at the Large Hadron Collider at CERN that searches for new particles and processes using head-on collisions of protons of extraordinarily high energy. The ATLAS experiment has observed a signal of the Higgs boson decaying into two tau lepton particles, but this process is a small signal buried in "background" noise.

The goal of the Higgs Boson Machine Learning Challenge is to explore the potential of machine learning methods to improve the discovery significance of the experiment. Using simulated data with features characterizing events detected by ATLAS, the task is to classify events into "tau tau decay of a Higgs boson" versus "background."

A data set of 250,000 "training" events is given, including their weight w (a continuous quantity), and their character (signal or background). In the simulated set, there is a sharp threshold in w separating signals (w < 0.05) and background (w > 0.05). The challenge asks to classify 550,000 data points in a test set as signal or background, including a likelihood ranking. The scoring algorithm takes into account the aggregate weights of both "true positives" (signals correctly identified) and "false positives" (background events mistaken for signals), but none of the "negatives" (data evaluated as background, rightly or wrongly).

### **Approach**

**Split into Subclasses**
Examination of the training data showed that the set contained a mix of four different physical decay mechanisms that involved any number between 0 and 3 "hadronic jets." Features that described jet properties often required a minimum number of jets present; otherwise they were meaningless and marked as "missing." After sorting the training set into classes by number of jets (with generally increasing number of relevant features), missing data was confined to a single data column, the predicted mass of the Higgs boson. As a workaround, I split each jet class further into events with and without predicted mass (which mostly provided background), ending with 8 distinct classes of events, but no missing data.

**Data Preprocessing**
Considering the definitions of different columns, and physical symmetries (like rotational symmetry) underlying the data, I found that certain sets of variables were linearly dependent, or irrelevant (e.g., only differences between angles have physical meaning). Irrelevant features were removed, and linearly dependent sets reduced to basis sets. Momentum-related features showed a wide range of values, with a skewed distribution toward small values. They were transformed into a more compact distribution by application of the logarithm. (The same was true for the attributed weights w of events.) All non-periodic features (i.e., everything but angle differences) were finally normalized to zero mean and unit variance.

**Feature Creation**
Preprocessing yielded classes with as little as 10 meaningful features. In order to expand the flexibility of the linear regression approach, I decided to multiply each column into a number of generated features by "Gaussian splits," defined by the overlap between a feature and a set of shifted Gaussians, in the spirit of kernel methods. Experiments showed that classifier improvement tapered off with 4- to 8-fold splits of each feature, so I settled on 8-fold splits for the competition.


## **Deployment Link**
https://higgsbosondecay.herokuapp.com/

![logo](https://github.com/sureshmecad/Higgs-Boson-Decay-TMLC/blob/main/image/Deploy_Higgs.JPG)



