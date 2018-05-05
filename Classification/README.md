# Classification

Regression involves predict a continuous-valued response. Classification involves predicting a categorical response. Classification problems tend to occur even more frequently than regression problems in practice. Just like regression, 

- Classification cannot be performed blindly in high-dimensions **because you will get zero training error but awful test error**.
- Properly estimating the test error is crucial.
- Classical classification approaches can be extended to high-dimensions, which we have seen in regression contexts.

There are many approaches out there for performing classification. These include

- Model-based methods: 
  - Logistic regression
  - LDA
  - QDA
  
- Non-parametric methods: KNN classification

- Margin-based classifiers: support vector machines (SVM)

The only difference from regression is that response y is a categorical variable with K categories. We mostly focus on K = 2. 

### Drawbacks of Linear Regression for Classification

If we code the values of y as 0 and 1 (instead of -1 and 1), then the linear regression gives an estimate of the probability P(y = 1 | X), which is sensible. However, there is no guarantee that the estimated probabilities are in fact between 0 and 1. And in general, they are actually not. 

There is also a serious problem if y has more than 2 categories. 
- Suppose that we are trying to predict the medical condition of a patient in th emergency room on the basis of her symptoms, and there are three possible diagnoses: stroke (coded as 1), drug overdose (coded as 2), and epileptic seizure (coded as 3). 
- Unfortunately, this coding implies an ordering on the outcomes, putting drug overdose between stroke and epileptic seizure. 
- In practice, there is no particular reason that this needs to be the case and one could choose any other equally reasonable coding. 

### 0-1 Loss & Optimal Classifier

- A natural loss function for categorical data is the 0-1 loss function which counts how many cases are classified incorrectly.
- As in the setting of linear regression, in general we want to estimate a function that gives the smallest 0-1 loss.
- Using this loss function, a good classifier is one for the test error is minimized.
- It turns out that the test error based on 0-1 loss is minimized by if we assign each observation to the most likely cases, given its predictor values P(Y = k | X = x_0). This is known as the **Bayes classifier**. In general, we cannot use this unless we know the joint probability distribution. 
  - We can also get the Bayes error rate, which is the lowest test error we can get. 

## High Dimensional Classification 
- Classification using linear regression
- Logistic regression (and penalized logistic regression)
- KNN classification
- LDA & QDA
- Support Vector Machines (SVM)

## Logistic Regression
- Straightforward extension of linear regression to the classification setting
- For simplicity, suppose y in {0,1}: a two-class classification problem.
- Instead logistic regression assume a parametric model. 
- If this assumption holds, logistic regression, is a good model-based alternative to Bayes classifier.

### Breast Cancer Subtypes Example

In the past 10 years, global gene expression analyses have identified at least 4 subtypes of breast cancer: 

1. Luminal A
2. Luminal B
3. Her2-enriched
4. Basal-like

Subgroups differ with respect to risk factors, incidence, baseline prognoses, response to therapies. Want to able to determine the subytpe for a new patient with breast cancer. Controversy over the best classifier for this task: 

- PAM50 classifier involves 50 genes.
- More recent proposal involving three genes.

Moving taret: nobody knows the "true" subtype. 

Citation: Prat et al., Breast Cancer Res Treat, 2012

### Proteomics for Ovarian Cancer

Ovarian cancer is the leading cause of gynecologic cancer deaths in the USA. Much interest in detecting the cancer at an earlier stage. In 2002, Petricon and Liotta - investigators from LDA and NCI - reported in the *The Lancet* that mass spectrometry analysis of circulating serum proteins can be used to discriminate between healthy patients and those with ovarian cancer. Great enthusiasm in popular press and general public. Planes were made to begin marketing a test absed on the reported diagnostic.

Independent researchers took a look at the data, which was publicly available, and discovered: 

1. Inadvertent changes in protocol mid-experiment: major batch effects present.
2. Problems with instrument calibration.
3. Difference in processing between tumor and normal samples.

In summary: the observed differences between cancer and normal proteomic patterns were attributable to "artifacts of sample processing, not the underlying biology of cancer."

### Gene Expression Signatures for Cancer Treatment

In the early 2000s, Joe Nevins, Anil Potti, and other researchers at Duke University began developing expression-based predictors of response to chemotherapy. Many (dozens of) very promising and very high-profile papers were published in *Nature Medicine*, *The Lancet*, *Journal of Clinical Oncology*, and more. Several clinical trials were initiated, using these predictors to direct therapy for cancer patients. This reserach was hailed as a major breakthrough in cancer treatment, and researchers from all over the world tried to use these sorts of techniques in their own labs.

Upon closer inspection: 

Using the fact that some of the data were publicly available, independent reserachers discovered the following errors (among many others): 

- Off by one errors in gene lists
- The same heatmap displayed in multiple (unrelated) papers
- Gene not measured on the array were reported as being part of the predictor obtained, and as providing evidence for biological plausibility
- Reversal of sensitive/resistant labels

A shocking paper published by Baggerly and Coombes in *Annals of Applied Statistics*, detailing all the errors made: "One theme that emerges is that the most common errors are simple (e.g., row or column offsets); conversely, it is our experience that the most simple errors are common."

What went wrong? 

- Need to have a proper independent test set, that you simply cannot peek at under any circumstances. 
- Need to have clearly documented code that contains all steps of all the analysis, from start to finish.  You must be able to share this code with independenet researchers, and you must be confident that your code is correct. If not, then your work is not ready.

## Comparing and Contrasting LDA & QDA

Linear Discriminant Analysis (LDA) 

- Assume f_h(x) has Gaussian density.

Quadratic Discriminant Analysis (QDA)