# Short biography

<a href="https://github.com/NathanMolinier">
   <img src="https://github.com/brainhack-school2024/molinier_project/assets/68945192/35bf52a6-ed2a-4c7f-944f-a040242f5154" width="100px;" alt=""/>
</a>

My name is Nathan Molinier, I'm a PhD student at Polytechnique Montreal, and I use deep learning methods to identify spinal structures on MRI scans.

# My brainhack project
## Context

Unlike other non-invasive medical imaging techniques such as computed tomography (CT scans), X-rays, or ultrasounds, Magnetic Resonance Imaging (MRI) employs various protocols resulting in significantly distinct images, also referred to as contrasts. While these contrasts are valuable in medical diagnosis for facilitating tissue identification and characterizing pathologies, they pose numerous challenges when it comes to the utilization of automated methods such as deep learning. Depending on the selected imaging parameters, there can be significant variations in intensity and noise distributions for the same region of interest, greatly impacting the capability and robustness of automated methods. Although significant efforts are currently being made to address this limitation by training models on a wider range of contrasts, many of single contrasts approaches remain underutilized due to a lack of compatibility between the training data and the data available for testing the models. To mitigate this issue, we propose converting any contrast into a simulated T2-weighted (T2w) image, which could be used to leverage the performance of deep learning models specifically trained on T2w contrasts. Given the complexity of accessing multi-contrast data, the aim of this initiative is to extend the scope of deep learning work regardless of the number of contrasts used for training.

### Examples

These deep learning models were only trained on T2-weighted scans

| Spine segmentation | Spinal cord segmentation |
|:---:|:---:|
| <img width="682" alt="Screenshot 2024-06-14 at 09 41 57" src="https://github.com/brainhack-school2024/molinier_project/assets/68945192/9f92316a-3c05-441b-9315-6c2517ab0bc2"> | <img width="637" alt="Screenshot 2024-06-14 at 09 42 22" src="https://github.com/brainhack-school2024/molinier_project/assets/68945192/0c4bfbef-8910-4881-baef-aeb1464d1a01"> |

## Contrast translation approach

My objective was to generate fake T2w scans from any given contrast to help deep learning models that were only trained on T2w scans during inference.

### Datasets

| Dataset name | Subjects | Contrasts used | Open source | Link |
| :---: | :---: | :---: | :---: | :---: |
| spine generic | 267 | T1w and T2w | yes | https://github.com/spine-generic/data-multi-subject |
| canproco | 450 | PSIR, STIR and T2w | No | X |
| lumbar-nusantara | 515 | T1w and T2w | yes | https://data.mendeley.com/datasets/k57fr854j2/2 |
| spider | 218 | T1w and T2w | yes | https://spider.grand-challenge.org/ |

### Preprocessing steps and method

<img width="930" alt="Screenshot 2024-06-14 at 09 53 12" src="https://github.com/brainhack-school2024/molinier_project/assets/68945192/a8c90f38-be21-435f-8f55-8bebaffb5395">

### Previous work on cervical FOV

For this work, the datasets `spine-generic` and `canproco` were used for the training of the cGAN approach.

<img width="1123" alt="Screenshot 2024-06-14 at 09 55 18" src="https://github.com/brainhack-school2024/molinier_project/assets/68945192/17379015-3f07-4542-96f6-d97a899f6ab4">

> spineps: https://github.com/Hendrik-code/spineps

### Extension of the method for lumbar FOV

For this work, the dataset `spider` was used for inference, the cGAN approach was only trained with the dataset `lumbar-nusantara`.

<img width="1123" alt="Screenshot 2024-06-14 at 13 52 30" src="https://github.com/brainhack-school2024/molinier_project/assets/68945192/40ff2c71-5454-4fcc-8f6f-82bca7b61e06">

> Surprisingly [spineps](https://github.com/Hendrik-code/spineps) performed well on the T1w lumbar scans of the `spider` dataset. One possible reason is that spineps was actually trained on the T2w scans of the same patients in this dataset.

### Evaluation of the lumbar spine segmentations

To evaluate the quality of the final segmentations with and without the use of the contrast translation approach, the framework [panoptica](https://github.com/BrainLesion/panoptica) was used.

> panoptica allows us to evaluate segmentations from both semantic and instance standpoint ([paper](https://arxiv.org/abs/2312.02608))

#### Global segmentation

Here, segmentations are binarized and metrics are computed on the full segmentations.

| Global Dice Score | Global average symmetric surface distance (ASSD)|
| :---: | :---: |
| <img width="645" alt="Screenshot 2024-06-14 at 14 12 28" src="https://github.com/brainhack-school2024/molinier_project/assets/68945192/0d523670-408b-48fd-9557-522369497605"> | <img width="779" alt="Screenshot 2024-06-14 at 14 14 17" src="https://github.com/brainhack-school2024/molinier_project/assets/68945192/6eb20996-362d-415b-acaf-dbb3aff115fe"> |
| <img width="850" alt="Screenshot 2024-06-14 at 14 12 28" src="https://github.com/brainhack-school2024/molinier_project/assets/68945192/dbd71b84-bda4-437c-9f2f-3c1a2b96c6cd"> | <img width="800" alt="Screenshot 2024-06-14 at 14 12 28" src="https://github.com/brainhack-school2024/molinier_project/assets/68945192/21c0327a-2b47-44b8-88e4-b8accb3835df"> |





