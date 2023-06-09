# Stable diffusion with Nvidia

<!-- TOC -->

* [Stable diffusion with Nvidia](#stable-diffusion-with-nvidia)
    * [Usage](#usage)
        * [Prerequisites](#prerequisites)
        * [Installation](#installation)
        * [⭐ Web UI with AUTOMATIC1111](#-web-ui-with-automatic1111)
        * [Adding Checkpoints/Embeddings/LoRA](#adding-checkpointsembeddingslora)

<!-- TOC -->

## Usage

For a detailed description of how to get this working in Windows using WSL2 and native Docker (not Docker Desktop), see
**[this blog post](https://trycatch.dev/2022/10/01/stable-diffusion-on-wsl2-with-docker/)**.

### Prerequisites

- Windows 10/11 with [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install) or native Linux
- Lots of free disk space (200+ GB recommended if experimenting)
- [Docker CE](https://docs.docker.com/engine/install/) installed
- Git installed in WSL2/Linux
- The file [`sd-v1-4.ckpt`](https://huggingface.co/CompVis/stable-diffusion-v-1-4-original)
  and/or [`v1-5-pruned-emaonly.ckpt`](https://huggingface.co/runwayml/stable-diffusion-v1-5) from Hugging Face (free
  registration required)
    - Alternatively, after registering for a Hugging Face account, you can generate a
      new [token](https://huggingface.co/settings/tokens) for automatic downloading

#### Prerequisites for usage with an Nvidia GPU

- A modern Nvidia GPU
- [Nvidia Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker)
  installed

### Installation

1. Clone this repository, and then `cd` into it:

```bash
git clone https://github.com/edwin-luijten/stable-diffusion-with-nvidia.git
cd stable-diffusion-with-nvidia
```

2. If *not* using a Hugging Face token, place the `sd-v1-4.ckpt` and/or `v1-5-pruned-emaonly.ckpt` file you downloaded
   earlier into `./storage/res/checkpoints`
3. If you do have a Hugging Face token, rename `env.dist` to `.env` and edit the `.env` file:
    - Uncomment the `#HUGGINGFACE_TOKEN=` line by removing the `#` in front
    - Insert your Hugging Face token after the equals sign, like so: `HUGGINGFACE_TOKEN=hf_asdfasdfasdfasdfasdf`
4. Run `./verify-resources.sh -d` to verify and download any missing models or weights
    - If you encounter any issues, please make sure they are resolved before continuing to the next step

All the resources (models and weights) are in `storage/res/` and all the output files generated by Stable Diffusion are
in `storage/out/`.

### ⭐ [Web UI with AUTOMATIC1111](https://github.com/AUTOMATIC1111/stable-diffusion-webui/)

- includes [Txt2Vectorgraphics](https://github.com/GeorgLegato/Txt2Vectorgraphics) script
  , [Deforum](https://github.com/deforum-art/deforum-for-automatic1111-webui)
  and [StylePy](https://github.com/some9000/StylePile) extension!
- fine-tuned VAE is enabled

Launch:

```bash
First time usage: 
docker compose up resources
--
docker compose up sd-cpu
docker compose up sd-gpu
```

Visit: http://0.0.0.0:7860 to access the web UI.

### Adding Checkpoints/Embeddings/LoRA

Go to https://civitai.com/ and download a checkpoint you like, for
example: https://civitai.com/models/15303/rmada-merge-sd-21-768.  
Once downloaded place it in: storage/checkpoints.

Checkpoints: storage/checkpoints  
Embeddings: storage/embeddings  
LoRA: storage/lora

Restart your container to make the new files available in the model selector.