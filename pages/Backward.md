- {{video https://youtu.be/9d2fwGjyb4M}}
- ## Issue
	- ### Gradient Vanishing & Explored
	  id:: 62f1118e-1c9f-4146-a393-74d1b837f08a
		- 由於[鏈式法則](https://zh.m.wikipedia.org/zh-tw/%E9%93%BE%E5%BC%8F%E6%B3%95%E5%88%99)的特性，在計算每一層參數的梯度時會累乘後方回傳的梯度，使得越靠前（接近輸入層）的梯度會成指數次的增加或減少，進而引起梯度爆炸（Gradient Explored）或梯度消失（Gradient Vanishing）
		- 梯度消失會讓模型變得難以訓練，靠近輸出的層數幾乎無法改動
	- ### Memory Cost
		- 由於 backpropagation 需要將 forward 的過程都記錄下來才能計算梯度
		  因此訓練 DL 模型會需要一定程度的記憶體。
		- 2018 年提出的 [Neural Ordinary Differential Equations](https://arxiv.org/abs/1806.07366) 系列在些許調整後可以用來解決這個問題，但代價是更長的訓練時間