常见 Java 异常解释：（译者注：非技术角度分析。阅读有风险，理解需谨慎o(╯□╰)o）

##java.lang
- ArithmeticException	
	- 你正在试图使用电脑解决一个自己解决不了的数学问题，请重新阅读你的算术表达式并再次尝试。
- ArrayIndexOutOfBoundsException	
	- 请查看 IndexOutOfBoundsException。不同之处在于这个异常越界的元素不止一个。
- ArrayStoreException	
	- 你已用光了所有数组，需要从数组商店中购买更多的数组。
- ClassCastException	
	- 你需要呆在自己出生的种姓或阶级。Java 不会允许达利特人表现得像刹帝利或者高贵种族的人假装成为工人阶级。为了保持向前兼容，Java 1.0中把Caste误写为Cast保留到了现在。
- ClassNotFoundException	
	- 你似乎创造了自己的类。这也是目前 Java 还未实现的种姓制度，但是 Java 明显使用了巴厘岛的种姓制度。也就是说，如果你是一个武士，也就相当于印度种姓制度中的第三层——吠舍。
- CloneNotSupportedException	
	- 你是一名克隆人。找到你的原型，告诉他你想做什么，然后自杀。
- IllegalAccessException	
	- 你是一个正在运行 Java 程序入室盗窃的小偷，请结束对电脑的盗窃行为，离开房子，然后再试一次。
- IllegalArgumentException	
	- 你试图反对之前的异常。
- IllegalMonitorStateException	
	- 请打开你的电脑屏幕背面。
- IllegalStateException	
	- 你来自一个尚未被联合国承认的国家，也许是库尔德斯坦或者巴勒斯坦。拿到真正的国籍后重新编译你的 Java 代码，然后再试一次。
- IllegalThreadStateException	
	- 你电脑的一颗螺丝上到了错误的螺纹孔里，请联系你的硬盘供应商。
- IndexOutOfBoundsException	
	- 你把食指放在了无法接收的地方，重新放置，再试一次。
- InstantiationException	
	- 不是每件事都会立即发生，请更耐心一点。
- InterruptedException	
	- 告诉你的同事、室友等，当你工作的时候，请勿打扰。
- NegativeArraySizeException	
	- 你创建了一个负数长度的数组。这会丢失信息，长期发展将会毁灭宇宙。不过放宽心，Java 发现了你正在做的事，不要再这么干了。
- NoSuchFieldException	
	- 你正试图去一个不存在的区域游览。如果你试图去参观一个事实上不存在，其实已经是最高机密的飞机场时，也会得到这个异常。我可以给你示例，然后不得不杀了你。
- NoSuchMethodException	
	- 不要使用那个方法！拜托了，就像我们一直做的那样去解决事情吧。
- NullPointerException	
	- 你没有狗。请你先找一只狗，比如一只布烈塔尼獵犬，然后再试一次。
- NumberFormatException	
	- 你正在使用过时的测量单位，比如英寸或者品脱。请转换成国际基本单位。有一个已知的 bug 会导致 Java 抛出这个异常，那就是你太矮了或者太高了。
- RuntimeException	
	- 你不能跑得足够快，可能因为你太胖了。关掉你的电脑，出门锻炼吧。
- SecurityException	
	- 你已被认为是国家安全的一个威胁。请你呆在原地别动，然后等着警察来并带你走。
- StringIndexOutOfBoundsException	
	- 你的内裤和这个地方格格不入。换掉它们，再试一次。另外如果你根本不穿任何内裤，也会得到这个异常。
- UnsupportedOperationException	
	- 因为一些原因，你正试图做一个在道德上不被 Java 支持的手术。包括不必要的截肢，例如割包皮。请停止滥用你的身体，不要移除你的孩子，该死的！

##java.util
- ConcurrentModificationException	
	- 有人修改了你的 Java 代码。你应该更改密码。
- EmptyStackException	
	- 为了让 Java 工作，你必须在桌子上放一叠 Java 书籍。当然，如果书很厚的话，一本就够了。
- MissingResourceException	
	- 你太穷了，不配使用 Java。换一个更便宜的语言吧（比如 Whitespace、Shakesperre、Cow、Spaghetti 或者 C#）。
- NoSuchElementException	
	- 这里只存在四种元素（地球、水、空气、火）。《第五元素》只是部电影而已。
- TooManyListenersException	
	- 你被太多秘密机构窃听了，SecurityException 马上就到。

##java.awt
- AWTException	
	- 你正在使用AWT，也就是说你的图形界面会很丑。这个异常只是一个警告可以被忽略。
- FontFormatException	
	- 你的布局很丑陋，或者你选择了一个糟糕的字体，或者太多的字体。请咨询一名专业的设计师。
- HeadlessException	
	- Java 认为身为一名程序员，你实在是太蠢了。
- IllegalComponentStateException	
	- 你的一个硬件（例如硬盘、CPU、内存）坏掉了。请联系你的硬件供应商。

##java.awt.color
- CMMException	
	- 你的 CMM 坏掉了，真是见鬼了。我经常烧毁自己的房子，然后去一个新的城市重新开始。
- ProfileDataException	
	- 你的个人档案包含可疑信息。如果你不是一名共产主义者、恐怖分子或者无神论者，请联系 CIA 修正错误。

##java.awt.datatransfer
- MimeTypeParseException	
	- 你的哑剧（Mime）糟透了，没人能够理解你到底想表达什么。尝试一些更简单的事情吧，比如迎风散步，或者被困在一个看不见的盒子里。
- UnsupportedFlavorException	
	- 你正试图使用一种 Java 不知道的香料。大部分人似乎只知道使用香草和樱桃。

##java.beans
- IntrospectionException	
	- 你太内向了，你应该变得外向一些。 别再当一个呆子，出门去见见人吧！
- PropertyVetoException	
	- 你的一部分财产被冻结了。这条信息应该已经告诉你谁干的和原因。如果没看见，你可能也不该询问。

##java.io
- CharConversionException	
	- 你一直试图焚烧一些不燃物。也可能是因为你试着把自己变成一条鱼，但这不可能发生。
- EOFException	
	- 你得到这条异常是因为你不知道EOF是什么意思。但是，我并不打算告诉你，因为你是一个不学无术的人。
- FileNotFoundException	
	- 一名木匠应该总是知道他的工具放在哪里。
- InterruptedIOException	
	- 你不顾之前的 IOException，一直在使用 IO，然后你的活动就被中断了。
- InvalidClassException	
	- 查看 ClassNotFoundException。
- InvalidObjectException	
	- 反对无效，就像他们在法庭上说的一样。
- IOException	
	- IO 代表输入、输出，并且不得不做收发数据的事。IO 是一个安全问题，不应使用。
- NotActiveException	
	- 这个异常意味着两件事。要么是未激活，需要激活；要么是已激活，需要停止。到开始工作为止，激活与未激活都是随机的。
- NotSerializableException	
	- 你正试图把一部电影改成电视剧。
- ObjectStreamException	
	- 你提出了一连串的反对（Object）意见。提出新的意见前，请限制自己一下，等待法官作出判决。查看 InvalidObjectException。
- OptionalDataException	
	- 你似乎认为一些可选数据是必须的。不要让事情变得复杂。
- StreamCorruptedException	
	- 你的数据流被损坏了，这意味着它已经被截包，并在黑市上贩卖。
- SyncFailedException	
	- 你试图与其他人同步你的失败，然后被证明比他人更加失败。去找一些跟你同等水平的人吧。
- UnsupportedEncodingException	
	- 如果你想在网上发送自己的代码，必须与美国国家安全局核对你的加密密匙。如果不这么做，将把你视为恐怖分子，并以适当方式处理。如果你得到这个异常，能跑多快跑多快。
- UTFDataFormatException	
	- UTF 代表通用传输格式，是一种无论你使用哪种格式都会用到的数据传输方式。你试图通过 UTF 传输错误格式的数据。
- WriteAbortedException	
	- 你需要在程序中的某处写上“aborted”。这通常没什么意义，但你就得这样做。

##java.net
- BindException	
 - Java编程和束缚不能混为一谈。
- ConnectException	
	- 你正试图与一个不能连接的事物建立连接。试着连接其他事物吧。也许可以通过一个特殊的连接对象实现你想要的连接。
- MalformedURLException	
	- 你正在制作一个形状错误的壶（例如一个“L”状），或者你有拼写错误的单词“urn”（例如“url”）。
- NoRouteToHostException	
	- 没有通往主机的“道路”，请联系公路管理员。
- PortUnreachableException	
	- 港口必须正确地放置在水边。如果在内陆，它们将会无法接触。
- ProtocolException	
	- 这是一个严重违反规定的结果（例如在你主机上的“puk韓g”）。解决方法很简单：不要那样做！
- SocketException	
	- 你把电脑连接到了错误的电源插座。大部分情况下你不得不寻找其它插座，但一些电脑背部有一个开关，可以设置电源插座类型。
- SocketTimeoutException	
	- 你的电脑连接了一个带计时器的电源插座，并且时间已经走完。只有烙铁和相似的东西才会使用这种插座。
- UnknownHostException	
	- 你的父母没有教过你不要和陌生人说话么？
- UnknownServiceException	
	- 你正试图进入接近一个未知服务。众所周知，未知服务或许是特工组织。
- URISyntaxException	
	- “You are I”是一个语法错误的句子。将其改为“You are me”，别管那到底啥意思。

##java.rmi
- AccessException	
	- 你正在使用“Microsoft Access”。请不要这样做。
- AlreadyBoundException	
	- 不管在 java.net.BindException 的描述中是什么状况，RMI 都提供捆绑服务。然而，你不能绑一个已经被捆绑的人。
- ConnectException	
	- 你正试图与一个不能连接的事物建立连接。试着连接其他事物吧。也许可以通过一个特殊的连接对象实现你想要的连接。
- ConnectIOException	
	- 你正试图通过 IO 与另一个不能被连接的事物建立连接。尝试连接其他事物吧。或许你可以通过一个特殊的连接对象实现想要的连接。
- MarshalException	
	- 你的“marshal”出问题了。你应做的事取决于我们正在讨论的是哪种“marshal”。他可以是陆军元帅、警察、消防队员或者只不过是一名普通的司仪。注意这个异常与马绍尔群岛共和国没有任何关系，也称为 RMI。
- NoSuchObjectException	
	- 你正试图使用一个不存在的对象。以爱因斯坦之名，创造它或者不要使用它！
- NotBoundException	
	- 如果你正在使用奴隶，请确认至少有一个人被绑住了。
- RemoteException	
	- 这是一条远程抛出的特殊异常。如果其他人的应用变得不稳定，以致于不能产生一条异常，相反地，你可能会得到这条异常。请找到源头并提醒那位程序员这个错误。
- RMISecurityException	
	- 马绍尔群岛共和国变得不稳定了。如果你住在这儿，你最好离开，直到安全得到保障为止都别回来。如果你住在其他地方，可以无视这个异常。
- ServerException	
	- 第二发球（或者双发失误同样适用）。
- ServerRuntimeException	
	- 只要是网球比赛都很长。当你花太长时间发球时，就会得到这条异常。
- StubNotFoundException	
	- 当你去看电影的时候，你应该一直保留自己的票根。如果不这么做，并且离开了电影院，你就不能重新进去，不得不去买张新票。所以保留你的票根！
- UnexpectedException	
	- 这个异常对你来说应该会成为一个大惊喜。如果发生了，所有事都变成它应该的样子。
- UnknownHostException	
	- 你父母没有教过你不要和陌生人说话吗？
- UnmarshalException	
	- 你没有完成一名法律工作人员的职责（例如你曾经的法官工作）。注意这个正确的术语是“曾经”（used to）。你已经被解雇（fire）了（如果你是一名消防队员（firefighter），这可真是讽刺啊）。

##java.security
- AccessControlException	
	- 你失去了对 Microsoft Access 的控制。如果你无法重获控制或者通过其他方式停止程序，你应该尽快切断电脑电源。
- DigestException	
	- 你应该注意自己的食物，消化不良也能变成严重的问题。
- GeneralSecurityException	
	- 在某些地方做一些事情并不安全。如果你有足够的权力，你应该随机入侵一个国家（最好在中东地区）。如果你没有那种权力，至少应该有一把枪。
- InvalidAlgorithmParameterException	
	- 你向一位残疾人用他不能理解的方式解释你的算法。简单一点！
- InvalidKeyException	
	- 这个异常有两种不同的原因：1、你正在使用错误的钥匙。我的建议是在你的钥匙上画不同颜色的小点来帮助你记住哪一把对应哪一个锁。2、 你不能锁住残疾人却不给他们钥匙，如果他们足够聪明发现如何使用钥匙，他们就有自由移动的权利。
- InvalidParameterException	
	- 你使用了蔑视的术语去描述一名残疾人。
- KeyException	
	- 不要尝试不用钥匙就能开锁。
- KeyManagementException	
	- 你遗失了自己的钥匙。很可能忘在办公室（如果你正试图进入你家）或者忘在家里（如果你正试图进入办公室）。
- KeyStoreException	
		- 延续之前 KeyManagementException 的解释就是你的钱包有个洞。
- NoSuchAlgorithmException	
	- 你试图用以前未知的方法解决问题。停止创新吧，用老算法重写一遍。你也可以为自己的想法申请专利，然后等待未来 Java 发布新版本的时候纳入其中。
- NoSuchProviderException	
	- 如果你是一名单亲妈妈，你没法成为家庭主妇。首先，你得为家庭找到一名供养者。
- PrivilegedActionException	
	- 你试图采取一个行动，但是没有得到权限。比如，只有名人才可以做到地从谋杀中逃脱，只有天主教神父和耶和华的高级见证人才能做地猥亵儿童，只有在私人企业担任管理职位的人才能被允许地偷钱。
- ProviderException	
	- 你是一名妇女并试图供养一个家庭。显而易见，你的丈夫不能成为一名“家庭主妇”，所以你得让他供养个家庭。想象一下，Java固执且不肯改变，事情就是这样工作的，解决它。
- SignatureException	
	- 要么你是伪造的其他人的签名，要么是无法接受你的签名。一个签名不能太丑陋、太易读或太大。
- UnrecoverableKeyException	
	- 该死。你把你的钥匙扔进了下水沟。我唯一能安慰你的就是其他人也无法恢复钥匙，所以倒不是必须换掉你的锁。

##java.text
- ParseException	
	- 你做的没有任何意义，冷静下来，再试一次。

---
原文链接：[rymden](http://rymden.nu/exceptions.html)  
首发至 [importnew](http://www.importnew.com/)   
译文链接：http://www.importnew.com/16725.html  
本文为原创文章，转载请注明http://honoka.cnblogs.com。

