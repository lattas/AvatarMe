# [AvatarMe: Realistically Renderable 3D Facial Reconstruction "in-the-wild"](https://arxiv.org/abs/2003.13845):
[![Youtube Video](https://img.shields.io/badge/HD%20Video-Results-lightgrey?logo=youtube)](https://www.youtube.com/watch?v=fEsgeZPN8Uw)
[![arXiv Prepring](https://img.shields.io/badge/arXiv-Preprint-lightgrey?logo=arxiv)](https://arxiv.org/pdf/2003.13845.pdf)
[![RealFaceDB](https://img.shields.io/badge/dataset-RealFaceDB-lightgrey)](https://github.com/lattas/avatarme#public-dataset)


Published in the IEEE/CVF Conference on Computer Vision and Pattern Recognition (__[CVPR 2020](https://openaccess.thecvf.com/content_CVPR_2020/html/Lattas_AvatarMe_Realistically_Renderable_3D_Facial_Reconstruction_In-the-Wild_CVPR_2020_paper.html)__)

# [AvatarMe++: Facial Shape and BRDF Inference with Photorealistic Rendering-Aware GANs](https://arxiv.org/abs/2112.05957):
[![arXiv Prepring](https://img.shields.io/badge/arXiv-Preprint-lightgrey?logo=arxiv)](https://arxiv.org/abs/2112.05957)

Published in IEEE Transaction on Pattern Analysis and Machine Intelligence (__[TPAMI 2021](https://ieeexplore.ieee.org/abstract/document/9606538)__)

[Alexandros Lattas](https://www.imperial.ac.uk/people/a.lattas),
[Stylianos Moschoglou](https://www.doc.ic.ac.uk/~sm3515/),
[Stylianos Ploumpis](https://www.imperial.ac.uk/people/s.ploumpis),
[Baris Gecer](http://barisgecer.github.io),<br>
[Abhijeet Ghosh](https://www.doc.ic.ac.uk/~ghosh/),
[Stefanos Zafeiriou](https://wp.doc.ic.ac.uk/szafeiri/)
<br/>
Imperial College London
<br/>

## Follow-up Works
If you are interested in this work, you may also be interested in our follow-up works:
- (CVPR 2023) FitMe: Deep Photorealistic 3D Morphable Model Avatars ([Project Page](https://lattas.github.io/fitme.html))
- (ICCV 2023) Relightify: Relightable 3D Faces from a Single Image via Diffusion Models ([Project Page](https://foivospar.github.io/Relightify/))

## Overview

![Intro Image](img/avatarme++_teaser.png "Teaser Image")

<br>

AvatarMe++ is a new method for reconstructing renderable photorealistic 3D faces from a single ‘in-the-wild”. 
Extending on AvatarMe we define a fast facial photorealistic differentiable rendering methodology 
with accurate facial skin diffuse and specular reflection, 
self-occlusion and subsurface scattering approximation. 
With this, we train a network that disentangles the facial diffuse and specular BRDF components 
from a shape and texture with baked illumination, reconstructed with a state-of-the-art 3DMM fitting method. 

<br>

## Method

![Method Image](img/avatarme++_method.png "Method Image")

<br>

Summary of the AvatarMe++ method: 
We acquire a 3DMM fitting and upscale its texture using a state-of-the-art super resolution network,
trained on synthetic data rendered in the texture’s domain. 
A image-translation network is then used to transform the upscaled texture and normals to
reflectance maps, namely the Diffuse Albedo, Specular Albedo, Diffuse Normals and Specular Normals.

<br>

![Training Image](img/avatarme++_training.png "Training Image")

We create a rendering module, 
with subsurface-scattering and self-occlusion approximation. 
During training, it is used to create synthetic data pairs, 
by rendering the captured data in the target’s environment and random ones, 
which are used for photorealistic rendering loss. 
The complete high resolution (up to 6k×4k) BRDF maps can be used for photorealistic rendering, 
while the specular normals can be used to enhance the original geometry with fine details.

<br>

## Results

![Results Image](img/avatarme++_results.png "Results Image")

<br>

Our high resolution mesh and reflectance textures 
(Diffuse Albedo, Specular Albedo, Diffuse Normals, Specular Normals)
can be used with most open-source or commercial renderers
to render the reconstructed subjects in various illumination environments.

<br>

![Generalization Image](img/avatarme++_generalization.png "Results Image")

Thanks to the photorealistic differentiable renderer and the stochastic rendering loss,
in contrast to AvatarMe, AvatarMe++ can be generalize for most examples with frontal facing illumination. 
As shown above, AvatarMe++ can be effectively used in reconstructions with
([Chen et al., 2019](https://openaccess.thecvf.com/content_ICCV_2019/papers/Chen_Photo-Realistic_Facial_Details_Synthesis_From_Single_Image_ICCV_2019_paper.pdf)),
([Gecer et al., 2021](https://openaccess.thecvf.com/content/CVPR2021/html/Gecer_OSTeC_One-Shot_Texture_Completion_CVPR_2021_paper.html))
and datasets such as 
[Facescape](https://facescape.nju.edu.cn/),
[Superface](https://www.micc.unifi.it/resources/datasets/florence-superface/)
and subjects captured with a [3dMD](https://3dmd.com/) device. 

<br>

## Code
This model has been commercialized and is not released publicly,
but we have released the rendering code used in AvatarMe++ as a Pytorch3D extension [Pytorch3D-Me](github.com/lattas/pytorch3d-me).
It includes the UV-space rendering, Blinn-Phong shader, subsurface scattering, and occlusion approximations.

## Public Dataset
*RealfaceDB* can now be obtained by accredited researchers
and used for training/testing methods similar to AvatarMe.

![Dataset Teaser](img/realfacedb_figure.png "Dataset")

The dataset contains patches of facial reflectance as described in the paper, 
namely the diffuse albedo, diffuse normals, specular albedo, specular normals,
as well as the shape in UV space. For the shape, 
reconstructed meshes have been registered to a common topology
and the `XYZ` values of the points have been mapped to the `RGB` in UV coordinates and interpolated to complete the UV map.
From the complete UV maps of `6144x4096` pixels, patches of `512x512` pixels have been sampled.
The dataset contains 7500 such patches (1500 of each datatype) that are anonymized, randomized
and sampled so that they do not contain identifiable features.

Our AvatarMe++ paper contains a section on photorealistically rendering such data, using [Pytorch3D](https://github.com/facebookresearch/pytorch3d). 
For any further questions, feel free to contact us.

To obtain access to the dataset,
you need to complete and sign a licence agreement,
which should be completed by a full-time academic staff member (not a student).
To obtain the licence agreement and the dataset please send an email to 
Alexandros Lattas (a.lattas@imperial.ac.uk)
and Stylianos Moschoglou (s.moschoglou@imperial.ac.uk).
Please contact us through your academic email
and include your name and position.
We will verify your request and contact you regarding how to download the dataset. Note that the agreement requires that:

- The data must be used for non-commercial research and education purposes only.
- You agree not to copy, sell, trade, or exploit the model for any commercial purposes.
- You must destroy the data after 2 years since the first download.
- If you will be publishing any work using this dataset, please cite the following paper.

## Citation
If you find this work useful in your research,
please cite our papers [AvatarMe](http://openaccess.thecvf.com/content_CVPR_2020/html/Lattas_AvatarMe_Realistically_Renderable_3D_Facial_Reconstruction_In-the-Wild_CVPR_2020_paper.html),
[AvatarMe++](https://ieeexplore.ieee.org/abstract/document/9606538/) using:
```
@InProceedings{lattas2020avatarme,
  author = {Lattas, Alexandros and Moschoglou, Stylianos and Gecer, Baris and Ploumpis, Stylianos and Triantafyllou, Vasileios and Ghosh, Abhijeet and Zafeiriou, Stefanos},
  title = {AvatarMe: Realistically Renderable 3D Facial Reconstruction "In-the-Wild"},
  booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
  month = {June},
  year = {2020}
}

@article{lattas2021avatarme++,
  title={AvatarMe++: Facial Shape and BRDF Inference with Photorealistic Rendering-Aware GANs},
  author={Lattas, Alexandros and Moschoglou, Stylianos and Ploumpis, Stylianos and Gecer, Baris and Ghosh, Abhijeet and Zafeiriou, Stefanos P},
  journal={IEEE Transactions on Pattern Analysis and Machine Intelligence},
  year={2021},
  publisher={IEEE}
}
```

## Contact
For any enquiries please contact the first author at the email listed on the above papers. 
