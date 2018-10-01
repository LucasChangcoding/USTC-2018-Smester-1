##	区块链第一次实验

通过区块链课程的实验，我们将实现一个简化版的区块链，并基于它来构建一个简化版的加密货币。

第一次实验有以下几点内容，每一小节分别对应一个文件夹，其中包含了 `Go` 和 `C++` 的实现

*	Prototype, 基本原型

*	PoW, 工作量证明

*	Persistence, 持久化(内存->磁盘)

*	CLI, 命令行接口

<br>

##	总结整理

本次实验体现的中心思想就是计算 `validHash = sha256(header)`

*	对于 `Prototype`

	```
	header := prevHash + msg + timestamp
	validHash = sha256(header)
	```

	`Prototype` 仅作展示，对 `validHash` 没有限制，所以创建成本很低

*	增加 `PoW`

	```
	header = prevHash + msg + timestamp + targetBits + nonce
	hash = sha256(header)
	validHash = validate(hash)
	```

	增加了 `PoW` 之后，我们对 `validHash` 就有了限制，即，`validHash` 的二进制形式的前 `targetBits` 位必须是 `0`

	由于 `prevHash`, `targetBits` 都是确定的值，而当我们在某个时间点准备创建新的 `block` 时，`timestamp` 也就确定了。于是，只有改变 `nonce` 才能改变输入量 `header` ，进而改变 `sha256(header)` 的结果

	所以，我们需要对输入量中的 `nonce` 进行遍历搜索，再进行 `sha256(header)` ，试图找到一个符合要求的 `validHash`

	这个过程就是挖矿 (mining)，挖矿比较耗时耗力，是你的工作量证明(Proof of Work)

*	持久化

	把内存中的数据保存到硬盘，使得数据可以长久保存

*	CLI

	增加命令行接口，方便交互

<br>

##	参考资料

*	[Building Blockchain in Go](https://jeiwan.cc/)

*	[Building Blockchain in Go, 中译 GitBook](https://liuchengxu.gitbook.io/blockchain/)

*	[blockchain_go, 实验文档](https://github.com/jJayyyyyyy/USTC-2018-Smester-1/blob/master/Blockchain/test00/blockchain_go.pdf)

<br>