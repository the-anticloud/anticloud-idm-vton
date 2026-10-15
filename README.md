# IDM_VTON

> Anticloud offline package — upstream: yisol/IDM-VTON @ `main`.

## What This Project Does

[ECCV2024] IDM-VTON : Improving Diffusion Models for Authentic Virtual Try-on in the Wild

## Upstream README

<div align="center">
<h1>IDM-VTON: Improving Diffusion Models for Authentic Virtual Try-on in the Wild</h1>

<a href='https://idm-vton.github.io'><img src='https://img.shields.io/badge/Project-Page-green'></a>
<a href='https://arxiv.org/abs/2403.05139'><img src='https://img.shields.io/badge/Paper-Arxiv-red'></a>
<a href='https://huggingface.co/spaces/yisol/IDM-VTON'><img src='https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Demo-yellow'></a>
<a href='https://huggingface.co/yisol/IDM-VTON'><img src='https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Model-blue'></a>


</div>

This is the official implementation of the paper ["Improving Diffusion Models for Authentic Virtual Try-on in the Wild"](https://arxiv.org/abs/2403.05139).

Star ⭐ us if you like it!

---


![teaser2](assets/teaser2.png)&nbsp;
![teaser](assets/teaser.png)&nbsp;



## Requirements

```
git clone https://github.com/yisol/IDM-VTON.git
cd IDM-VTON

conda env create -f environment.yaml
conda activate idm
```

## Data preparation

### VITON-HD
You can download VITON-HD dataset from [VITON-HD](https://github.com/shadow2496/VITON-HD).

After download VITON-HD dataset, move vitonhd_test_tagged.json into the test folder, and move vitonhd_train_tagged.json into the train folder.

Structure of the Dataset directory should be as follows.

```

train
|-- image
|-- image-densepose
|-- agnostic-mask
|-- cloth
|-- vitonhd_train_tagged.json

test
|-- image
|-- image-densepose
|-- agnostic-mask
|-- cloth
|-- vitonhd_test_tagged.json

```

### DressCode
You can download DressCode dataset from [DressCode](https://github.com/aimagelab/dress-code).

We provide pre-computed densepose images and captions for garments [here](https://kaistackr-my.sharepoint.com/:u:/g/personal/cpis7_kaist_ac_kr/EaIPRG-aiRRIopz9i002FOwBDa-0-BHUKVZ7Ia5yAVVG3A?e=YxkAip).

We used [detectron2](https://github.com/facebookresearch/detectron2) for obtaining densepose images, refer [here](https://github.com/sangyun884/HR-VITON/issues/45) for more details.

After download the DressCode dataset, place image-densepose directories and caption text files as follows.

```
DressCode
|-- dresses
    |-- images
    |-- image-densepose
    |-- dc_caption.txt
    |-- ...
|-- lower_body
    |-- images
    |-- image-densepose
    |-- dc_caption.txt
    |-- ...
|-- upper_body
    |-- images
    |-- image-densepose
    |-- dc_caption.txt
    |-- ...
```


## Training


### Preparation

Download pre-trained ip-adapter for sdxl(IP-Adapter/sdxl_models/ip-adapter-plus_sdxl_vit-h.bin) and image encoder(IP-Adapter/models/image_encoder) [here](https://github.com/tencent-ailab/IP-Adapter).

```
git clone https://huggingface.co/h94/IP-Adapter
```

Move ip-adapter to ckpt/ip_adapter, and image encoder to ckpt/image_encoder.

Start training using python file with arguments,

```
accelerate launch train_xl.py \
    --gradient_checkpointing --use_8bit_adam \
    --output_dir=result --train_batch_size=6 \
    --data_dir=DATA_DIR
```

or, 

## License

Upstream terms preserved in `THIRD_PARTY_LICENSES/`. Overlay licensed under Anticommons 0.1.0.

## Verification

Recompute the SHA3-256 of `BENCH.json` and compare to this package’s register. Any drift = invalid package.
