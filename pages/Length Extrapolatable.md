- [蘇劍林老師對 Transformer 外推機制的研究與想法](https://spaces.ac.cn/tag/外推/)
- 由於 Transformer 需要使用 Positional Encoding 獲取位置資訊，而位置數量則是在訓練時就決定好的超參數，因此不能如同 RNN 與 CNN 一般任意擴展輸入大小。
- ##  [Train Short, Test Long](https://arxiv.org/abs/2108.12409)
	- 為了解決這些限制，後續有許多研究在探討如何作到 [Train Short, Test Long](https://arxiv.org/abs/2108.12409)，希望在訓練時使用較短的輸入可以減少 Transformer $O(L^2)$ 的空間複雜度帶來的成本，並在推理時能接收到更長的輸入序列而不會降低性能。
	- 依據 https://spaces.ac.cn/archives/8823 的推導與實驗，將 self attn 在 softmax 前乘上一個縮放係數 $\cfrac{log_{512}n}{\sqrt{d}}$ 來強化外推能力
- ## 不使用 PE
	- 依據 [Transformer Language Models without Positional Encodings Still Learn Positional Information](https://aclanthology.org/2022.findings-emnlp.99/)，使用 Causal Mask 的 [[Autoregression]] Transformer 實際上不用加上 PE 也可以透過單向 AR 的機制學到位置資訊
	- https://paperswithcode.com/paper/the-impact-of-positional-encoding-on-length
	- [The Impact of Positional Encoding on Length Generalization in Transformers](https://arxiv.org/abs/2305.19466)
	-