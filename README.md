
<br>

## Background

Organisations identify or detect words/strings of interest within documents or data blobs for a variety of purposes, e.g., knowledge graph development, text redaction, criminal investigations, etc.  Organisations may opt for manual word detection if off-the-shelf solutions cannot address their needs.  For example, most redaction software solutions focus on detecting and redacting words/strings of a narrow set of categories, and it is rarely possible to adapt the solution to the detection of words/strings of bespoke categories.
<br><br>  
A viable solution strategy involves the creation of custom models via <i>named entity recognition</i> machine learning algorithms; also known as token classification algorithms. These algorithms can be trained by domain or problem, leading to compact, domain specific, word/string detection models.  
This project publishes an adaptable token classification modelling set-up, i.e., artificial/machine learning engineers can fork and adapt the repositories to their (a) token classification problem, (b) development environment, and (c) the <a href="https://github.com/membranes/text/blob/master/src/models/interface.py#L70">range of language models</a> that they would like to try.  The latter point is discussed below.

<br>
<br>

## Concept

For a specific token classification dependent problem, an artificial intelligence engineer can
<ul>
  <li>Develop a token classification model per language model architecture, e.g., <a href="https://arxiv.org/abs/1907.11692">RoBERTa (Robustly Optimized BERT Pretraining Approach)</a>, <a href="https://arxiv.org/abs/2003.10555">ELECTRA (Efficiently Learning an Encoder that Classifies Token Replacements Accurately)</a>.  Per architecture, <a href="https://wires.onlinelibrary.wiley.com/doi/epdf/10.1002/widm.1484">hyperparameter optimisation/tuning techniques</a>, and <a href="https://docs.ray.io/en/latest/tune/index.html">libraries</a>, aid the development of quite effective models, subject to early stopping, etc., constraints.</li>
  <li>Select the best model amongst the set of models; a single model per architecture.</li>
</ul>

For this exercise, the best model was selected by comparing a testing phase metric, specifically Matthews Correlation Coefficient (MCC):

$$MCC = \frac{(tn \bullet tp) - (fn \bullet fp)}{{\Large{[}}(tp + fp)(tp + fn)(tn + fp)(tn + fn){\Large{]}}^{0.5}}$$

<br>

$$MCC \in [-1, \quad +1]$$


wherein $tn$, $tp$, $fn$, and $fp$ denote true negative, true positive, false negative, and false positive, respectively.  <b>Note</b>, the best model of a set must undergo (a) mathematical evaluation, and (b) business/cost evaluation.  The latter is critical because an acceptable mathematical metric, e.g., $precision > 0.9$ does not necessarily lead to excellent business/cost metrics.<br><br>

### Definitions

* false positive (fp): ... an incorrect model decision whereby the model's decision is true/present, instead of false/absent.  Example: the model indicates that there are inflammable items in a suitcase, but there aren't.
* false negative (fn): ... an incorrect model decision whereby the model's decision is false/absent, instead of true/present.  Example: A model indicates that there are no inflammable items in the suitcase, but there are.
* true positive (tp): ... a model correctly indicates the **presence of**, e.g., a disease.
* true negative (tn): ... a model correctly indicates the **absence of**, e.g., a disease.


<br>
<br>


## A Problem Statement

This section outlines a plausible (a) problem statement, (b) corresponding outcome expectations/underlying aims, and (c) deployment goal vis-à-vis token classification model development.

<br>

#### PROBLEM STATEMENT

An organisation manually classifies trauma incidents for all the major trauma centres of five countries.  Per trauma case, an injury coding expert <b>(a)</b> examines the case's free and structured text, and assigns each piece of text to a category, and <b>(b)</b> assigns the case to a trauma category based on the combination text pieces & categories detected; text pieces of the other/miscellaneous category are excluded from this exercise.  Trauma injury coding is an extremely intensive and time-consuming exercise, and injury coding error rates - per annum - can be quite high.  Hence, and as a first step, we are in search of a solution that automatically classifies text pieces vis-à-vis a set of provided categories.

<br>

#### OUTCOME EXPECTATIONS, UNDERLYING AIMS

* <b>Outcome Expectations:</b> Real-time availability of classifications per trauma case.
* <b>Underlying Aim:</b> The automatic classification of trauma case text pieces; objective &#8594;
  * per case, automatic classification time < 180 seconds.
  * model metrics limits false negative rate &#8804; 0.02, false positive rate &#8804; 0.04

<br>

#### DEPLOYMENT GOAL

A potential machine learning dependent project without a deployment goal is directionless, do not proceed.  A plausible deployment goal is<br><br><br><br><img src='/assets/images/deployment-goal.png' alt='input' width='596px'/>



<br>
<br>

<br>
<br>

<br>
<br>

<br>
<br>
