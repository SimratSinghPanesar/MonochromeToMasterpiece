# MonoChrome To MasterPiece
Given a grayscale photograph as input, this application attacks the problem of hallucinating a plausible color version of the photograph.
## Table of Content
  * [Demo](#demo)
  * [Overview](#overview)
  * [Motivation](#motivation)
  * [Technical Aspect](#technical-aspect)
  * [Technologies Used](#technologies-used)
  * [Credits](#credits)
## Demo
![Alt Text](https://github.com/SimratSinghPanesar/MonochromeToMasterpiece/blob/master/Result_images/OutputGif.gif)

## Overview
Image colorization is the process of taking an input grayscale (black and white) image and then producing an output colorized image that represents the semantic colors and tones of the input. For example, an ocean on a clear sunny day must be plausibly 'blue' it cannot be colored 'hot pink' by the model.

## Motivation

When I learned linear algebra and came to know about how the machine inteprets pictures as tensors and concept of image segmentation. I remember there were some movies which was restored and colorized in theatre. I came across Research papers of University of california in image colorization. And most importantly when I colorized photos of my grandparents, that smile on their faces is worth every penny.

Here is a photo of Robin William's colorized:

<img target="_blank" src="https://github.com/SimratSinghPanesar/MonochromeToMasterpiece/blob/master/Result_images/RobinWilliams.png" width=600>

## Technical Aspect
- The technique used is from Richard Zhang's 2016 ECCV paper, [Colorful Image Colorization](http://richzhang.github.io/colorization/). Developed at the University of California, Berkeley by Richard Zhang, Phillip Isola, and Alexei A. Efros.

- Previous approaches to black and white image colorization relied on manual human annotation and often produced    desaturated results that were not believable as true colorizations.

- Zhang decided to attack the problem of image colorization by using Convolutional Neural Networks to  'hallucinate' what an input grayscale image would look like when colorized.

- To train the network Zhang started with the [ImageNet dataset](http://image-net.org/) and converted all images from the RGB color space to the Lab color space.

- Similar to the RGB color space, the Lab color space has three channels. But unlike the RGB color space, Lab encodes color information differently:
  - The **L channel** encodes lightness intensity only
  - The **a channel** encodes green-red.
  - And the **b channel** encodes blue-yellow.

- As explained in the original paper, the authors, embraced the underlying uncertainty of the problem by posing it as a classification task using class-rebalancing at training time to increase the diversity of colors in the result. AI approach is implemented as a feed-forward pass in a CNN at test time and is trained on over a million color images.

- The color photos were decomposed using Lab model and 'L' channel is used as an input feature and 'a and b' channels as classification labels as shown in below diagram.

<img target="_blank" src="https://user-images.githubusercontent.com/71431013/99061015-eb844a80-25c6-11eb-8850-bcc9f74d91e6.png" width=500>

- The trained model (that is available publically and in models folder of this repo or [download it by clicking here]( http://eecs.berkeley.edu/~rich.zhang/projects/2016_colorization/files/demo_v2/colorization_release_v2.caffemodel), we can use it to colorize a new B&W photo, where this photo will be the input of the model or the component 'L'. The output of the model will be the other components 'a' and 'b', that once added to the original 'L', will return a full colorized image.

## The entire (simplified) process can be summarized as:
- Convert all training images from the RGB color space to the Lab color space.
- Use the L channel as the input to the network and train the network to predict the ab channels.
- Combine the input L channel with the predicted ab channels.
- Convert the Lab image back to RGB.

<img target="_blank" src="https://user-images.githubusercontent.com/71431013/99061033-f048fe80-25c6-11eb-8bc5-d6312c7021b6.png" width=500>

## Technologies Used
![](https://forthebadge.com/images/badges/made-with-python.svg)

[<img target="_blank" src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/32/OpenCV_Logo_with_text_svg_version.svg/730px-OpenCV_Logo_with_text_svg_version.svg.png" width=200>](https://opencv.org/)[<img target="_blank" src="https://miro.medium.com/max/4000/0*cSCGhssjeajRD3qs.png" width=200>](https://www.streamlit.io/)

## Credits
- [The official publication of Zhang et al.](http://richzhang.github.io/colorization/)
