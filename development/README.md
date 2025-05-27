<br>

# Notes

<br>

* [Data](#data)
  * [Sources](#sources)
  * [Annotating](#annotating)
  * [Extracting text from documents](#extracting-text-from-documents)
* [Model Development](#model-development)
  * [Hyperparameters](#hyperparameters)
  * [TensorBoard](#tensorboard)
  * [Computation Metrics](#computation-metrics-ray-prometheus-grafana)
  * [File formats of developed models](#file-formats-of-developed-models)
  * [Steps & Epochs](#steps--epochs)
  * [Classes of interest](#classes-of-interest)
* [References](#references)
  * [Natural Language Processing](#natural-language-processing)
  * [Mathematics](#mathematics)
  * [Interfaces](#interfaces)

<br>

## Data

### Sources

[W-NUT 2017 (W-NUT 2017 Emerging and Rare entity recognition)](https://paperswithcode.com/dataset/wnut-2017-emerging-and-rare-entity)[^w-nut]
* [Token Classification & W-NUT 2017](https://huggingface.co/docs/transformers/tasks/token_classification)
* [get W-NUT 2017](https://huggingface.co/datasets/leondz/wnut_17)

[Few-NERD](https://paperswithcode.com/dataset/few-nerd)[^nerd]
* [get Few-NERD](https://huggingface.co/datasets/DFKI-SLT/few-nerd?library=datasets)


<br>

### Annotating

For example, word level annotation scheme: <abbr title="Inside, Outside, Beginning">IOB</abbr> Tagging.

* [Annotation Tools](https://www.labellerr.com/blog/7-best-text-annotation-labeling-tools-in-2024/)
* [Doccano](https://microsoft.github.io/nlp-recipes/examples/annotation/Doccano.html)
  * [More](https://doccano.github.io/doccano/)
  * [doccano](https://github.com/doccano/doccano)
* [NER (Named Entity Recognition) Annotator](https://github.com/tecoholic/ner-annotator)
* [Acharya for NER (Named Entity Recognition)](https://acharya.astutic.com/docs/intro)
* [gradio & NER (Named Entity Recognition)](https://www.gradio.app/guides/named-entity-recognition)
* [tagtog](https://docs.tagtog.com)

<br>

### Extracting text from documents

* [pypdf](https://pypdf.readthedocs.io/en/stable/user/extract-text.html), [pip](https://pypi.org/project/pypdf/)
  * [example](https://www.geeksforgeeks.org/extract-text-from-pdf-file-using-python/)
* [PyMuPDF](https://pymupdf.readthedocs.io/en/latest/), [pip](https://pypi.org/project/PyMuPDF/)
  * [example](https://www.geeksforgeeks.org/extract-text-from-pdf-file-using-python/)


<br>
<br>

## Model Development

### Hyperparameters

Note [RunConfig](https://docs.ray.io/en/latest/train/api/doc/ray.train.RunConfig.html), [CheckpointConfig](https://docs.ray.io/en/latest/train/api/doc/ray.train.CheckpointConfig.html), [TuneConfig](https://docs.ray.io/en/latest/tune/api/doc/ray.tune.TuneConfig.html), [ScalingConfig](https://docs.ray.io/en/latest/train/api/doc/ray.train.ScalingConfig.html) $\in$ [ray.tune.run](https://docs.ray.io/en/latest/tune/api/doc/ray.tune.run.html).

* Default Search Algorithm: [BasicVariantGenerator](https://docs.ray.io/en/latest/tune/api/suggestion.html#random-search-and-grid-search-tune-search-basic-variant-basicvariantgenerator)
* Default Scheduler: [FIFOScheduler](https://docs.ray.io/en/latest/tune/api/schedulers.html#fifoscheduler-default-scheduler)
* [trainer_utils](https://github.com/huggingface/transformers/blob/main/src/transformers/trainer_utils.py)
* [default_compute_objective](https://github.com/huggingface/transformers/blob/main/src/transformers/trainer_utils.py#L267)
* [BestRun](https://github.com/huggingface/transformers/blob/main/src/transformers/trainer_utils.py#L245)
* [An example of next steps](https://christianjmills.com/posts/transformers-book-notes/chapter-8/index.html)
* huggingface.co [hyperparameter_search(...)](https://huggingface.co/docs/transformers/hpo_train)

<br>

### TensorBoard

The progress of a model training exercise is observable via TensorBoard

```shell
tensorboard --logdir 
    /tmp/ray/session_{datetime}_{host.code}/artifacts/{datetime}/tuning/driver_artifacts 
        --bind_all
```

Subsequently, a link of the form `http://...:6007/` or `http://...:6006/` is printed.  Access the underlying pages via a browser.  It might be necessary to switch to `http://localhost:6007/` or `http://localhost:6006/`. [^hyper]


<br>

### Computation Metrics: Ray, Prometheus, Grafana

Via [Ray Dashboard](https://docs.ray.io/en/latest/ray-observability/getting-started.html), aided by Prometheus & Grafana[^tracking]; the set-up for the latter pair is upcoming.  Ensure [usage statistics sharing/collection is disabled](https://docs.ray.io/en/latest/cluster/usage-stats.html).  Options

* os.environ['RAY_USAGE_STATS_ENABLED']='0'
* Either
  * ray start --disable-usage-stats --head --dashboard-host=0.0.0.0 --dashboard-port=8265
  * ray start --disable-usage-stats --head --dashboard-host=172.17.0.2 --dashboard-port=8265
  * etc.

The computation metrics will be accessible via
* localhost:8265
* localhost:6379

<br>

### File formats of developed models

* GGUF: GPT-Generated Unified Format[^gpt]
* GGML: GPT-Generated Model Language
* [What is GGUF and GGML?](https://medium.com/@phillipgimmi/what-is-gguf-and-ggml-e364834d241c)
* [About GGUF](https://github.com/ggerganov/ggml/blob/master/docs/gguf.md)
* [to GGUF](https://medium.com/@qdrddr/the-easiest-way-to-convert-a-model-to-gguf-and-quantize-91016e97c987)
* [to GGUF discussion](https://github.com/ggerganov/llama.cpp/discussions/2948)
* [Hugging Face & GGUF](https://huggingface.co/docs/hub/gguf)

<br>

### Steps & Epochs

The formulae in focus are

> * max_steps_per_epoch = self.__source['train'].shape[0] // (variable.TRAIN_BATCH_SIZE * variable.N_GPU)
> * max_steps = max_steps_per_epoch * self.__n_epochs

<br>

### Classes of interest

* [transformers](https://huggingface.co/docs/transformers/index)
* [transformers.PreTrainedTokenizer](https://huggingface.co/docs/transformers/v4.41.3/en/main_classes/tokenizer#transformers.PreTrainedTokenizer.__call__)
* [serving](https://medium.com/@anthonyproctor/how-to-use-ollama-an-introduction-to-efficient-ai-model-serving-43870d5ae62c)
* [pytorch DataLoader](https://pytorch.org/docs/stable/data.html#torch.utils.data.DataLoader)
* [pytorch Dataset](https://pytorch.org/docs/stable/data.html#torch.utils.data.Dataset)
* [TokenClassifierOutput](https://huggingface.co/docs/transformers/main_classes/output#transformers.modeling_outputs.TokenClassifierOutput)
* [DatasetInfo, Dataset, etc](https://huggingface.co/docs/datasets/v2.20.0/en/package_reference/main_classes#main-classes)
* [Tensors](https://pytorch.org/docs/stable/tensors.html)
* For tensors that have a single value: [torch.Tensor.item()](https://pytorch.org/docs/stable/generated/torch.Tensor.item.html#torch.Tensor.item)
* Optimisation: [torch.optim](https://pytorch.org/docs/stable/optim.html#module-torch.optim)
* [PretrainedConfig](https://huggingface.co/docs/transformers/v4.44.2/en/main_classes/configuration#transformers.PretrainedConfig)

<br>
<br>

## References

### Natural Language Processing

* [A Survey of Transformer-based Pretrained Models in Natural Language Processing](https://arxiv.org/abs/2108.05542)
* [A review of pretrained language models: from BERT, RoBERTa, to ELECTRA, DeBERTa, BigBird, and more](https://tungmphung.com/a-review-of-pre-trained-language-models-from-bert-roberta-to-electra-deberta-bigbird-and-more/)
* [Graph Transformers: A Survey](https://arxiv.org/abs/2407.09777)
* [A Broad-Coverage Challenge Corpus for Sentence Understanding through Inference](https://arxiv.org/abs/1704.05426)
* [Word Pieces: Google's Neural Machine Translation System: Bridging the Gap between Human and Machine Translation](https://arxiv.org/abs/1609.08144)

<br>

### Mathematics

#### Fundamentals

* [Minimisation Algorithms](https://era.ed.ac.uk/handle/1842/4109)
* [A simple illustration of likelihood functions in relation to based transformer models](https://etc.cuit.columbia.edu/news/basics-language-modeling-transformers-gpt)
* [Pattern Recognition & Machine Learning](https://www.microsoft.com/en-us/research/uploads/prod/2006/01/Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf)
* [Deep Learning](https://www.bishopbook.com)

<br>

#### Transformers
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

#### Research
* [A one-year-long research workshop on large multilingual models and datasets](https://bigscience.huggingface.co)
  * [Estimating the Carbon Footprint of BLOOM, a 176B Parameter Language Model](https://arxiv.org/abs/2211.02001)
* [Investigate Clay](https://madewithclay.org/#introduction)
  * [The State of AI in EO](https://www.linkedin.com/pulse/state-ai-eo-bruno-sanchez-andrade-nuño-kogxf)
  * [National Agriculture Imagery Program (NAIP) data embedded with Clay v1.5 (rev2)](https://source.coop/clay/clay-v1-5-naip-2)
  * [National Agriculture Imagery Program](https://naip-usdaonline.hub.arcgis.com)
  * [National Agriculture Imagery Program](https://en.wikipedia.org/wiki/National_Agriculture_Imagery_Program)
  * [Bruno Sanchez-Andrade Nuño](https://www.linkedin.com/in/nasonurb/)



<br>

#### Optimisation

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


<br>

#### Miscellaneous

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

### Interfaces

#### GRADIO

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


[^w-nut]: W-NUT: [Workshop on Noisy User-generated Text](https://noisy-text.github.io)
[^nerd]: A [Few-shot NERD (Named Entity Recognition Dataset)](https://aclanthology.org/2021.acl-long.248/)
[^gpt]: GPT: Generative Pre-trained Transformer
[^hyper]: Using `CheckpointConfig.num_to_keep <= 2` with <abbr title="Population Based Training">PBT</abbr> can lead to restoration problems when checkpoints are deleted too early, too early for other trials to exploit them. If this happens, increase the value of `num_to_keep`.
[^tracking]: [Ray, Grafana, Prometheus](https://docs.ray.io/en/latest/cluster/configure-manage-dashboard.html#observability-visualization-setup)
