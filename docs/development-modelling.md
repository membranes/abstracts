# Model Development

## Hyperparameters

Note [RunConfig](https://docs.ray.io/en/latest/train/api/doc/ray.train.RunConfig.html), [CheckpointConfig](https://docs.ray.io/en/latest/train/api/doc/ray.train.CheckpointConfig.html), [TuneConfig](https://docs.ray.io/en/latest/tune/api/doc/ray.tune.TuneConfig.html), [ScalingConfig](https://docs.ray.io/en/latest/train/api/doc/ray.train.ScalingConfig.html) $\in$ [ray.tune.run](https://docs.ray.io/en/latest/tune/api/doc/ray.tune.run.html).

* Default Search Algorithm: [BasicVariantGenerator](https://docs.ray.io/en/latest/tune/api/suggestion.html#random-search-and-grid-search-tune-search-basic-variant-basicvariantgenerator)
* Default Scheduler: [FIFOScheduler](https://docs.ray.io/en/latest/tune/api/schedulers.html#fifoscheduler-default-scheduler)
* [trainer_utils](https://github.com/huggingface/transformers/blob/main/src/transformers/trainer_utils.py)
* [default_compute_objective](https://github.com/huggingface/transformers/blob/main/src/transformers/trainer_utils.py#L267)
* [BestRun](https://github.com/huggingface/transformers/blob/main/src/transformers/trainer_utils.py#L245)
* [An example of next steps](https://christianjmills.com/posts/transformers-book-notes/chapter-8/index.html)
* huggingface.co [hyperparameter_search(...)](https://huggingface.co/docs/transformers/hpo_train)

<br>

## TensorBoard

The progress of a model training exercise is observable via TensorBoard

```shell
tensorboard --logdir 
    /tmp/ray/session_{datetime}_{host.code}/artifacts/{datetime}/tuning/driver_artifacts 
        --bind_all
```

<br>

Subsequently, a link of the form `http://...:6007/` or `http://...:6006/` is printed.  Access the underlying pages via a browser.  It might be necessary to switch to `http://localhost:6007/` or `http://localhost:6006/`. [^hyper]


<br>

## Computation Metrics: Ray, Prometheus, Grafana

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

## File formats of developed models

* GGUF: GPT-Generated Unified Format[^gpt]
* GGML: GPT-Generated Model Language
* [What is GGUF and GGML?](https://medium.com/@phillipgimmi/what-is-gguf-and-ggml-e364834d241c)
* [About GGUF](https://github.com/ggerganov/ggml/blob/master/docs/gguf.md)
* [to GGUF](https://medium.com/@qdrddr/the-easiest-way-to-convert-a-model-to-gguf-and-quantize-91016e97c987)
* [to GGUF discussion](https://github.com/ggerganov/llama.cpp/discussions/2948)
* [Hugging Face & GGUF](https://huggingface.co/docs/hub/gguf)

<br>

## Steps & Epochs

The formulae in focus are

> * max_steps_per_epoch = self.__source['train'].shape[0] // (variable.TRAIN_BATCH_SIZE * variable.N_GPU)
> * max_steps = max_steps_per_epoch * self.__n_epochs

<br>

## Classes of interest

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

<br>
<br>

<br>
<br>

<br>
<br>

[^gpt]: GPT: Generative Pre-trained Transformer
[^hyper]: Using `CheckpointConfig.num_to_keep <= 2` with <abbr title="Population Based Training">PBT</abbr> can lead to restoration problems when checkpoints are deleted too early, too early for other trials to exploit them. If this happens, increase the value of `num_to_keep`.
[^tracking]: [Ray, Grafana, Prometheus](https://docs.ray.io/en/latest/cluster/configure-manage-dashboard.html#observability-visualization-setup)
