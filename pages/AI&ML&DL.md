- AI
	- 設計模擬人類行為的函數 $f_{\phi}(x)$
		- $\phi$ 與 $x$ 分別代表參數與輸入
	- ML
		- 從資料中學習不斷學習並更新參數 $\phi$
		- 像是 HMM、GMM、Decision Tree 與 Neural Network
		- DL #[[DL Introduction]]
			- $f$ 由多層（Deep）的 Neural Network 組成
			- $f_{\phi}(x)\equiv (f^{(n)}_{\phi_n}\circ\cdots\circ f^{(2)}_{\phi_2}\circ f^{(1)}_{\phi_1})(x)$
				- $f^{(i)}_{\phi_i}$ 皆是由 Neural Network 建構