在设计 lan (Github: [https://github.com/phodal/lan](https://github.com/phodal/lan)) 物联网平台的时候，结合之前的一些经验，构建出一个实际应用中的物联网构架模型。

然后像[lan](https://github.com/phodal/lan)这样的应用，在里面刚属于服务层。

##物联网层级结构

通常，我们很容易在网上看到如下图所示的三层结构:

![物联网三层结构][1]

从理论上划分这样的层级结构是没有问题的，也是有各种理论依据。然而理论和现实往往是严重脱轨的，如上图所示，图中将网络层单独分为了一层，而并没有独立出应用程序相关的功能。

从实践的角度上，我更愿意用如下的架构来构建我的物联网系统。

![物联网层级结构][2]

其功能可以用下表来表示。

层级|作用|与下一层级的连接方式 
---|----------|------------------
硬件层|获取、发送传感器数据，执行指令|串口、蓝牙、有线、SPI、WiFi、USB等等
协调层|协调硬件层与服务器的通信，并负责处理部分数据|网络连接及硬件层的连接方式
服务层|以视为服务器层|网络连接
应用程序层|为用户提供交互功能|网络连接

硬件层包含了数据众多的传感器、控制器、以及执行器，通常这部份会由硬件人员与硬件开发人员一起协作和开发。而协调层则是充当硬件与服务层通信的桥梁，这是在系统中需要**特别考虑**的部份，一个物联网系统的设计主要**取决于这个层级**。

##物联网服务层

而服务层的核心是传统的Web应用程序的结构，只是协议层变成了一些适配器，我们需要支持不同的协议，这导致了我们在这个层需要有一个更好的结构，故而我们建议使用**六边形架构**。而在实际中，用户最后接触到的便是应用程序层，在这一层中需要有很好的用户体验设计及流畅度。

因而在设计[Lan](https://github.com/phodal/lan)物联网平台的时候，参考了之前的[物联网平台](https://github.com/phodal/diaonan)的设计，增加了用户授权以及模块化加载思想。

![IoT Server Layer][3]

上图的模型可以让我们脱离具体的框架与实现，关注于业务上逻辑。

  [1]: /static/media/uploads/iot-3-layer.jpg
  [2]: /static/media/uploads/iot-layer.jpg
  [3]: /static/media/uploads/iot-server.jpg
  
  