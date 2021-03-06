---
title: Ethereum
tags: 小书匠语法,技术
renderNumberedHeading: true
grammar_abbr: true
grammar_table: true
grammar_defList: true
grammar_emoji: true
grammar_footnote: true
grammar_ins: true
grammar_mark: true
grammar_sub: true
grammar_sup: true
grammar_checkbox: true
grammar_mathjax: true
grammar_flow: true
grammar_sequence: true
grammar_plot: true
grammar_code: true
grammar_highlight: true
grammar_html: true
grammar_linkify: true
grammar_typographer: true
grammar_video: true
grammar_audio: true
grammar_attachment: true
grammar_mermaid: true
grammar_classy: true
grammar_cjkEmphasis: true
grammar_cjkRuby: true
grammar_center: true
grammar_align: true
grammar_tableExtra: true
---

[toc]

#### 简介

不管你们知不知道以太坊（Ethereum blockchain）是什么，但是你们大概都听说过以太坊。最近在新闻里出现过很多次，包括一些专业杂志的封面，但是如果你们对以太坊到底是什么没有一个基本的了解的话，看这些文章就会感觉跟看天书一样。 所以，什么是以太坊？本质上，就是一个保存数字交易永久记录的公共数据库。重要的是，这个数据库不需要任何中央权威机构来维持和保护它。相反的它以一个“无信任”的交易系统来运行—一个个体在不需要信任任何第三方或对方的情况下进行点对点交易的架构。

依然感到很困惑？这就是这篇文章存在的理由。我的目标是在技术层面来解释以太坊的工作原理，但是不会出现很复杂的数学问题或看起来很可怕的公式。即使你不是一个程序员，我希望你看完之后最起码对技术有个更好的认识。如果有些部分技术性太强不好理解，这是非常正常的，真的没有必要完全理解每一个小细节。我建议只要宏观的理解一下事物就行了。
这篇文章中的很多议点都是以太坊黄皮书中讨论过的概念的细分。我添加了我自己的解释和图表使理解以太坊更加简单一点。那些足够勇敢的人可以挑战一下技术，去阅读一下以太坊的黄皮书。

##### 区块链定义

区块链就是一个具有共享状态的密码性安全交易的单机(cryptographically secure transactional singleton machine with shared-state)。

这有点长，是吧？让我们将它分开来看：
1. “密码性安全(Cryptographically secure)”是指用一个很难被解开的复杂数学机制算法来保证数字货币生产的安全性。将它想象成类似于防火墙的这种。它们使得欺骗系统近乎是一个不可能的事情（比如：构造一笔假的交易，消除一笔交易等等）。

2. “交易的单机(Transactional singleton machine)”是指只有一个权威的机器实例为系统中产生的交易负责任。换句话说，只有一个全球真相是大家所相信的。

3. “具有共享状态(With shared-state)”是指在这台机器上存储的状态是共享的，对每个人都是开放的。
以太坊实现了区块链的这个范例。

##### 以太坊模型

以太坊的本质就是一个基于交易的状态机(transaction-based state machine)。在计算机科学中，一个 状态机 是指可以读取一系列的输入，然后根据这些输入，会转换成一个新的状态出来的东西。

根据以太坊的状态机，我们从创世纪状态(genesis state)开始。这差不多类似于一片空白的石板，在网络中还没有任何交易的产生状态。当交易被执行后，这个创世纪状态就会转变成最终状态。在任何时刻，这个最终状态都代表着以太坊当前的状态。

以太坊的状态有百万个交易。这些交易都被“组团”到一个区块中。一个区块包含了一系列的交易，每个区块都与它的前一个区块链接起来。

为了让一个状态转换成下一个状态，交易必须是有效的。为了让一个交易被认为是有效的，它必须要经过一个验证过程，此过程也就是挖矿。挖矿就是一组节点（即电脑）用它们的计算资源来创建一个包含有效交易的区块出来。
任何在网络上宣称自己是矿工的节点都可以尝试创建和验证区块。世界各地的很多矿工都在同一时间创建和验证区块。每个矿工在提交一个区块到区块链上的时候都会提供一个数学机制的“证明”，这个证明就像一个保证：如果这个证明存在，那么这个区块一定是有效的。

为了让一个区块添加到主链上，一个矿工必须要比其他矿工更快的提供出这个“证明”。通过矿工提供的一个数学机制的“证明”来证实每个区块的过程称之为工作量证明(proof of work)。

证实了一个新区块的矿工都会被奖励一定价值的奖赏。奖赏是什么？以太坊使用一种内在数字代币—以太币(Ether)作为奖赏。每次矿工证明了一个新区块，那么就会产生一个新的以太币并被奖励给矿工。

你也许会在想：什么能确保每个人都只在区块的同一条链上呢？我们怎么能确定不会存在一部分矿工创建一个他们自己的链呢？
前面，我们定义了区块链就是一个具有共享状态的交易单机。使用这个定义，我们可以知道正确的当前状态是一个全球真相，所有人都必须要接受它。拥有多个状态（或多个链）会摧毁这个系统，因为它在哪个是正确状态的问题上不可能得到统一结果。如果链分叉了，你有可能在一条链上拥有10个币，一条链上拥有20个币，另一条链上拥有40个币。在这种场景下，是没有办法确定哪个链才是最”有效的“。

不论什么时候只要多个路径产生了，一个”分叉“就会出现。我们通常都想避免分叉，因为它们会破坏系统，强制人们去选择哪条链是他们相信的链。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108774.png)

为了确定哪个路径才是最有效的以及防止多条链的产生，以太坊使用了一个叫做“GHOST协议(GHOST protocol.)”的数学机制。

==GHOST = Greedy Heaviest Observed Subtree== 

简单来说，GHOST协议就是让我们必须选择一个在其上完成计算最多的路径。一个方法确定路径就是使用最近一个区块（叶子区块）的区块号，区块号代表着当前路径上总的区块数（不包含创世纪区块）。区块号越大，路径就会越长，就说明越多的挖矿算力被消耗在此路径上以达到叶子区块。使用这种推理就可以允许我们赞同当前状态的权威版本。

##### 以太坊系统主要组成部分

现在你大概对区块链是什么有个理性的认识，让我们在再深入了地解一下以太坊系统主要组成部分：
1. 账户(accounts)
2.  状态(state)
3.  损耗和费用(gas and fees)
4.  交易(transactions)
5.  区块(blocks)
6.  交易执行(transaction execution)
7.  挖矿(mining)
8.  工作量证明(proof of work)

**账户**

以太坊的全局“共享状态”是有很多小对象（账户）来组成的，这些账户可以通过消息传递架构来与对方进行交互。每个账户都有一个与之关联的状态(state)和一个20字节的地址(address)。在以太坊中一个地址是160位的标识符，用来识别账户的。
这是两种类型的账户：
- 外部拥有的账户，被私钥控制且没有任何代码与之关联
- 合约账户，被它们的合约代码控制且有代码与之关联

**外部拥有账户与合约账户的比较**
理解外部拥有账户和合约账户的基本区别是很重要的。一个外部拥有账户可以通过创建和用自己的私钥来对交易进行签名，来发送消息给另一个外部拥有账户或合约账户。在两个外部拥有账户之间传送的消息只是一个简单的价值转移。但是从外部拥有账户到合约账户的消息会激活合约账户的代码，允许它执行各种动作。（比如转移代币，写入内部存储，挖出一个新代币，执行一些运算，创建一个新的合约等等）。
不像外部拥有账户，合约账户不可以自己发起一个交易。相反，合约账户只有在接收到一个交易之后(从一个外部拥有账户或另一个合约账户接)，为了响应此交易而触发一个交易。我们将会在“交易和消息”部分来了解关于合约与合约之间的通信。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108775.png)

> 因此，在以太坊上任何的动作，总是被外部控制账户触发的交易所发动的。

**账户状态**
账户状态有四个组成部分，不论账户类型是什么，都存在这四个组成部分：
- nonce：如果账户是一个外部拥有账户，nonce代表从此账户地址发送的交易序号。如果账户是一个合约账户，nonce代表此账户创建的合约序号
- balance： 此地址拥有Wei的数量。1Ether=10^18Wei
- storageRoot： Merkle Patricia树的根节点Hash值（我们后面在解释Merkle树）。Merkle树会将此账户存储内容的Hash值进行编码，默认是空值
- codeHash：此账户EVM（以太坊虚拟机，后面细说）代码的hash值。对于合约账户，就是被Hash的代码并作为codeHash保存。对于外部拥有账户，codeHash域是一个空字符串的Hash值

**世界状态**

好了，我们知道了以太坊的全局状态就是由账户地址和账户状态的一个映射组成。这个映射被保存在一个叫做Merkle Patricia树的数据结构中

==Merkle Tree（也被叫做Merkle trie）== 是一种由一系列节点组成的二叉树，这些节点包括：
- 在树底的包含了源数据的大量叶子节点
- 一系列的中间的节点，这些节点是两个子节点的Hash值
- 一个根节点，同样是两个子节点的Hash值，代表着整棵树

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108782.png)

> 树底的数据是通过分开我们想要保存到chunks的数据产生的，然后将chunks分成buckets，再然后再获取每个bucket的hash值并一直重复直到最后只剩下一个Hash：根Hash。

这棵树要求存在里面的值（value）都有一个对应的key。从树的根节点开始，key会告诉你顺着哪个子节点可以获得对应的值，这个值存在叶子节点。在以太坊中，key/value是地址和与地址相关联的账户之间状态的映射，包括每个账户的balance, nonce, codeHash和storageRoot（storageRoot自己就是一颗树）。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108877.png)

同样的树结构也用来存储交易和收据。
更具体的说，每个块都有一个头(header)，保存了三个不同Merkle trie结构的根节点的Hash，包括：
- 状态树
- 交易树
- 收据树

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108889.png)

**节点类型**

在Merkle tries中存储所有信息的高效性在以太坊中的“轻客户端”和“轻节点”相当的有用。
记住区块链就是一群节点来维持的。广泛的说，有两种节点类型：全节点和轻节点。

全节点通过下载整条链来进行同步，从创世纪块到当前块，执行其中包含的所有交易。通常，矿工会存储全节点，因为他们在挖矿过程中需要全节点。也有可能下载一个全节点而不用执行所有的交易。无论如何，一个全节点包含了整个链。

不过除非一个节点需要执行所有的交易或轻松访问历史数据，不然没必要保存整条链。这就是轻节点概念的来源。比起下载和存储整个链以及执行其中所有的交易，轻节点仅仅下载链的头，从创世纪块到当前块的头，不执行任何的交易或检索任何相关联的状态。由于轻节点可以访问块的头，而头中包含了3个tries的Hash，所有轻节点依然可以很容易生成和接收关于交易、事件、余额等可验证的答案。

这个可以行的通是因为在Merkle树中hash值是向上传播的—如果一个恶意用户试图用一个假交易来交换Merkle树底的交易，这个会改变它上面节点的hash值，而它上面节点的值的改变也会导致上上一个节点Hash值的改变，以此类推，一直到树的根节点。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108893.png)

任何节点想要验证一些数据都可以通过Merkle证明来进行验证，Merkle 证明的组成：
- 一块需要验证的数据
- 树的根节点Hash
- 一个“分支”（从 chunk到根这个路径上所有的hash值）

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108894.png)

任何可以读取证明的人都可以验证分支的hash是连贯的，因此给出的块在树中实际的位置就是在此处。
总之，使用Merkle Patricia树的好处就是该结构的根节点加密取决于存储在树中的数据，而且根据点的hash还可以作为该数据的安全标识。由于块的头包含了状态、交易、收据树的根hash，所有任何节点都可以验证以太坊的一小部分状态而不用保存整个状态，这整个状态的的大小可能是非常大的。

**Gas和费用**

在以太坊中一个比较重要的概念就是费用(fees)，由以太坊网络上的交易而产生的每一次计算，都会产生费用—没有免费的午餐。这个费用是以称之为”gas”的来支付。

gas就是用来衡量在一个具体计算中要求的费用单位。gas price就是你愿意在每个gas上花费Ether的数量，以“gwei”进行衡量。“Wei”是Ether的最小单位，1Ether表示10^18Wei. 1gwei是1,000,000,000 Wei。

对每个交易，发送者设置gas limit和gas price。gas limit和gas price就代表着发送者愿意为执行交易支付的Wei的最大值。
例如，假设发送者设置gas limit为50,000，gas price为20gwei。

这就表示发送者愿意最多支付 `50,000*20gwei = 1,000,000,000,000,000 Wei = 0.001 Ether`来执行此交易。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108776.png)

记住gas limit代表用户愿意花费在gas上的钱的最大值。
如果在他们的账户余额中有足够的Ether来支付这个最大值费用，那么就没问题。
在交易结束时任何未使用的gas都会被返回给发送者，以原始费率兑换。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108891.png)

在发送者没有提供足够的gas来执行交易，那么交易执行就会出现“gas不足”然后被认为是无效的。在这种情况下，交易处理就会被终止以及所有已改变的状态将会被恢复，最后我们就又回到了交易之前的状态—完完全全的之前状态就像这笔交易从来没有发生。因为机器在耗尽gas之前还是为计算做出了努力，
所以理论上，将不会有任何的gas被返回给发送者。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108892.png)

这些gas的钱到底去了哪里？发送者在gas上花费的所有钱都发送给了“受益人”地址，通常情况下就是矿工的地址。因为矿工为了计算和验证交易做出了努力，所以矿工接收gas的费用作为奖励。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108895.png)

通常，发送者愿意支付更高的gas price，矿工从这笔交易总就能获得更多的价值。因此，矿工也就更加愿意选择这笔交易。这样的话，矿工可以自由的选择一笔交易自己愿意验证或忽略。为了引导发送者应该设置gas price为多少，矿工可以选择建议一个最小的gas值他们愿意执行一个交易。

==存储也有费用==
gas不仅仅是用来支付计算这一步的费用，而且也用来支付存储的费用。存储的总费用与所使用的32位字节的最小倍数成比例。
存储费用有一些比较细微的方面。比如，由于增加了的存储增加了所有节点上的以太坊状态数据库的大小，所以激励保持数据存储量小。为了这个原因，如果一个交易的执行有一步是清除一个存储实体，那么为执行这个操作的费用就会被放弃，并且由于释放存储空间的退款就会被返回给发送者。

**费用的作用是什么**

以太坊可以运作的一个重要方面就是每个网络执行的操作同时也被全节点所影响。然而，计算的操作在以太坊虚拟机上是非常昂贵的。因此，以太坊智能合约最好是用来执行最简单的任务，比如运行一个简单的业务逻辑或者验证签名和其他密码对象，而不是用于复杂的操作，比如文件存储，电子邮件，或机器学习，这些会给网络造成压力。施加费用防止用户使网络超负荷。

以太坊是一个图灵完备语言（短而言之，图灵机器就是一个可以模拟任何电脑算法的机器。对于图灵机器不太熟悉的人可以看看这个 和这个 ）。这就允许有循环，并使以太坊受到停机问题 的影响，这个问题让你无法确定程序是否无限制的运行。如果没有费用的话，恶意的执行者通过执行一个包含无限循环的交易就可以很容易的让网络瘫痪而不会产生任何反响。因此，费用保护网络不受蓄意攻击。

你也许会想，“为什么我们还需要为存储付费？”

其实就像计算一样，以太坊网络上的存储是整个网络都必须要负担的成本。

**交易和消息**

之前说过以太坊是一个基于交易的状态机。换句话说，在两个不同账户之间发生的交易才让以太坊全球状态从一个状态转换成另一个状态。

最基本的概念，一个交易就是被外部拥有账户生成的加密签名的一段指令，序列化，然后提交给区块链。

有两种类型的交易：消息通信和合约创建(也就是交易产生一个新的以太坊合约)。
不管什么类型的交易，都包含：
- nonce：发送者发送交易数的计数
- gasPrice：发送者愿意支付执行交易所需的每个gas的Wei数量
- gasLimit：发送者愿意为执行交易支付gas数量的最大值。这个数量被设置之后在任何计算完成之前就会被提前扣掉
- to：接收者的地址。在合约创建交易中，合约账户的地址还没有存在，所以值先空着
- value：从发送者转移到接收者的Wei数量。在合约创建交易中，value作为新建合约账户的开始余额
- v,r,s：用于产生标识交易发生着的签名
- init（只有在合约创建交易中存在）：用来初始化新合约账户的EVM代码片段。init值会执行一次，然后就会被丢弃。当init第一次执行的时候，它返回一个账户代码体，也就是永久与合约账户关联的一段代码。
- data（可选域，只有在消息通信中存在）：消息通话中的输入数据(也就是参数)。例如，如果智能合约就是一个域名注册服务，那么调用合约可能就会期待输入域例如域名和IP地址

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108896.png)

在这里我们学到交易—消息通信和合约创建交易两者都总是被外部拥有账户触发并提交到区块链的。换种思维思考就是，交易是外部世界和以太坊内部状态的桥梁。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108902.png)

但是这也并不代表一个合约与另一个合约无法通信。在以太坊状态全局范围内的合约可以与在相同范围内的合约进行通信。他们是通过“消息”或者“内部交易”进行通信的。我们可以认为消息或内部交易类似于交易，不过与交易有着最大的不同点—它们不是由外部拥有账户产生的。相反，他们是被合约产生的。它们是虚拟对象，与交易不同，没有被序列化而且只存在与以太坊执行环境。
当一个合约发送一个内部交易给另一个合约，存在于接收者合约账户相关联的代码就会被执行。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108897.png)

一个重要需要注意的事情是内部交易或者消息不包含gasLimit。因为gas limit是由原始交易的外部创建者决定的（也就是外部拥有账户）。外部拥有账户设置的gas limit必须要高到足够将交易完成，包括由于此交易而长生的任何”子执行”，例如合约到合约的消息。如果，在一个交易或者信息链中，其中一个消息执行使gas已不足，那么这个消息的执行会被还原，包括任何被此执行触发的子消息。不过，父执行没必要被还原。

**区块**

所有的交易都被组成一个”块”。一个区块链包含了一系列这样的链在一起区块。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108898.png)

注意每个区块是如何包含三个树结构的，三个树结构分别对应：
- 状态（stateRoot）
- 交易（transactionsRoot）
- 收据（receiptsRoot）
这三个树结构就是我们前面讨论的Merkle Patricia树。

**日志**

eventlog
以太坊允许日志可以跟踪各种交易和信息。一个合约可以通过定义“事件”来显示的生成日志。
一个日志的实体包含：
记录器的账户地址
代表本次交易执行的各种事件的一系列主题以及与这些事件相关的任何数据
日志被保存在bloom过滤器 中，过滤器高效的保存了无尽的日志数据

**交易收据**

receipt log
自于被包含在交易收据中的日志信息存储在头中。就像你在商店买东西时收到的收据一样，以太坊为每笔交易都产生一个收据。

像你期望的那样，每个收据包含关于交易的特定信息。这些收据包含着：
- 区块序号
- 区块Hash
- 交易Hash
- 当前交易使用了的gas
- 在当前交易执行完之后当前块使用的累计gas
- 执行当前交易时创建的日志
等等

**区块难度**

区块的难度是被用来在验证区块时加强一致性。创世纪区块的难度是131,072，有一个特殊的公式用来计算之后的每个块的难度。如果某个区块比前一个区块验证的更快，以太坊协议就会增加区块的难度。

----------------------

#### 以太坊的私钥存储文件

keystore文件是你独有的，用于签名交易的以太坊私钥的加密文件。一旦丢失文件或加密密码就意味着你失去了此地址发起交易、签名交易的特权，账户里面的资金将永远被锁。

keystore文件存在的价值就是以加密的方式存储密钥，同时在使用的时候只需要提供keystore文件和对应的密码即可发起交易。安全性与可用性达到了完美的平衡。

但是，我们需要注意的是一旦用密码对加密文件进行解锁之后，在有效时间内通一个客户端下，你可以发起交易，如果别人可以访问你的客户端，同样也可以发起交易。在网络安全不足的情况下，这是被盗币的场景之一。

##### 私钥文件的内容

秘钥文件为文本文件，可以使用任何文本编辑器或浏览器打开。
通过文件中的内容，我们能看到的是一个json字符串，里面包含了此秘钥对应的地址和加密相关的一些信息。

*   cipher：加密算法，对称加密，AES算法，用于加密以太坊私钥;
*   cipherparams：cipher算法需要的参数，参数iv，是aes-128-ctr加密算法需要的初始化向量;
*   ciphertext：加密后的密文，aes-128-ctr函数的加密输入密文；
*   kdf：秘钥生成函数，用于使用密码加密keystore文件；
*   kdfparams：kdf算法所需要的参数；
*   mac：验证密码的编码；

##### 加密私钥

一个以太坊账户是由一对公私钥对构成，并使用强对称算法（cipher）进行加密。
我们看一下具体的流程图 "ciphertex密文的对称解密"：

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108899.png)

> 客户端读取密钥文件和加密密码，对私钥进行解密，然后使用私钥对发送的交易进行签名。

##### 密码保护

以太坊使用基于密码保护的机制来解密密钥。这样用户就不需要记住一串非用户友好的密码。为了达到此效果，以太坊使用密钥生成函数，根据输入的密码和一系列参数就能计算解密密钥。这就涉及到kdf和kdfparams的用途：

*   kdf是一个密钥生成函数，根据密码计算（或者取回）解密密钥。kdf用的是scrypt算法。
*   kdfparams是scrypt函数需要的参数。更多的参数可以参考：[https://tools.ietf.org/html/rfc7914](https://tools.ietf.org/html/rfc7914)

用kdfparams参数对scrypt函数进行调整，反馈密码中，得到解密密钥，也就是密钥生成函数的输出。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108903.png)

##### 错误的密码

当输入错误密码时，密码派生和解密等操作都会成功，但最终计算所得的以太坊私钥不是正确的，因此无法进行解锁账户的操作。

keystore文件中mac值起作用的地方。在密钥生成函数执行之后，它的输出（解密密钥）和ciphertext密文就被处理，并且和mac（类似于数据签名）作比较。如果结果和mac相同，那么密码就是正确的，可以开始解密操作。

在和mac进行比较之前，需要解密密钥（左起第二字节开始的16字节）要和ciphertext 密文连接在一起，并进行哈希散列（用SHA3-256的方法）。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108904.png)

##### 整个流程

输入密码
密码作为kdf密钥生成函数的输入
计算解密密钥
用解密密钥和ciphertext密文连接并进行处理
和mac比较确保密码正确
最后，通过cipher对称函数用解密密钥对ciphertext 密文解密。

![](https://raw.githubusercontent.com/OliverRen/olili_blog_img/master/Ethereum/2020811/1597124108905.png)

-----------------------

#### 以太坊的交易流程

- 以太坊的交易业务逻辑是有规范的,但是在不同的客户端中有不同的实现
- 根据客户端运行的模式也会有不同的执行方式

这里使用 geth v1.9.0 stable的客户端,运行全节点模式来进行阐述

##### 交易流程的整体流程

- 发起交易：设定 `from,to,value,gas,gaslimit,nonce`等参数生成交易
- 交易签名：使用账户私钥对交易进行签名
- 提交交易：把交易加入到交易池`txpool`中
- 广播交易：把交易信息广播给其他结点
- 处理交易：矿工取交易，`EVM`执行，改变状态即打包成区块

##### 结合代码来看的整个流程

###### 前端发起交易
使用cli或者相应的ui客户端组装用户的交易意图

###### 节点接受到交易 `internal/ethapi/api.go`
*  `PublicTransactionPoolAPI.SendTransaction`,根据参数创建交易,签名,`submitTransaction`提交交易
*  `PublicTransactionPoolAPI.SendRawTransaction`,解码已签名交易,`submitTransaction`提交交易
*  `PrivateAccountAPI.SendTransaction`,根据参数创建签名交易,`submitTransaction`提交交易
*  `submitTransaction`,调用后端发送交易方法`Backend.SendTx`

###### 节点异步处理请求 `eth/api_backend.go`
* `Backend.SendTx`,调用交易池添加交易到本地 `EthAPIBackend.eth.txPool.AddLocal(signedTx)`

###### 交易池操作 `core/tx_pool.go`

> TxPool 包含 `pending` 和 `queue`两个交易队列,类型为 `map[common.Address,txList]`,即以address地址为key的一个map
> pending:当前可执行交易队列
> queue:当前不可执行交易队列
> 衍生到btc中可以参考 mempool 是相同的一个东西

1. **TxPool.AddLocal**,调用**TxPool.addTx**将交易加入交易池. (除AddLocal还有**AddRemote**,内部都调用**TxPool.addTx**,如果是local交易会写入本地磁盘日志中,在节点重启时加载恢复,在一些过滤操作中保留的优先级高)

2. **TxPool.addTx**内部调用**TxPool.add**,add方法进行一系列验证后将交易加入queue,用于后续提升至pending中去执行,具体逻辑包括：
		2.1 通过交易哈希验证是未知交易,如果交易池已包含该交易,return
		2.2 TxPool.validateTx交易有效验证,验证不通过,return
		2.3 判断交易池已满时,判断如果交易手续费比当前交易池中手续费最低的交易还低,return,否则,移除一些交易以腾出空间
		2.4 判断交易池pending中包含相同from和nonce的交易时,比较gasPrice大于旧交易gasPrice且大于`threshold`(门槛),则替换并协程发送事件进行广播 `go TxPool.txFeed.Send(NewTxsEvent{types.Transactions{tx}})`,否则return
		2.5 不是以上两种替换交易池中已有交易的情况,TxPool.enqueueTx将交易插入queue
		2.6 判断如果是local交易,记录并将交易写入本地磁盘日志中
		
3. **TxPool.add**方法返回是否有替换交易(replace bool),如果为false,不是替换,仅仅是添加一个新的交易,执行参数为from的**TxPool.promoteExecutables**

4. **TxPool.promoteExecutables**方法把queue中变得可执行的交易转移到pending中,并删除所有无效交易,具体逻辑包括：
		4.1 创建临时变量交易列表promoted
		4.2 判断参数accounts(类型\[]common.Address)是否为空,如果为空则赋值为queue中所有地址
		4.3 遍历accounts,取出key为addr的list,即from为addr的交易列表,在循环中：
				4.3.1 丢弃nonce比当前账户nonce低的交易
				4.3.2 丢弃交易花费超过账户余额和gas使用超出当前交易池可用gas的交易
				4.3.3 根据`TxPool.pendingState`的nonce值取出所有可执行的交易,执行**TxPool.promoteTx**将交易插入pending,如果插入成功则把交易加入到promoted (即如果交易可以执行 直接在promoted,如果不是,则需要他调用promoteTx从queue中提起再插入pending,再加入到 promoted)
				4.3.4 如果addr不是本地账户,如果列表大小超过交易池中每个账户最多不可执行交易数量(默认64),丢弃
				4.3.5 如果列表已经为空,删除queue中addr这个key
		4.4 判断如果promoted大小大于0,协程发送事件进行广播 `go pool.txFeed.Send(NewTxsEvent{promoted})`
		4.5 判断如果pending中交易数量超出限制(4096),做平衡操作：创建集合记录交易数量超出限制的非本地账户,丢弃pending中这些账户下的部分交易直到数量不超过限制,更新TxPool.pendingState
		4.6 判断如果queue中交易数量超出限制(1024),取出非本地账户交易,根据心跳排序,丢弃交易直到数量不超过限制
		
5. 扩展,有`TxPool.promoteExecutables`还有**TxPool.demoteUnexecutables**,具体逻辑：
		5.1 调用时机：在reset中调用,reset方法在NewTxPool和TxPool.loop中收到ChainHeadEvent时调用,在矿工worker.resultLoop收到resultCh和BlockChain.InsertChain后会PostChainEvents
		5.2 遍历pending,得到addr下交易列表:
				5.2.1 丢弃nonce比当前账户nonce低的交易
				5.2.2 丢弃交易花费超过账户余额和gas使用超出当前交易池可用gas的交易,这些移除的交易最小的nonce为lowest,列表中nonce大于lowest的交易移除并加入临时列表invalids返回
				5.2.3 遍历invalids,调用TxPool.enqueueTx插入queue
				5.2.4 判断如果当前列表中找不到addr当前nonce对应的交易,从pending中移除列表中所有交易,调用TxPool.enqueueTx插入queue
				5.2.5 pending和beats的key该删除的删除
				
6. 当有新交易插入 pending 时,广播 `NewTxsEvent`,**SubscribeNewTxsEvent**方法用于监听到`NewTxsEvent`,调用时机:
		6.1 `ethstats/ethstats.go: Start`方法中开启loop协程,在该协程中订阅并处理,主要是通知交易事件,并在时间上过滤避免过于频繁的事件处理
		6.2 `eth/filters/filter_system.go`
		6.3 `eth/handler.go: ProtocolManager.Start`方法中订阅(该方法会在节点启动时调用),go pm.txBroadcastLoop()开启协程处理,当收到NewTxsEvent,调用ProtocolManager.BroadcastTxs方法广播交易到其他所有没有该交易的节点
		6.4 `miner/worker.go: newWorker`方法中订阅,并开启了协程来处理,当收到NewTxsEvent
				6.4.1 判断如果节点不在挖矿,这里会立即调用worker.commitTransactions方法处理并更新快照,其中worker.commitTransactions方法核心逻辑是调用core.ApplyTransaction处理交易
				6.4.2 判断如果节点在挖矿,不处理

7. **core/state_processor.go**
		ApplyTransaction方法,将Transaction转化为Message,创建evm,调用core/state_transition.go ApplyMessage执行Message,执行成功后更新状态,创建交易回执并返回
		
8. **core/state_transition.go**
		ApplyMessage会创建一个StateTransition对象并调用其TransitionDb方法,该方法让虚拟机evm处理交易数据(创建合约或普通交易),并更新nonce,balance等状态

> 在core/tx_list.go Add方法中如何计算threshold(门槛)
old.gasprice(100+priceBump)/100=threshold阙值
priceBump默认为10
即每次bumpfee增加的gasprice最少时1.1倍

-----------------------

#### 如何正确处理以太坊交易的Nonce

###### 什么时Nonce
官方文档对此参数的解释是：整数类型，允许使用相同随机数覆盖自己发送的处于pending状态的交易。

仅从官网的解释，我们无法获取到更多的有效的信息。但在真实生成中我们会发现如果传错nonce字段值，通过RPC接口调用发送的交易很大可能将不会被确认。

如果通过console命令来操作一般不会出现此问题，因为节点已经帮我们处理了。

###### Nonce错误引发的问题

如果继续追踪问题，会发现nonce传递错误的交易可以通过`eth_getTransaction`查询得到相关信息，但是它的blocknumber始终为null，也就说这边交易始终未被确认。如果是在dev模式下，应该是很快就会被确认的。更进一步，通过`txpool.content`命令，会发现那笔交易一直处于queued队列中，而未被消费。(需要节点打开txpool的api)

###### 原因解析

为了防止交易重播，ETH（ETC）节点要求每笔交易必须有一个nonce数值。
每一个账户从同一个节点发起交易时，这个nonce值从0开始计数，发送一笔nonce对应加1。
当前面的nonce处理完成之后才会处理后面的nonce。
注意这里的前提条件是相同的地址在相同的节点发送交易。 

###### 以下是nonce使用的几条规则： 
- 当nonce太小（小于之前已经有交易使用的nonce值），交易会被直接拒绝。 
- 当nonce太大，交易会一直处于队列之中，这也就是导致我们上面描述的问题的原因； 
- 当发送一个比较大的nonce值，然后补齐开始nonce到那个值之间的nonce，那么交易依旧可以被执行。 
- 当交易处于queue中时停止geth客户端，那么交易queue中的交易会被清除掉。

###### 获取nonce值
经过上面的解释追踪，我们已经了解到了nonce的基本使用规则。那么，在实际应该用中我们如何保障nonce值的可靠性呢？

这里有两个思路:
第一个思路就是由业务系统维护nonce值的递增。如果交易发送就出现问题，那么该地址下一笔交易继续使用这个nonce进行发送交易。
第二个思路就是使用现有的api查询当前地址已经发送交易的nonce值，然后对其加1，再发送交易。

对应的API接口为：`eth_getTransactionCount`
此方法由两个参数:
第一个参数为需要查询nonce的地址
第二个参数为block的状态：latest、earliest和pending。
一般情况使用pending就可以查询获得最新已使用的nonce。其他状态大家可以自行验证。

-----------------------

#### ERC20

提到ERC20首先解释一下什么叫做ERC.
> ERC的定义及标准列表
ERC代表“Etuereum Request for Comment"，这是Ethereum版的意见征求稿 （RFC），RFC是由互联网工程任务组制定的一个概念。 RFC中的备忘录包含技术和组织注意事项。 对于ERC，意见征求稿中包括一些关于以太坊网络建设的技术指导。

> ERC是Ethereum开发者为以太坊社区编写的。 因此，ERC的创建流程中包括开发人员。 为了创建一个以太坊平台的标准，开发人员应当提交了一个以太坊改进方案（EIP）， 改进方案中包括协议规范和合约标准。 一旦EIP被委员会批准并最终确定，它就成为ERC。 EIP的完整列表可以在 [Github](https://github.com/ethereum/EIPs) 找到

> - 草稿（Draft）	处于打开状态，便于考察讨论；
> - 接受（Accepted）	即将被接受，例如将包含在下一个硬分叉中；
> - 定稿（Final）	在上一个硬分叉中被接受，已定稿；
> - 延期（Deferred）	不会马上被接受，但也许在将来的硬分叉版本会考虑。

##### ERC20接口标准

ERC20相关ERC包括: ERC20、ERC223、ERC621、ERC827

当要实现一个满足 ERC-20 接口标准的 Token 智能合约时，该合约必须满足以下内容实现。
```
contract ERC20{
    //总共要发多少币   
    function totalSupply() constant returns (uint totalSupply); 
    //返回当前指定地址的余额
    function balanceOf(address _owner) constant returns (uint balance); 
    //调用transfer 将自己的token 转移 到 _to 地址  _value 为转账到数量
    function transfer(address _to, uint _value) returns (bool success); 
    //与_approve 函数配合使用, _approve 批准之后，调用transerFrom 转移token
    function transferFrom(address _from, address _to, uint _value) returns (bool success); 
    // 授权_spender 可以从 自己的账户转移的余额，可以分多次转移.
    function approve(address _spender, uint _value) returns (bool success);
    // 返回spender 还能提取的token 数量.
    function allowance(address _owner, address _spender) constant returns (uint remaining); 
    // 当token 转移之后会触发事件
    event Transfer(address indexed _from, address indexed _to, uint _value); 
     //当任何的approve 被触发之后，都会调用此函数.                  .
    event Approval(address indexed _owner, address indexed _spender, uint _value);
}
```
#### ERC721

##### ERC721接口标准

ERC721是针对不可置换Token的智能合约标准接口，(non-fungiletokens)不可置换Token简称NFTs

```
contract ERC721{
    //发行代币的总量
    function totalSupply() public view returns (uint256 total);
    //根据指定的地址返回代币的数量
    function balanceOf(address _owner) public view returns (uint256 balance);
    //根据指定的tokenId 返回 当前拥有者
    function ownerOf(uint256 _tokenId) external view returns (address owner);
    //当前用户是否有转移代币的权力.
    function approve(address _to, uint256 _tokenId) external;
    //tokenid 资产转移。
    function transfer(address _to, uint256 _tokenId) external;
    //将指定的tokenid 从 _from 转移 到 _to
    function transferFrom(address _from, address _to, uint256 _tokenId) external;
    event Transfer(address from, address to, uint256 tokenId);
    event Approval(address owner, address approved, uint256 tokenId);
}
```

#### 比较ERC20和ERC721标准的区别

首先且先说ERC20,他是基于同质化的代币，是可置换的，意味着所有的Token直接没有区别，、所有Token都是一样的，我有两个ERC20的Token，并不会因为我花的方式不一样而不一样。

然而ERC721 的代币是基于是非同质化的，不可互换的Token，简单理解为每个Token都是独一无二的。也就是说ERC721的每个Token都拥有独立唯一的tokenId编号。像在CryptoKitties中的猫都被赋予拥有基因，每只猫的基因都是不一样的.

--------------------------

#### 以太坊的ABI

##### ABI是什么

ABI全称 Application Binary Interface，字面意思是应用程序二进制接口，可以通俗的理解为合约的接口说明，当合约被编译后，它对应的abi也就确定了。

abi有点类似于程序中的接口文档，描述了字段名称、字段类型、方法名称、参数名称、参数类型、方法返回值类型等

##### 为什么需要ABI

我们编写智能合约的流程是：

*   编写合约代码（一般使用solidity语言）
*   编译合约，将solidity编写的代码编译成EVM可识别的bytecode，这一步生成abi
*   部署合约，将合约部署到区块链上，生成合约地址，将合约内容（即上一步生成的bytecode）作为input date输入。部署合约是一个交易过程，所以也会生成一个交易Has
*   执行合约，获取合约地址，然后传入参数调用合约中的方法，获得执行结果

从上面的步骤可以看出，abi对于EVM来说，其实是不需要的。但是对于调用者来说，就需要知道合约有哪些方法，方法的参数是什么，返回值是什么，而这些信息就记录在智能合约的abi中。所以abi其实就相当于开发者的接口文档，方便开发者调用执行合约

##### ABI的内容

我们使用solidity编写一个最简单的合约

``` solidity
pragma solidity ^0.4.24;

contract Demo {

    uint private x;

    function set(uint _x) public {
        x = _x;
    }
}
```

使用 truffle comple 执行编译,就可以生成 json文件了

``` json
{
  "contractName": "Demo",
  "abi": [
    {
      "constant": false,
      "inputs": [
        {
          "name": "_x",
          "type": "uint256"
        }
      ],
      "name": "set",
      "outputs": [],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    }
  ],
  "bytecode": "0x6080604052348015600f57600080fd5b5060a48061001e6000396000f300608060405260043610603f576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff16806360fe47b1146044575b600080fd5b348015604f57600080fd5b50606c60048036038101908080359060200190929190505050606e565b005b80600081905550505600a165627a7a723058201dfe7c019fec67ccd87250c9ac8642c163cc5f43588715b33e8a8953df3715f60029",
  "deployedBytecode": "0x608060405260043610603f576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff16806360fe47b1146044575b600080fd5b348015604f57600080fd5b50606c60048036038101908080359060200190929190505050606e565b005b80600081905550505600a165627a7a723058201dfe7c019fec67ccd87250c9ac8642c163cc5f43588715b33e8a8953df3715f60029",
  "sourceMap": "27:97:1:-;;;;8:9:-1;5:2;;;30:1;27;20:12;5:2;27:97:1;;;;;;;",
  "deployedSourceMap": "27:97:1:-;;;;;;;;;;;;;;;;;;;;;;;;69:52;;8:9:-1;5:2;;;30:1;27;20:12;5:2;69:52:1;;;;;;;;;;;;;;;;;;;;;;;;;;;112:2;108:1;:6;;;;69:52;:::o",
  "source": "pragma solidity ^0.4.24;\n\n\ncontract Demo {\n\n    uint private x;\n\n    function set(uint _x) public {\n        x = _x;\n    }\n\n}\n",
  "sourcePath": "/Users/root/Workspace/DApp/demo/contracts/Demo.sol",
  "ast": {
    ...
  },
  "legacyAST": {
    ...
  },
  "compiler": {
    "name": "solc",
    "version": "0.4.24+commit.e67f0147.Emscripten.clang"
  },
  "networks": {},
  "schemaVersion": "2.0.1",
  "updatedAt": "2018-09-14T11:57:49.750Z"
}
```

*   name：函数名称
*   type：方法类型，包括function, constructor, fallback(缺省方法)可以缺省，默认为function
*   constant：布尔值，如果为true指明方法不会修改合约字段的状态变量
*   payable：布尔值，标明方法是否可以接收ether
*   stateMutability：状态类型，包括pure (不读取区块链状态)，view (和constant类型，只能查看，不会修改合约字段)，nonpayable（和payable含义一样），payable（和payable含义一样）。其实保留payable和constant是为了向后兼容
*   inputs：数组，描述参数的名称和类型
		*   name：参数名称
		*   type：参数类型
*   outputs：和inputs一样，如果没有返回值，缺省是一个空数组

##### 调用指定的函数

我们通过对ABI的了解知道了合约的函数定义, 但是只有函数定义也是不行的，我们还需要调用，当调用一个函数时也需要对该函数进行编码，这样EVM才能执行，那么以太坊是如何生成可供EVM调用的字节码的呢?

生成的字节码主要分两部分：
- 函数选择器
- 参数编码

**函数选择器**
即函数编码，对函数名称+参数类型进行sha3（keccak256）哈希运算之后，取前4个字节
函数编码占用了4个字节，所以参数编码从第五位开始

**参数编码**

由于函数编码占用了4个字节，所以参数编码从第五位开始
参数的编码根据类型的不同，编码方式也有所区别。主要分为固定类型和动态类型
1. 固定类型
uint：M为integer类型代表M bits,0 < M <= 256 , M % 8 == 0，如uint32，uint8,  uint256。
int：同上。同为从8到256位的无符号整数。
uint和int：整型，分别是uint256和int256的别名。注意: 函数参数类型是uint，转sha3码时要变成uint256。
address：地址，20个字节，160bits。
bool：布尔类型，1个字节，true:1，false:0。高位补0
bytes：固定大小的字节数组，0<M<=32,byte都是bytes1的别名。

2. 动态类型
bytes：动态分配大小字节数组。不是一个值类型!
string：动态大小UTF8编码的字符串,不是一个值类型!
T\[] 某个类型的不定长数组
T\[k] 某个类型的定长数组

固定类型的编码就很简单，直接将参数值转成32字节长度的16进制即可。
但是有区别的是：不足32bytes时，数字类型，如果是正数高位补0，如果是负数高位补1，布尔类型高位补0，字节类型、字符串类型在低位补全

这里大体将的是将外部的参数转换为字节数组,或者是转换为字符串,然后需要使用RLP编码转换为最终传入以太坊交易的data二进制数据.

-------------------------

#### RLP编码和解码

以太坊中调用合约的参数是使用RLP进行编码的.

RLP (Recursive Length Prefix，递归的长度前缀)
是一种编码规则，可用于编码任意嵌套的二进制数组数据。
RLP编码的结果也是二进制序列。
RLP主要用来序列化/反序列化数据。

##### RLP数据定义

RLP编码的定义只处理以下两类数据：

*   字符串（string）是指字节数组。
		例如，空串""，再如单词"cat"，以及句子"aaa bbb"等.
*   列表（list）是一个可嵌套结构，里面可包含字符串和列表。
		例如，空列表\[]，再如一个包含两个字符串的列表\["cat","dog"]
		再比如嵌套列表的复杂列表\["cat", \["puppy", "cow"], "horse", \[\[]], "pig", \[""], "sheep"]。

其他类型的数据需要转成以上的两类数据，才能编码。转换的规则RLP编码不统一规定，可以自定义转换规则。
		例如struct可以转成列表，int可以转成二进制序列（属于字符串这一类, 必须去掉首部0，必须用大端模式表示）。
		
从上面的数据类型定义中可以看出，RLP编码的数据是可嵌套的。
从RLP编码的名字可以看出，RLP编码是递归的，这一点从下面的规则和代码可以看出。

##### RLP编码规则

* RLP编码的重点是给数据前面添加一个字节的前缀，而这个前缀是和**数据的长度**相关的。
* RLP编码中的长度是数据的实际存储空间的字节大小，去掉首位0的正整数，用**大端模式**表示的二进制格式表示。
* RLP编码规定数据（字符串或列表）的长度的长度不得大于**8字节**。因为超过8字节后，一个字节的前缀就不能存储了。

1. 如果字符串的长度是1个字节，并且它的值在\[0x00, 0x7f] 范围之间，那么其RLP编码就是字符串本身。即前缀为空，用前缀代表字符串本身；0-127的数字

2. 否则，如果一个字符串的长度是0-55字节，其RLP编码是前缀跟上(拼接)字符串本身，前缀的值是**0x80加上字符串的长度**。由于在该规则下，字符串的最大长度是55,因此前缀的最大值是0x80+55=0x80+0x37=0xb7，所以在本规则下前缀(第一个字节)的取值范围是\[0x80, 0xb7],10进制的话是\[128,183]；

3. 如果字符串的长度大于55个字节，其RLP编码是前缀跟上字符串的长度再跟上字符串本身。前缀的值是0xb7加上字符串长度的二进制形式的字节长度（即字符串长度的存储长度）。即用额外的空间存储字符串的长度，而前缀中只存字符串的长度的长度。例如一个长度是1024的字符串，字符串长度(0x400)的二进制形式是 \x04 \x00，因此字符串长度的长度是2个字节，所以前缀应该是0xb7+2=0xb9，由此得到该字符串的RLP编码是\xb9\x04\x00再跟上字符串本身。因为字符串长度的长度最少需要1个字节存储，因此前缀的最小值是0xb7+1=0xb8；又由于长度的最大值是8个字节，因此前缀的最大值是0xb7+8=0xbf，因此在本规则下前缀的取值范围是\[0xb8, 0xbf],10进制的话是\[184,191]；

> 以上3个规则是针对字符串的，接下来的两个规则针对列表的。

4. 由于列表的任意嵌套的，因此列表的编码是递归的，先编码最里层列表，再逐步往外层列表编码。如果一个列表的总长度（payload，列表的所有项经过编码后拼接在一起的字节大小）是0-55字节，其RLP编码是前缀依次跟上列表中各项的RLP编码。前缀的值是0xc0加上列表的总长度。即0xc0+55=0xc0+0x37=0xf7 在本规则下前缀的取值范围是\[0xc0, 0xf7],10进制则是\[192,247]。本规则与规则2类似；

5. 如果一个列表的总长度大于55字节，它的RLP编码是前缀跟上列表的长度再依次跟上列表中各元素项的RLP编码。前缀的值是0xf7加上列表总长度的长度。编码的第一个字节的取值范围是\[0xf8, 0xff]。本规则与规则3类似；

##### RLP编码示例

*   整数 0(‘\x00’) = \[0x00] （规则一）
*   整数 1024(‘\x04\00’) = \[0x82, 0x04, 0x00] （规则二）
*   空字符串(‘null’) = 0x80 （规则二）
*   字符串 “dog” = \[0x83, ‘d’, ‘o’, ‘g’ ] （规则二）
*   字符串 “Lorem ipsum dolor sit amet, consectetur adipisicing elit” = \[0xb8, 0x38, ‘L’, ‘o’, ‘r’, ‘e’, ‘m’, ’ ‘, … , ‘e’, ‘l’, ‘i’, ‘t’] （规则三）
*   空列表 \[] = \[0xc0] （规则四）
*   列表 \[“cat”,”dog”] = \[0xc8, 0x83, ‘c’, ‘a’, ‘t’, 0x83, ‘d’, ‘o’, ‘g’ ] （规则四）
*   嵌套列表 \[ \[], \[\[]], \[ \[], \[\[]] ] ] = \[0xc7, 0xc0, 0xc1, 0xc0, 0xc3, 0xc0, 0xc1, 0xc0] （规则四）

##### RLP解码规则

根据RLP编码规则和过程，RLP解码的输入一律视为二进制字符数组，其过程如下：

1.  根据输入首字节数据，解码数据类型、实际数据长度和位置；
2.  根据类型和实际数据，解码不同类型的数据；
3.  继续解码剩余的数据；

其中，解码数据类型、实际数据类型和位置的规则如下：

1.  如果首字节(prefix)的值在\[0x00, 0x7f]范围之间，那么该数据是字符串，且字符串就是首字节本身；
2.  如果首字节的值在\[0x80, 0xb7]范围之间，那么该数据是字符串，且字符串的长度等于首字节减去0x80，且字符串位于首字节之后；
3.  如果首字节的值在\[0xb8, 0xbf]范围之间，那么该数据是字符串，且字符串的长度的字节长度等于首字节减去0xb7，数据的长度位于首字节之后，且字符串位于数据的长度之后；
4.  如果首字节的值在\[0xc0, 0xf7]范围之间，那么该数据是列表，在这种情况下，需要对列表各项的数据进行递归解码。列表的总长度（列表各项编码后的长度之和）等于首字节减去0xc0，且列表各项位于首字节之后；
5.  如果首字节的值在\[0xf8, 0xff]范围之间，那么该数据为列表，列表的总长度的字节长度等于首字节减去0xf7，列表的总长度位于首字节之后，且列表各项位于列表的总长度之后；
