- > IEEE/ACM TRANSACTIONS ON AUDIO, SPEECH, AND LANGUAGE PROCESSING, VOL. 31, 2023
- Phase 對時間位移太過敏感，導致其難以直接從 magnitube 直接估計，因此本研究將估測目標由 phase 換成了 Frequency Phase Difference (FPD) 與 Baseband Phase Difference (BPD) 這兩個強健性更高的相位相關係數，再利用公式將其轉換回 Phase。
- 使用 DNN 從 magnitube 估計 Frequency Phase Difference (FPD) 與 Baseband Phase Difference (BPD)
	- FPD 的計算公式為 $U[m,n]=\Phi[m,n]-\Phi[m-1,n]$
	- BPD 是由 STFT Phase Reconstruction in Voiced Speech for an Improved Single-Channel Speech Enhancement 提出，計算公式為 $W[m,n]=\mathcal{W}\left(V[m,n]-\cfrac{2\pi\alpha m}{M}\right)$，$\alpha$ 為 hop size
		- 上式的 $V[m,n]=\Phi[m,n]-\Phi[m,n-1]$，代表 Time Phase Difference
		- 而函數 $\mathcal{W}(\Phi)=\text{Arg}(e^{j\Phi})$
- 並使用估計的 FPD $\hat{U}$ 與 BPD $\hat{W}$ 計算 phase $\hat{\Phi}$ 並得到重建的複數頻譜 $\hat{X}[m,n]=A[m,n]e^{j\hat{\Phi}[m,n]}$
	- $\hat{\Phi}[m,n]=\text{Arg}(\utilde{X}[m,n])$
		- $[\utilde{X}[0,n],\ldots,\utilde{X}[M-1,n]]^{\top}=(\Lambda_n+D^{\top}_n\Gamma_n D^{\top}_n)^{-1}\Lambda_n y_n$
			- $\Lambda_n$ 與 $\Gamma_n$ 為對角矩陣，兩者的對角元素分別為
				- $\Lambda_n[m,m]=(A[m,n]A[m,n-1])^p$
				- $\Gamma_n[m,m]=\gamma_0 (A[m,n]A[m-1,n])^p$
				- 在後續的時驗中決定超參數 $p=10^{-0.4}$ 與 $\gamma_0=10$
			- $D_n \in \mathbb{R}^{M-1\times M}$
				- $D_n[m-1,m]=1$
				- $D_n[m-1,m-1]=-\mathfrak{\hat{U}}[m,n]$
					- $\mathfrak{\hat{U}[m,n]}=\cfrac{A[m,n]}{A[m-1,n]}e^{j\hat{U}[m,n]}$
				- other entries are zero.
			- $y_n=\mathfrak{\hat{V}}_n\hat{X}_{n-1}$
				- $\mathfrak{\hat{V}[m,n]}=\cfrac{A[m,n]}{A[m,n-1]}e^{j\hat{V}[m,n]}$
				- $\hat{V}[m,n]=\hat{W}[m,n]+\cfrac{2\pi\alpha m}{M}$