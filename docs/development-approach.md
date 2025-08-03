
# Approach

For a specific token classification dependent problem, an artificial intelligence engineer can
<ul>
  <li>Develop a token classification model per language model architecture, e.g., <a href="https://arxiv.org/abs/1907.11692">RoBERTa (Robustly Optimized BERT Pretraining Approach)</a>, <a href="https://arxiv.org/abs/2003.10555">ELECTRA (Efficiently Learning an Encoder that Classifies Token Replacements Accurately)</a>.  Per architecture, <a href="https://wires.onlinelibrary.wiley.com/doi/epdf/10.1002/widm.1484">hyperparameter optimisation/tuning techniques</a>, and <a href="https://docs.ray.io/en/latest/tune/index.html">libraries</a>, aid the development of quite effective models, subject to early stopping, etc., constraints.</li>
  <li>Select the best model amongst the set of models; a single model per architecture.</li>
</ul>

<br>

## Selecting the best model

For this exercise, the best model was selected by comparing a testing phase metric, specifically Matthews Correlation Coefficient (MCC):

$$MCC = \frac{(tn \bullet tp) - (fn \bullet fp)}{{\Large{[}}(tp + fp)(tp + fn)(tn + fp)(tn + fn){\Large{]}}^{0.5}}$$

$$MCC \in [-1, \quad +1]$$


wherein <abbr><i>tn</i></abbr>, <abbr><i>tp</i></abbr>, <abbr><i>fn</i></abbr>, and <abbr><i>fp</i></abbr> denote true negative, true positive, false negative, and false positive, respectively.

<br>

## Warning

<b>Note</b>, the best model of a set must undergo (a) mathematical evaluation, and (b) business/cost evaluation.  The latter is critical because an acceptable mathematical metric, e.g., $precision > 0.9$ does not necessarily lead to excellent business/cost metrics.

<br>
<br>

<br>
<br>

<br>
<br>

<br>
<br>
