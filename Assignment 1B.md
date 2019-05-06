Channels:
A channel is a container of a specific kind of information(in context of computer vision). It is a bag of similar features.
An image can be seen as a combination of various types of simple or complex features, for example, edges/gradients, textures, patterns, part of objects, objects etc. A channel can be seen as a group of similar features within the image. eg: one channel for horizontal edges, another for vertical etc. Another important thing to notice, since a channel is a group of similar features of a single image, an image can be divided into multiple channels and when we combine all channels of an image, it will result in the original image reformation.

Kernels:
A kernel is a numerical matix which by the process of convulution, extracts the features from an image. Different kernel are required to extract different features from image. eg: a horizontal edge detector will be different from vertical edge detector. And since a channel is a bag of similar features, each kernel will have seperate channel for it in the output. A kernel is also called a feature extractor or a filter.

Benefits of 3x3 Kernels:
We should try to use 3x3 kernel because the convolution process of higher dimensional kernel can be achieved through a sequence of 3x3 convolutions. For example a 5X5 convolution on a 7X7 image will result in 3X3 image. This computation can also be obtained by performing 3X3 convolution on 7X7 image 2 times sequentially. 7X7 image -(3x3 kernel)-> 5X5 -(3x3 kernel)-> 3X3 image. Here we are obtaining same output through 3X3 kernels, but the advantage behind using 3X3 kernel is that it will use less no of computation cycles as compared to 5X5 convolution.

199x199 to 1X1 through 3X3 convolution:
199 -> 197 -> 195 -> 193 -> 191 -> 189 -> 187 -> 185 -> 183 -> 181 -> 179 -> 177 -> 175 -> 173 -> 171 -> 169 -> 167 -> 165 -> 163 -> 161-> 159 -> 157 -> 155 -> 153 -> 151 -> 149 -> 147 -> 145 -> 143 -> 141 -> 139 -> 137 -> 135 -> 133 -> 131 -> 129 -> 127 -> 125 -> 123 -> 121->
119 -> 117 -> 115 -> 113 -> 111 -> 109 -> 107 -> 105 -> 103 -> 101 -> 99 -> 97 -> 95 -> 93 -> 91 -> 89 -> 87 -> 85 -> 83 -> 81 -> 79 ->
77 -> 75 -> 73 -> 71 -> 69 -> 67 -> 65 -> 63 -> 61 -> 59 -> 57 -> 55 -> 53 -> 51 -> 49 -> 47 -> 45 -> 43 -> 41 -> 39 -> 37 -> 35 -> 33 ->
31 -> 29 -> 27 -> 25 -> 23 -> 21 -> 19 -> 17 -> 15 -> 13 -> 11 -> 9 -> 7 -> 5 -> 3 -> 1. In total, we need to perform 3x3 convolution operation 99 times to reach 1x1 from 199x199.
