- [Attention is all you need](https://papers.nips.cc/paper/2017/hash/3f5ee243547dee91fbd053c1c4a845aa-Abstract.html), NIPS, 2017
- ## 前置
	- [[ResNet]]
	- [[Multi-Head Attention]]
- ## Encoder Layer
	- Encoder Layer 中的輸入只有一串長度為 $T$ 的序列，
	  並使用 Multi-Head **Self** Attention（$Q_{in}$ 與 $K_{in}$&$V_{in}$ 的來源**相同**）抽取輸入的特徵
	- ### 計算流程
		- $\textbf{Input}~x\in\mathbb{R}^{T\times d},~M\in\mathbb{R}^{T\times T}$
		- $\textbf{Output}~o\in\mathbb{R}^{T\times d}$
		- $\textbf{Params}~\gamma,~\hat{\gamma},~\beta,~\hat{\beta},~\phi,~\hat{\phi}$
		- $\textbf{Forward}$
			- $h\leftarrow (\text{LN}_{\gamma,\beta}\circ add(x)\circ \text{MHAttn}_{\phi})(x,x,x,M)$ // Self Attention
			- $o\leftarrow (\text{LN}_{\hat{\gamma},\hat{\beta}}\circ add(h)\circ \text{MLP}_{\hat{\phi}})(h)$
		- > $\text{MHAttn}(Q_{\text{in}},K_{\text{in}},V_{\text{in}},M)$：Multi-Head Attention
		  > 
		  > $add(a)(b)$：$a+b$，residual 機制的 shortcut
		  > 
		  > $\text{LN}(\cdot)$：Layer Normalization
- ## Decoder Layer
	- Decoder Layer 有兩串輸入，分別為長度為 $L$ 的序列 input $x$ 與長度為 $T$ 的序列 memory $m$，
	  除了 Self Attention 外還會使用 Multi-Head **Cross** Attention（$Q_{in}$ 與 $K_{in}$&$V_{in}$ 的來源**不同**）融合 input 與 memory 的資訊
		- 使用 Cross Attention 可以將兩串不同長度的特徵序列合成
	- ### 計算流程
		- $\textbf{Input}~x\in\mathbb{R}^{L\times d}, m\in\mathbb{R}^{T\times d},~M_{\text{self}}\in\mathbb{R}^{L\times L},~M_{\text{cross}}\in\mathbb{R}^{L\times T}$
		- $\textbf{Output}~o\in\mathbb{R}^{L\times d}$
		- $\textbf{Params}~\gamma,~\hat{\gamma},~\tilde{\gamma},~\beta,~\hat{\beta},~\tilde{\beta},~\phi,~\hat{\phi},~\tilde{\phi}$
		- $\textbf{Forward}$
			- $h\leftarrow (\text{LN}_{\gamma,\beta}\circ add(x)\circ \text{MHAttn}_{\phi})(x,x,x,M_{\text{self}})$ // Self Attention
			- $u\leftarrow (\text{LN}_{\hat{\gamma},\hat{\beta}}\circ add(h)\circ \text{MHAttn}_{\hat{\phi}})(h,m,m,M_{\text{cross}})$ // Cross Attention
			- $o\leftarrow (\text{LN}_{\tilde{\gamma},\tilde{\beta}}\circ add(u)\circ \text{MLP}_{\tilde{\phi}})(u)$
- ## 更多研究
	- Post-LN 與 Pre-LN
		- [On Layer Normalization in the Transformer Architecture](https://arxiv.org/abs/2002.04745), ICLR, 2020
		- [On Layer Normalizations and Residual Connections in Transformers](https://arxiv.org/abs/2206.00330), arXiv, 2022
	- Skip connections（shortcut）與 MLP 的重要性
		- [Attention is Not All You Need: Pure Attention Loses Rank Doubly Exponentially with Depth](https://arxiv.org/abs/2103.03404), PMLR, 2021