# StyleGAN2: projecting images

The goal of this [Google Colab](https://colab.research.google.com/) notebook is to project images to latent space with StyleGAN2.

## Usage

-   Run [`stylegan2_projecting_images.ipynb`][stylegan2_projecting_images].

## Data

Data consists of:
-   1 picture of the French president Emmanuel Macron, found on [Nice Matin][french-president] ([archive][french-president-archive]),
-   37 individual pictures of the French government, found on [Wikipedia][french-government] ([list][french-government-archive]),
-   3 pictures of famous paintings, found on Wikipedia ([list][famous-paintings-archive]):
    - [La Joconde](https://fr.wikipedia.org/wiki/La_Joconde), 
    - [Le Condottière](https://fr.wikipedia.org/wiki/Le_Condotti%C3%A8re_(Antonello_de_Messine)),
    - [La Jeune Fille à la perle](https://fr.wikipedia.org/wiki/La_Jeune_Fille_%C3%A0_la_perle).

<img alt="Original image of the French president" src="https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/img/emmanuel-macron.jpg" width="250">

## Pre-processing

There are two possible pre-processing methods:
-   either center-cropping (to 1024x1024 resolution) as sole pre-processing,

<img alt="Center-cropping" src="https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/img/emmanuel-macron-crop.jpg" width="250">

-   or the same pre-processing as for the [FFHQ dataset]:
    1. first, an alignment based on 68 face landmarks returned by [dlib],
    2. then reproduce `recreate_aligned_images()`, as detailed in [FFHQ pre-processing code].

<img alt="FFHQ pre-processing" src="https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/img/emmanuel-macron-aligned.png" width="250">

Finally, the pre-processed image can be projected to the latent space of the StyleGAN2 model trained with configuration f on the Flickr-Faces-HQ (FFHQ) dataset.

## Results

NB: results are different if the code is run twice, even if the same pre-processing is used.

### With center-cropping as sole pre-processing

The result below is obtained with center-cropping as sole pre-processing, hence some issues with the projection.

![Projection (with issues) as GIF](https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/gif/movie0000-opt.gif)

From left to right: the target image, the result obtained at the start of the projection, and the final result of the projection.

<img alt="Target image" src="https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/00000-project-real-images/image0000-target.png" width="250"><img alt="Projected image n°1/5" src="https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/00000-project-real-images/image0000-step0200.png" width="250"><img alt="Projected image n°5/5" src="https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/00000-project-real-images/image0000-step1000.png" width="250">

From left to right: the target image, the result obtained at the start of the projection, intermediate results, and the final result.

![Projection results (with issues) as PNG](https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/results/result0000.png)

The background, the hair, the ears, and the suit are relatively well reproduced, but the face is wrong, especially the neck (in the original image) is confused with the chin (in the projected images).
It is possible that the face is too small relatively to the rest of the image, compared to the FFHQ training dataset, hence the poor results of the projection.

### With the same pre-processing as for the FFHQ dataset

The result below is obtained with the same pre-processing as for the FFHQ dataset, which allows to avoid the projection issues mentioned above.

![Projection (without issues) as GIF](https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/gif/movie0001-opt.gif)

From left to right: the target image, the result obtained at the start of the projection, and the final result of the projection.

<img alt="Target image" src="https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/00001-project-real-images/image0001-target.png" width="250"><img alt="Projected image n°1/5" src="https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/00001-project-real-images/image0001-step0200.png" width="250"><img alt="Projected image n°5/5" src="https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/00001-project-real-images/image0001-step1000.png" width="250">

From left to right: the target image, the result obtained at the start of the projection, intermediate results, and the final result.

![Projection results as PNG](https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/results/result0001.png)

## References

-   StyleGAN2:
    -   [StyleGAN2](https://github.com/NVlabs/stylegan2)
    -   [Steam-StyleGAN2](https://github.com/woctezuma/steam-stylegan2)
-   [rolux/stylegan2encoder](https://github.com/rolux/stylegan2encoder): align faces based on detected landmarks (same as FFHQ pre-processing).
-   [rosasalberto/StyleGAN2-TensorFlow-2.x][rosasalberto-fork]: tutorial notebooks to [generate][rosasalberto-sample-from-latents] from latent vectors and [edit][rosasalberto-edit-latents] them.
-   Learnt [latent directions](https://github.com/a312863063/generators-with-stylegan2) for StyleGAN2
-   Colab [user interface](https://github.com/tg-bomze/StyleGAN2-Face-Modificator) for projection and face modification along latent directions
-   Interesting external tools:
    -   On my Wiki: [GIF editing][wiki-gif-editing] with [MoviePy][moviepy] and [Gifsicle][gifsicle]
    -   [ArtBreeder](https://artbreeder.com/) by Joel Simon
-   Papers about discovering latent directions:
    - [Shen, Y., Gu, J., Tang, X., & Zhou, B. (2019). Interpreting the latent space of gans for semantic face editing. arXiv preprint arXiv:1907.10786.][interfacegan]
    - [Härkönen, E., Hertzmann, A., Lehtinen, J., & Paris, S. (2020). GANSpace: Discovering Interpretable GAN Controls. arXiv preprint arXiv:2004.02546.][ganspace]
    - [Pidhorskyi, S., Adjeroh, D., & Doretto, G. (2020). Adversarial Latent Autoencoders. arXiv preprint arXiv:2004.04467.][ALAE]
    - [Shen, Y., & Zhou, B. (2020). Closed-Form Factorization of Latent Semantics in GANs. arXiv preprint arXiv:2007.06600.][closed-form]

<!-- Definitions -->

[french-president]: <https://cdn.static01.nicematin.com/media/npo/1440w/2017/06/emmanuel-macron.jpg>
[french-president-archive]: <https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/img/emmanuel-macron.jpg>
[french-government]: <https://fr.wikipedia.org/wiki/Gouvernement_%C3%89douard_Philippe_(2)#Galerie_du_gouvernement_actuel>
[french-government-archive]: <https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/img/french-government-links.txt>
[famous-paintings-archive]: <https://raw.githubusercontent.com/wiki/woctezuma/stylegan2-projecting-images/img/famous-paintings-links.txt>
[FFHQ dataset]: <https://github.com/NVlabs/ffhq-dataset>
[dlib]: <http://dlib.net/face_landmark_detection.py.html>
[FFHQ pre-processing code]: <https://github.com/NVlabs/ffhq-dataset/blob/master/download_ffhq.py>

[stylegan2_projecting_images]: <https://colab.research.google.com/github/woctezuma/stylegan2-projecting-images/blob/master/stylegan2_projecting_images.ipynb>

[wiki-gif-editing]: <https://github.com/woctezuma/stylegan2-projecting-images/wiki/README>
[moviepy]: <https://github.com/Zulko/moviepy>
[gifsicle]: <https://github.com/kohler/gifsicle>

[interfacegan]: <https://github.com/genforce/interfacegan>
[ganspace]: <https://github.com/harskish/ganspace>
[ALAE]: <https://github.com/podgorskiy/ALAE>
[closed-form]: <https://github.com/rosinality/stylegan2-pytorch#closed-form-factorization-httpsarxivorgabs200706600>

[rosasalberto-fork]: <https://github.com/rosasalberto/StyleGAN2-TensorFlow-2.x>
[rosasalberto-sample-from-latents]: <https://github.com/rosasalberto/StyleGAN2-TensorFlow-2.x/blob/master/example_how_to_use.ipynb>
[rosasalberto-edit-latents]: <https://github.com/rosasalberto/StyleGAN2-TensorFlow-2.x/blob/master/example_latent_changes.ipynb>
