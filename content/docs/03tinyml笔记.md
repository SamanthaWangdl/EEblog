# 深度学习 边缘部署



![img](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/NeuralNetworkZo19High.png)

• **RecurrentNN(RNN)** – feedback

• **LongShort-TermMemory(LSTM)** – feedback + storage

• **Encoders
** – output smaller than input

• **Decoders
** – output larger than input

• **Transformers
** – “attention” mechanism

![Screenshot 2024-01-15 at 12.00.55](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot 2024-01-15 at 12.00.55.png)

Size of
 **Output Feature Map** = (**Input Feature Map** – **Filter** + **Stride**) / **Stride**

*# of multiplications?*

![Screenshot 2024-01-15 at 12.06.07](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot 2024-01-15 at 12.06.07.png)

![Screenshot 2024-01-15 at 12.06.35](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot 2024-01-15 at 12.06.35.png)

- **N – Number of** **input fmaps/****output fmaps** **(batch size)**
- **C – Number of channels in** **input fmaps** **(activations) &** **filters** **(weights)**
- **H – Height of** **input fmap** **(activations)**
- **W – Width of** **input fmap** **(activations)**
- **R – Height of** **filter** **(weights)**
- **S – Width of** **filter** **(weights)**
- **M – Number of channels in** **output fmaps** **(activations)**
- **P – Height of** **output fmap** **(activations)**
- **Q – Width of** **output fmap** **(activations)**
- **U – Stride of convolution**

![Screenshot 2024-01-15 at 12.08.36](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot 2024-01-15 at 12.08.36.png)

![Screenshot 2024-01-15 at 12.09.42](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot 2024-01-15 at 12.09.42.png)

![Screenshot 2024-01-15 at 12.10.32](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot 2024-01-15 at 12.10.32.png)

![Screenshot 2024-01-15 at 12.12.58](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot%202024-01-15%20at%2012.12.58.png)

还给了einstein公式

no need for bn

Typical operations that we will use: 

– Convolution (CONV)

– Fully-Connected (FC) 

– Max Pooling
 – ReLU



**Popular CNNs**

• **LeNet** (1998)

• **AlexNet** (2012)

• **OverFeat** (2013)

• **VGGNet** (2014)

• **GoogleNet** (2014)

• **ResNet** (2015)

![Screenshot 2024-01-11 at 16.39.15](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot%202024-01-11%20at%2016.39.15.png)

（on imagenet）

![Screenshot 2024-01-15 at 12.18.36](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot 2024-01-15 at 12.18.36.png)

![Screenshot 2024-01-15 at 12.28.14](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot 2024-01-15 at 12.28.14.png)

![Screenshot 2024-01-15 at 12.29.22](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot 2024-01-15 at 12.29.22.png)

![Screenshot 2024-01-15 at 12.31.23](https://raw.githubusercontent.com/SamanthaWangdl/imagehub/main/imagehub/Screenshot 2024-01-15 at 12.31.23.png)

stacked filter

bottlenet 是啥

靠，这个ppt内容超多。。。