# Style_GAN

The Style Generative Adversarial Network, or StyleGAN for short, is an extension of the GAN architecture first proposed by Karras et al., (2018). Which introduces two new structure Mapping network and the Synthesis network.

![image](https://github.com/Yukino1010/Style_GAN/blob/master/pic2.png?raw=true)

The main modification in style gan
1. Mapping network: instead of putting the latent vector z directly into the network, StyleGAN using multiple fully connected (FC) layers to map it to the space which fits the network more.
2. The synthesis network: after we got the vector w (A) from the previous Mapping network,we concat it to every layer (AdaIN) while adding some noise (B) into it.


## Mapping network
To solve the problem of less control over the style of the classic gan, we have to first talk about the concept of entanglement. <br>

![image](https://github.com/Yukino1010/Style_GAN/blob/master/mapping_net.png)

The above was the explanation from the original paper, let's try to explain it in normal English. <br>

When we want to control a specific feature of an image, such as the hair length of a male, we often assume that this can be achieved by adjusting a single component of the latent vector. 
However, there is no guarantee that each latent component controls only a single feature due to "entanglement". <br>

For instance, if a component affects both hair length and gender, modifying it could lead to an unexpected result, such as a female with long hair. To address this issue, it's necessary to ensure that each component exclusively manages a single feature, a process known as disentangling. <br>

In StyleGAN, we can easily disentangle the latent space by introducing a mapping network composed mainly of fully connected (FC) layers !

## Synthesis network

StyleGAN introduces a unique feature in its synthesis network. Unlike traditional GANs that use latent vectors directly to generate images, StyleGAN uses these vectors to adjust the style of the image.
The latent vector w in StyleGAN is applied across all layers. This means that w is mainly used for style changes at each layer. The starting point of the network is a fixed constant, which is different from classic GANs. <br>

Moreover, since image generation in StyleGAN begins with a fixed constant, to ensure diversity in the outcomes, StyleGAN adds noise to every style block, introducing randomness into the model.
# Result
By controlling the input of the last style block, we can control the hair color of the image. <br>
I haven't tried to modify the input of other style blocks, but we could expect that each style block will control certain style!

![image](https://github.com/Yukino1010/Style_GAN/blob/master/results/demo/final_image1.png)
![image](https://github.com/Yukino1010/Style_GAN/blob/master/results/demo/final_image2.png)

# Reference
1. ***Generative Adversarial Networks*** [[arxiv](https://arxiv.org/abs/1406.2661)]
2. ***A Style-Based Generator Architecture for Generative Adversarial Networks*** [[arxiv](https://arxiv.org/abs/1812.04948)]
3. ***Face image generation with StyleGAN*** (https://keras.io/examples/generative/stylegan/)
