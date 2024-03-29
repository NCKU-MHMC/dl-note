- ## 特點
	- 與 [[Multilayer Perceptron]] 相比具有平移不變性
	- 相比 [[RNN]] 具有高度平行化
	- 感受野（Receptive Field）內的資訊不會遺失
		- 但無法取代以外的資訊
		- 感受野大小在設計架構時就已經確立
	- 訓練所需的資料量比 [[Transformer Block]] 更少
- ## 細節
	- Convolution
		- ![conv.png](../assets/conv.png){:width 500}
		- ![conv-slide.gif](../assets/conv-slide.gif){:width 500}
			- [DEMYSTIFYING DEEP LEARNING: PART 8, Convolutional Neural Networks](https://mukulrathi.com/demystifying-deep-learning/convolutional-neural-network-from-scratch/#interpretation-2-a-sliding-filter-over-the-image)
	- Receptive Field
		- ![receptive_field.png](../assets/receptive_field.png){:width 450}
		- 經過越多層的 Convolutional Layer 就能處理更範圍的資訊
	- Padding
		- ![padding.png](../assets/padding.png){:width 400}
		- 藉由調整 Padding size，可以讓輸出的 feature map 大小固定
	- Pooling
		- ![pooling.png](../assets/pooling.png){:width 400}
		- {{video https://youtu.be/fApFKmXcp2Y}}
		- 能夠縮小輸出的 feature map，快速的增加感受野範圍並減少下一層 Convolution 的計算量
			- 但將 feature map 縮小有可能會遺失細部資訊
	- Stride
		- ![stride.png](../assets/stride.png){:width 450}
		- 功能與 Pooling 相近，但除了下一層之外還連帶減少本次的計算量
	- Dilation
		- ![dilation_conv.gif](../assets/dilation_conv.gif)
			- https://github.com/vdumoulin/conv_arithmetic
		- 能在不改變 feature map 大小的情況下擴張感受野並限制計算量