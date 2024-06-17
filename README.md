# 🐦 Magpie

This is the official repository for "[Alignment Data Synthesis from Scratch by Prompting Aligned LLMs with Nothing](https://arxiv.org/abs/2406.08464)".

- 🤗 [**Huggingface (Models and Datasets)**](https://huggingface.co/Magpie-Align)
- 🕸️ [**Website**](https://magpie-align.github.io/)
- 📄 [**Technical Report**](https://arxiv.org/abs/2406.08464)

You can try the no-code Magpie demo [🤗 here](https://huggingface.co/spaces/davanstrien/magpie) to generate instruction-response pairs. Thanks a lot for the quick implementation from @davanstrien!

[![arXiv](https://img.shields.io/badge/arXiv-paper-b31b1b.svg)](https://arxiv.org/abs/2406.08464) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Currently, Magpie has been fully tested on the Llama-3 series. Testing is ongoing for model families including Llama-2, Mistral, Qwen, and more. Feel free to submit a pull request to ```configs/model_configs.json``` with more model support.

We hope Magpie can contribute to the democratization of AI. With your help, we can provide more data and enhance the transparency of model alignment processes!

## Abstract

High-quality instruction data is critical for aligning large language models (LLMs). Although some models, such as Llama-3-Instruct, have open weights, their alignment data remain private, which hinders the democratization of AI. High human labor costs and a limited, predefined scope for prompting prevent existing open-source data creation methods from scaling effectively, potentially limiting the diversity and quality of public alignment datasets. Is it possible to synthesize high-quality instruction data at scale by extracting it directly from an aligned LLM? We present a self-synthesis method for generating large-scale alignment data named Magpie. Our key observation is that aligned LLMs like Llama-3-Instruct can generate a user query when we input only the left-side templates up to the position reserved for user messages, thanks to their auto-regressive nature. We use this method to prompt Llama-3-Instruct and generate 4 million instructions along with their corresponding responses. We perform a comprehensive analysis of the extracted data and select 300K high-quality instances. To compare Magpie data with other public instruction datasets, we fine-tune Llama-3-8B-Base with each dataset and evaluate the performance of the fine-tuned models. Our results indicate that in some tasks, models fine-tuned with Magpie perform comparably to the official Llama-3-8B-Instruct, despite the latter being enhanced with 10 million data points through supervised fine-tuning (SFT) and subsequent feedback learning. We also show that using Magpie solely for SFT can surpass the performance of previous public datasets utilized for both SFT and preference optimization, such as direct preference optimization with UltraFeedback. This advantage is evident on alignment benchmarks such as AlpacaEval, ArenaHard, and WildBench.

## Overview

![Overview](figs/overview.png)

## Installation

**Build environment**
```
git clone https://github.com/magpie-align/magpie.git
cd magpie
conda create -n magpie python=3.10
conda activate magpie
pip install -r requirements.txt
```

**Get access to Llama-3 models from 🤗 Huggingface**

You can apply for Llama-3 model access [here](https://huggingface.co/meta-llama/Meta-Llama-3-8B-Instruct). To login in the terminal, enter:
```
huggingface-cli login
```
then enter your Huggingface private key beginning with "hf_".

## Toy Example

**Play with Jupyter Notebook**

The toy example can be found in [```demo.ipynb```](demo.ipynb). Have fun! 

<a target="_blank" href="https://colab.research.google.com/github/magpie-align/magpie/blob/main/demo.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

## Batched Data Generation

To run batched generation, you can simply run:
```
cd scripts
bash magpie.sh
```
The script will generate both instructions and responses in ```data``` folder. The script has been tested on an RTX 4090 24G GPU. If you are using GPUs with less memory, consider implementing [quantization](https://docs.vllm.ai/en/latest/quantization/fp8.html).

## Dataset Tagging
Available soon!

## Dataset Sanitization
Available soon!

## Citation

If you find the model, data, or code useful, please cite our paper:
```
@misc{xu2024magpie,
    title={Magpie: Alignment Data Synthesis from Scratch by Prompting Aligned LLMs with Nothing}, 
    author={Zhangchen Xu and Fengqing Jiang and Luyao Niu and Yuntian Deng and Radha Poovendran and Yejin Choi and Bill Yuchen Lin},
    year={2024},
    eprint={2406.08464},
    archivePrefix={arXiv},
    primaryClass={cs.CL}
}
```
