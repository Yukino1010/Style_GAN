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

In the case that we want to control two factors (eyes and face size), we assume that we only need to modify a single element of the latent vector to control both eye and face size at the same time. (entanglement) <br>

By controlling (increase or decrease) the value of the element, we could get four kinds of different combinations [small eyes, small face], [small eyes, big face], [big eyes,  small face] and [big eyes, big face]. However, the combination [small eyes, big face] and [big eyes,  small face] are rare or do not exist in real-world situations. As a result, the generator will try to generate images that are unrealistic. <br>

With the mapping net of the latent vector (z), we can now expect the FC layer could transfer the original vector z into w which has disentangled spaces (simply means each element of vector w only control a single style)

## Synthesis network

Synthesis network is another important change in style gan. Unlike the classic gan using latent vectors z as the sources to generate images, style gan uses the z to change the style of the image. <br>

***Classic GAN***: 

The image is generated from the latent vectors z. By upsampling the vectors z, we could get the image with a shape (64, 64, 3). In this case, z could be seen as the source of the generator. 

***Style GAN***:

Different to the classic gan, the latent vector w of the Style GAN is applied to all the layers. This could be seen as vector w is only used for the style transfer in each layer. Besides, the starting point of the network will be a constant value. (the starting point of the classic gan is latent vectors z)

# Result
By controlling the input of the last style block, we can control the hair color of the image. <br>
I haven't tried to modify the input of other style blocks, but we could expect that each style block will control certain style!

![image](https://github.com/Yukino1010/Style_GAN/blob/master/results/demo/final_image1.png)
![image](https://github.com/Yukino1010/Style_GAN/blob/master/results/demo/final_image2.png)

# Reference
1. ***Generative Adversarial Networks*** [[arxiv](https://arxiv.org/abs/1406.2661)]
2. ***A Style-Based Generator Architecture for Generative Adversarial Networks*** [[arxiv](https://arxiv.org/abs/1812.04948)]
3. ***Face image generation with StyleGAN*** (https://keras.io/examples/generative/stylegan/)
