
# References

## Natural Language Processing

* [A Survey of Transformer-based Pretrained Models in Natural Language Processing](https://arxiv.org/abs/2108.05542)
* [A review of pretrained language models: from BERT, RoBERTa, to ELECTRA, DeBERTa, BigBird, and more](https://tungmphung.com/a-review-of-pre-trained-language-models-from-bert-roberta-to-electra-deberta-bigbird-and-more/)
* [Graph Transformers: A Survey](https://arxiv.org/abs/2407.09777)
* [A Broad-Coverage Challenge Corpus for Sentence Understanding through Inference](https://arxiv.org/abs/1704.05426)
* [Word Pieces: Google's Neural Machine Translation System: Bridging the Gap between Human and Machine Translation](https://arxiv.org/abs/1609.08144)

<br>

## Mathematics

### Fundamentals

* [Minimisation Algorithms](https://era.ed.ac.uk/handle/1842/4109)
* [A simple illustration of likelihood functions in relation to based transformer models](https://etc.cuit.columbia.edu/news/basics-language-modeling-transformers-gpt)
* [Pattern Recognition & Machine Learning](https://www.microsoft.com/en-us/research/uploads/prod/2006/01/Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf)
* [Deep Learning](https://www.bishopbook.com)

<br>

### Transformers
* [A catalogue of transformer models](https://arxiv.org/html/2302.07730v4)
* [Transformers: Attention is all you need](https://arxiv.org/abs/1706.03762): Re-visit this paper for a basic reminder of the underlying mathematics of [BERT (Bidirectional Encoder Representations from Transformers)](https://arxiv.org/abs/1810.04805)
  * [Annotated @ 2022](https://nlp.seas.harvard.edu/annotated-transformer/)
  * [Annotated @ 2018](https://nlp.seas.harvard.edu/2018/04/03/attention.html)
* [XLNet: Generalized Autoregressive Pretraining for Language Understanding](https://arxiv.org/abs/1906.08237)
* [DeBERTaV3: Improving DeBERTa using ELECTRA-Style Pre-Training with Gradient-Disentangled Embedding Sharing](https://arxiv.org/abs/2111.09543)
* [ELECTRA](https://research.google/blog/more-efficient-nlp-model-pre-training-with-electra/)
* [Large Language Models: A Survey](https://arxiv.org/pdf/2402.06196v1)
* [New LLM Pre-training and Post-training Paradigms](https://magazine.sebastianraschka.com/p/new-llm-pre-training-and-post-training)
* [A survey on recent advances in Named Entity Recognition](https://arxiv.org/html/2401.10825v1)
* [END-TO-END NAMED ENTITY RECOGNITION AND RELATION EXTRACTION USING PRE-TRAINED LANGUAGE MODELS](https://arxiv.org/pdf/1912.13415)
* [Knowledge graph extension with a pre-trained language model via unified learning method](https://dl.acm.org/doi/10.1016/j.knosys.2022.110245)
* [Graph Transformer Networks](https://arxiv.org/abs/1911.06455)
* [DistilBertForTokenClassification](https://huggingface.co/docs/transformers/model_doc/distilbert#transformers.DistilBertForTokenClassification)

<br>

### Research
* [A one-year-long research workshop on large multilingual models and datasets](https://bigscience.huggingface.co)
  * [Estimating the Carbon Footprint of BLOOM, a 176B Parameter Language Model](https://arxiv.org/abs/2211.02001)
* [Investigate Clay](https://madewithclay.org/#introduction)
  * [The State of AI in EO](https://www.linkedin.com/pulse/state-ai-eo-bruno-sanchez-andrade-nuño-kogxf)
  * [National Agriculture Imagery Program (NAIP) data embedded with Clay v1.5 (rev2)](https://source.coop/clay/clay-v1-5-naip-2)
  * [National Agriculture Imagery Program](https://naip-usdaonline.hub.arcgis.com)
  * [National Agriculture Imagery Program](https://en.wikipedia.org/wiki/National_Agriculture_Imagery_Program)
  * [Bruno Sanchez-Andrade Nuño](https://www.linkedin.com/in/nasonurb/)

<br>

### Optimisation

* [2.2 Transformer Model $\odot$ Position Information in Transformers: An Overview](https://direct.mit.edu/coli/article/48/3/733/111478/Position-Information-in-Transformers-An-Overview): Study this paper for an understanding of an *unknown* transformer model function.
* [ADAM: Dive into Deep Learning](https://d2l.ai/chapter_optimization/adam.html)
* [ADAM: PyTorch](https://pytorch.org/docs/stable/generated/torch.optim.Adam.html#torch.optim.Adam)
* [ADAM: A METHOD FOR STOCHASTIC OPTIMIZATION](https://arxiv.org/abs/1412.6980)
* [KLDivLoss](https://pytorch.org/docs/stable/generated/torch.nn.KLDivLoss.html#torch.nn.KLDivLoss)
* [Hyperparameter optimization: Foundations, algorithms,best practices, and open challenges](https://wires.onlinelibrary.wiley.com/doi/epdf/10.1002/widm.1484)
* [Hyperparameters in Deep Learning: A Comprehensive Review](https://ijisae.org/index.php/IJISAE/article/view/6967/5881)
* [Why Do We Need Weight Decay in Modern Deep Learning?](https://arxiv.org/pdf/2310.04415)
* [Hyperparameter Optimization For LLMs: Advanced Strategies](https://neptune.ai/blog/hyperparameter-optimization-for-llms)
* [Population Based Training of Neural Networks](https://arxiv.org/abs/1711.09846)
* [Hyperparameter Search with the Huggingface Trainer](https://blog.franglen.io/posts/2025/03/08/hyperparameter-search.html)

<br>

### Miscellaneous

* [Freedom of information (FOI) Improvement Plan 2024](https://www.gov.scot/publications/freedom-of-information-foi-improvement-plan-2024/)
* [Text Classification Notebook](https://github.com/huggingface/notebooks/blob/main/examples/text_classification.ipynb)
* [Using Huggingface Transformers with Tune, <abbr title="Population Based Training">PBT</abbr>](https://docs.ray.io/en/latest/tune/examples/pbt_transformers.html)
* [Fine-tune a Hugging Face Transformers Model](https://docs.ray.io/en/latest/train/examples/transformers/huggingface_text_classification.html)
* [Tune Trial Schedulers (tune.schedulers)](https://docs.ray.io/en/latest/tune/api/schedulers.html)
* [Tune Search Algorithms (tune.search)](https://docs.ray.io/en/latest/tune/api/suggestion.html)
* [.hyperparameter_search(compute_objective=...)](https://www.sbert.net/examples/training/hpo/README.html#compute-objective)
  * And much more.
  * [class](https://huggingface.co/docs/transformers/main_classes/trainer#transformers.Trainer.hyperparameter_search)
  * [cf.](https://discuss.huggingface.co/t/using-hyperparameter-search-in-trainer/785/10)
* [Analyzing Tune Experiment Results](https://docs.ray.io/en/latest/tune/examples/tune_analyze_results.html)
* [Get Started with Distributed Training using Hugging Face Transformers](https://docs.ray.io/en/latest/train/getting-started-transformers.html)
* [Visualizing Population Based Training (PBT) Hyperparameter Optimization](https://docs.ray.io/en/latest/tune/examples/pbt_visualization/pbt_visualization.html)
* [Displaying Mathematics Formulae](https://en.wikipedia.org/wiki/Help:Displaying_a_formula)

<br>

## Interfaces

### GRADIO

* [button](https://www.gradio.app/docs/gradio/button)
* [space embedding](https://huggingface.co/docs/hub/spaces-embed)
* [gradio spaces](https://huggingface.co/docs/hub/spaces-sdks-gradio)
* [entity recognition interface](https://www.gradio.app/guides/named-entity-recognition)

<br>
<br>

<br>
<br>

<br>
<br>

<br>
<br>
