- 像是 [[Self-Supervised]] 與 [[Self-Supervised]] 等等方法可以使用未標記訓練
	- 此類方法在實際測試時也可以將測試資料視為未標記再次訓練
	- 這種使用到測試資料訓練的方法就是 Transductive Learning
	- > **並沒有使用到測試資料的人工標記**
- ## Inductive Learning
	- 沒有以任何形式將測試資料加入訓練
		- e.g. Supervised Learning 所使用的訓練資料與測試資料完全不重疊