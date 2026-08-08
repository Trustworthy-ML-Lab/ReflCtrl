# ReflCtrl: Controlling LLM Reflection Efficiently via Representation Engineering
This is the official repository for [ReflCtrl: Controlling LLM Reflection Efficiently via Representation Engineering](https://openreview.net/forum?id=ungnJ4O0AD), published at COLM 2026. (Spotlight presentation on NeurIPS 2025 MI workshop)
For more information, please check out the [project website](https://lilywenglab.github.io/ReflCtrl/).
## Overview
In this work, we study the self-reflection behavior of Large Reasoning Models (LRMs) from the perspective of representation engineering. We segment model’s reasoning into steps, identify the steps corresponding
to reflection, and extract a reflection direction in the latent space that governs this
behavior. Using this direction, we propose a stepwise steering method that can
control reflection frequency. 
![](overview.png)
## Preparation
To start, install all dependency by 
```
pip install -r requirements.txt
```
## Extract reflection direction
Before steering, extract reflection direction by running
```
bash run_collect_and_extract.sh
```
## Steering
For running steering experiments, we first host our model via vllm. For example:
```
python launch_server.py --gpus 2 --model deepseek-r1-qwen-1.5b  --router_port 8088 --step_begin_only --intervention_layers 6-22 --max_model_len 16384
```
When server is ready, run `query_llm.py` for evaluation:
```
python query_llm.py --dataset gsm8k --max_length 8192 --instruction " Please reason step by step, and put your final answer within \boxed{}."  --mode api --model deepseek-r1-qwen-1.5b --n_samples 4  --step_begin_only --with_intervention -0.48 --intervention_layers 6-22

```
## Cite this work
ReflCtrl: Controlling LLM Reflection Efficiently via Representation Engineering, Ge Yan, Chung-En Sun, Linbo Liu, Tsui-Wei Weng, COLM 2026.
```
@inproceedings{
    yan2026reflctrl,
    title={ReflCtrl: Controlling {LLM} Reflection Efficiently via Representation Engineering},
    author={Ge Yan and Chung-En Sun and Linbo Liu and Tsui-Wei Weng},
    booktitle={Third Conference on Language Modeling},
    year={2026},
    url={https://openreview.net/forum?id=QSKP3uvMm9}
}
```
