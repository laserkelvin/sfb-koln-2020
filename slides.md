---
title: SFB-AstroML-Day 2020
revealOptions:
    transition: 'fade'
    transition-speed: 'fast'
    width: '100%'
    height: '100%'
    center: false
    margin: 0
    minScale: 1
    maxScale: 1
    symbolperslideprogress:
        position: 'left'
        align: 'vertical'
        symbolColor: ""
        symbolActiveColor: ""
    menu:
        side: "left"
        width: "normal"
    tableofcontents:
        title: ""
        position: 2
        titleTag: "h1"
        titleTagSelector: "h1, h2, h3"
        ignoreFirstSlide: true

---

# Semi-Supervised Machine Learning for Molecular Spectroscopy

### Kelvin Lee

#### SFB AstroML Day

<figure>
	<img class="column" src="figures/mit-logo.png" style="width: 40%; padding: 20px">
	<img class="column" src="figures/cfa-logo-transparent.png" style="width: 40%">
</figure>

---

# Machine Learning in Spectroscopy

<div style="padding-top: 200px"> 

<div class="column" style="width: 30%">
  <figure>
  <img src="figures/benzene.svg" style="width: 80%">
  <figcaption> Large data volumes </figcaption>
  </figure>
</div>

<div class="column" style="width: 20%">
  <figure>

  <p style="display: block; margin: auto; width: 50%; padding-top: 60px; padding-bottom: 60px;"> $\hat{H} \Psi = E\Psi$ </p>

  <figcaption> Approximations to intractable problems </figcaption>
  </figure>
</div>

<div class="column">
  <figure>
  <img src="figures/matched-filter.png" style="width: 70%">
  <figcaption>  Simulations of rare events </figcaption>
  </figure>
</div>

</div>

----

# Automation through Machine Learning

<div id="left" style="padding-top: 50px">
  <figure>
    <img src="https://imgs.xkcd.com/comics/automation.png" style="width: 600px">
  </figure>
</div>

<div class="fragment" id="right" style="padding-top: 200px">
  There is a hidden dimension to the problem:

  > How _reliable_ is the automation?
</div>

----

# Reliable machine learning

<div id="left" style="padding-top: 100px">

- How reliable are machine (deep) learning models?
- Model overconfidence and inaccuracies with unseen data
- Need to make models robust by design

<p class="pop fragment"> Take the machine learning off autopilot! </p>

<div class="fragment">

  Semi-supervised learning to get best of both worlds:

  - Human and physical intuition
  - Model uncertainty
  - Generalization

</div>

</div>

<div id="right">

<figure style="display: block; margin: auto; width: 80%">
<img src="figures/adversarial-attack.png">
<figcaption>Goodfellow, arXiv: 1412.6572</figcaption>

<img src="figures/natural-adversarial.png" style="width: 80%">
<figcaption>Hendrycks, arXiv: 1907.07174</figcaption>

</figure>

</div>

----

# Applications

<div style="padding-top: 170px">

<div style="width: 40%; display: inline-block">

  <figure>
    <img src="figures/stephen-ion-image.png" style="width: 50%; margin: auto; display:block">
    <figcaption>Ion imaging</figcaption>
  </figure>

</div>

<div style="width: 40%; display: inline-block;">

<figure>
  <img src="figures/benzene.svg" style="width: 90%; margin: auto; display:block">
  <figcaption>Spectroscopic line assignment and analysis</figcaption>
</figure>

</div>

</div>

---

# Ion imaging

<div id="left">

- Measuring nascent charged particle velocity
- Infer dynamics from radial and angular (anisotropy) distributions

<div class="fragment">

- Sensitivity of reconstruction to noise and affine transformations
- Image resolution
- Low signal counts
- Solve these problems with deep convolutional neural networks!

</div>

<div class="fragment">
  
  <figure>
    <img src="figures/yen_hl_tau.png" style="width: 40%">
    <figcaption>Many of the same challenges in astronomical imaging!</figcaption>
  </figure>
  </div>

</div>

<div id="right">
  <figure>
    <img src="figures/vmi-experiment.png">
  </figure>
</div>

----

# Autoencoder models

<div id="left">

- Encoder and decoder models learn cooperatively to reconstruct input data from compression
  - Encoder learns to extract useful information
  - Decoder learns to recreate original image
- Apply model to reconstruct true 3D distribution from 2D projections

</div>

<div id="right">
  <figure>

  <img src="figures/autoencoder.svg">

  </figure>
</div>

<div class="fragment">

$\mathscr{L}_\theta = \mathrm{MSE}(I, I_\theta)$

> Simple reconstruction loss between input image $I$ and predicted image $I_\theta$

</div>

----

<div>
  <figure>
    <img src="figures/unsupervised-result-10epochs.png" style="width: 1400px">
    <figcaption>Ten epochs</figcaption>
  </figure>
  </div>

----

# Semi-supervised autoencoder

<div id="left">

Convergence is slow, and anisotropy not captured well

<div class="fragment">

$\mathscr{L}_\theta = \mathrm{MSE}(I, I_\theta) + \gamma[\mathrm{MSE}(r(I), r'_\theta) + \mathrm{MSE}(r(I), r_\theta(I_\theta))]$

> Loss forces encoder to extract desired radial distribution
  
1. What the encoder _thinks_ the radial distribution is
2. What the actual radial distribution is

Hyperparameter $\gamma$ tunes relative importance

</div>

</div>

<div id="right" class="fragment">

<figure>
  <img src="figures/predict_radial_profile.png">
  <figcaption>Fewer epochs, better reconstruction!</figcaption>
</figure>

</div>

----

<div>
  <figure>
    <img src="figures/50epochs.png" style="width: 1400px">
    <figcaption>$\gamma = 0.3$, 10 epochs</figcaption>
  </figure>
  </div>

----

# Next steps

> Reconstructing inputs is not as useful as it can be!

<div id="left">

<div class="fragment" style="padding-top: 200px">
  <ol>
    <li>Image de-noising and focusing</li>
    <li>Pixelwise conditional reconstruction (PixelCNN)</li>
    <li>Quantifiable uncertainty ($\beta$-VAE)</li>
    <li>Super-resolution imaging</li>
    <li>Image segmentation</li>
  </ol>
</div>
</div>

<div id="right" class="fragment">

  <figure>
    <img src="figures/uncertainty.png">
  </figure>

  <figure>
    <img src="figures/segmentation.png">
  </figure>

</div>

----

<div>
  <figure>
    <img src="figures/variational-autoencoder.svg" style="width: 1400px">
  </figure>

  > Generative model for low-signal images, upsampling, and segmentation
</div>

---

# Spectroscopic analysis

<div id="left">

- Radio band molecular line surveys
- Molecules as sensitive probes of the ISM
  - Temperature and density estimation
- From molecules to planets and stars
- Origins of life

<div class="fragment" data-fragment-index=1>

> Spectra don't come with labels!

High resolution and bandwidth spectra now routine; we are drowning in data!

</div>

</div>

<div id="right" class="fragment" data-fragment-index=1>
  <div>
    <embed src="figures/benzene-spectrum.html" width=900px height=500px>
  </div>
</div>

----

# Spectroscopic deep learning

> Designing intelligent systems to automate spectroscopic analysis

<div class="fragment" style="display: block; margin: auto; width: 50%; padding-top: 150px">

For a given congested spectrum:

1. Which features belong to the same molecule(s)?
2. What is the identity of unknown signal carriers?

</div>

----

# Spectral autoencoder

<div id="left">
  
  > Train model to _understand_ molecular spectra

<div class="fragment" style="padding-top: 30px">

  Semi-supervised autoencoder learning of sequences with three targets, for observed frequencies $\nu$
  
  - Reproduce current frequency
  - Predict next frequency
  - Classify spectral type ($a$, $b$, $c$-type)

</div>

</div>

<div id="right">

<figure>
  <img src="figures/spectral-encoder-decoder.svg" style="width: 70%">
</figure>

</div>

----

# Spectra, or noise?

<div id="left">

<figure>
  <img src="figures/embedding-viz.png">
  <figcaption>UMAP embedding visualization</figcaption>
</figure>

- 99% spectral type classification accuracy
- Reproduction error of 0.1% (100 MHz at 100 GHz)
- Prediction error of 0.2%

<div class="fragment" data-fragment-index=1>

- 97% discriminator classification accuracy

</div>

</div>

<div id="right" style="padding-left: 50px" class="fragment" data-fragment-index=1>
  <img src="figures/recurrent-encoder-decoder.png" style="width: 50%">
</div>

----

# Computer spectroscopist

> Deep reinforcement learning for spectroscopic assignment and segmentation

<div id="left">

<div>

  1. Collect spectra
  2. Screen spectra for molecular features
  3. Fit transitions to rotational Hamiltonians
  4. Identify carriers from rotational parameters

</div>

<div class="fragment" data-fragment-index=1>

  > Replace (2) with actor-critic model to significantly narrow down candidate sequences

  > See McCarthy & Lee arXiv: 2003.12388 for (4)

</div>

</div>

<div id="right" class="fragment" data-fragment-index=1>

  <figure style="padding-top: 100px">
    <img src="figures/reinforcement_learning.svg" style="width: 60%">
  </figure>

</div>

---

# Take home messages

<div style="padding-top: 200px">

> Deep learning can automate significant portions of conventional spectroscopic workflows.

> Models developed for spectroscopy useful for laboratory and observational data.

> Learning needs to be semi-supervised—for convergence and for reliability.

</div>

----

# Acknowledgements

<div id="left">

<figure style="padding-left: 50px; padding-top: 100px">
  <img src="figures/kocheril.jpg" style="width: 90%;">
  <figcaption>Stephen Kocheril (Brown) </figcaption>
</figure>

</div>

<div id="right">

  <figure>
    <img class="round-img" src="figures/mccarthy2016.jpg" style="width: 250px;">
    <figcaption>Michael McCarthy (CfA) </figcaption>
  </figure>

  <figure style="padding-left: 50px">
    <img class="round-img" src="figures/mcguire2018.jpg" style="width: 250px;">
    <figcaption>Brett McGuire (MIT) </figcaption>
  </figure>

  <div style="padding-top: 50px">
  <figure>
    <img src="figures/nsf.png" style="width: 320px">
  </figure>

  <figure style="padding-left: 50px">
    <img src="figures/nasa.png" style="width: 320px">
  </figure>
  </div>

</div>

----

<div class="grid sidebar">
    <h1> Thank you! </h1>
</div>

<div class="l-multiple" style="padding-top: 200px">
    <div class="img-frame">
        <img src="figures/twitter.png" class="end-icons">
        <span>@cmmmsubmm</span>
    </div>
    <div class="img-frame">
        <img src="figures/www.png" class="end-icons">
        <span>laserkelvin.github.io</span>
    </div>
    <div class="img-frame">
      <img src="figures/Octocat.png" class="end-icons">
      <span>@laserkelvin</span>
    </div>
</div>

<footer>

<!-- Copyright © 2020 Kelvin Lee -->

</footer>
