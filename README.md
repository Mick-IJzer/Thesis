# Who Needs an Encoder? Evaluating the Use of Random Latent Representations in Variational Autoencoders

This repository contains the most important documents of my thesis for the Master Artificial Intelligence at the Vrije Universiteit Amsterdam. This project was carried out under supervision of Jakub Tomczak.

## Abstract
In recent years generative models have been the focus of many studies. As the name implies, generative models can generate novel data based on some initial data set. The most used and most well-known generative models are Variational Autoencoders (VAEs) and Generative Adversarial Networks (GANs). While VAEs are often more stable to train, the images GANs produce tend to be of better quality. In VAEs the latent representation of a data point is learned by an encoder that is parameterized by a neural network. In this report, the learned latent representations are replaced by a randomly generated latent representations. This is achieved by freezing the weights of the encoder directly after initialization. Additionally, the effect of using random kitchen sinks instead of the regular encoder will be assessed as well. Results are obtained by training and evaluating 24 VAEs on the MNIST data set. The factors that are used are related to the encoder type (i.e. learnable, partially non-learnable, non-learnable, and random kitchen sinks), layer type (i.e. fully connected and convolutional), and prior (i.e. standard normal prior, Real-NVP flow-prior with 2 flows, and Real-NVP flow-prior with 6 flows). Results demonstrate that a decent quality of generated images can be produced when using randomly generated latent representations. However, the quality of generated images is not as high as that of the standard encoder, and the circumstances under which a VAE can use random latent representations are very specific. A fully convolutional VAE in combination with a Real-NVP flow-prior with 6 flows were needed to produce interpretable results. The main conclusions are that (1) it is possible to use randomly generated latent representations in VAEs, (2) the power of VAEs does not depend on the encoder, but rather the combination of the encoder, prior, and decoder, and (3) a VAE can be made more computationally efficient without losing generative performance by making the first layers of the encoder non-learnable. Implications, limitations, and future research directions are discussed.

## Structure of the repository
Only the most relevant documents are uploaded to this repository. More specifically, the full thesis, two presentations, the code, and the results are uploaded. The two presentations are part of the required KIM meetings, where the first presentation covers the project plan and the final presentation covers the complete thesis. The code is split into two seperate files; one for the VAEs with convolutional layers and one for the VAEs with fully connected layers. The only differences between these to files are the layer-types (i.e. linear/convolutional) that were used in defining the classes for the encoder and decoder. With respect to the results folder there are two types of files; the quantitative metrics that werer computed after training each model, and the reconstructed, generated images and the interpolation between generated images. The two csv files contain the quantitative metrics and the subsequent folders (i.e. MNIST images and SVHN images) contain the png files. It is important to note that the entire experiment was carried out five times. This means that for each combination of prior, layer type, and encoder type there are five files for the generated images etc. and five entries in the csv files.

## Using this repository
To be able to use the code there are several packages that have to be installed (see Requirements.txt || TODO). Additionally, the MNIST data set and SVHN data set have to be downloaded. Finally, the paths where the data is retrieved and where the results are saved should be changed to suit your own folder structure. For each epoch the negative ELBO, the reconstruction error, and the regularization term will be printed. Every 10 epochs the qualitative performance of the VAE is made visible by generating 64 new images, reconstructing 8 images, and plotting the interpolation between 8 pairs of generated images. These png files are saved in a seperate folder. This way it is possible to keep an eye on the qualitative and quantitative performance of the VAE while training. Within the notebooks there is a cell that contains the hyperparameters (e.g. learning rate and number of epochs), and the data set that is used. If you wish to train and evaluate a single encoder type and prior, you have to define those variables and then call the experiment() function. The definition of the required variables is as follows:
* Learnable Encoder: 'variant = "Normal"' and 'partial = True'
* Partially Non-Learnable Encoder: 'variant = "RandomNet"' and 'partial = True'
* Non-Learnable Encoder: 'variant = "RandomNet"' and 'partial = False'
* Random Kitchen Sinks Encoder: 'variant = "RKS"' and 'partial = False'
* Standard Normal Prior: 'prior = "Normal"' and 'flows = 2'
* Real-NVP Flow-prior with **n** flows: 'prior = "Flow"' and 'flows = **n**'
