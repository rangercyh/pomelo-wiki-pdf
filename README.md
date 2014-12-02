pomelo是基于Node.js的，目前pomelo已经完全支持Windows、Linux、Mac等多种平台。

准备
========

* 确保你的机器可以上网,因为安装pomelo的过程需要从网上下载其依赖的包。

* 确保你的系统上已经要安装了Node，目前最新的Node提供了已经编译好的二进制安装包，包括Windows，Mac和Linux等平台。想省事的话，直接去[这里](http://nodejs.org/download/ "下载Node安装包")下载对应的安装包，直接安装就好了。Node同时也提供了传统的从源码编译的方式安装，不过比起直接使用二进制的方式要麻烦。

* 确保你的系统中安装有python(2.5 < version < 3.0)以及C++的编译器。Node的源码主要由C++代码和JavaScript代码构成，但是却用[gyp](http://code.google.com/p/gyp/ "gyp")工具来做源码的项目管理，该工具采用Python语言写成的。对于非windows平台，一般都会预装Python以及C++编译工具；对于Windows系统，请确保你的Windows系统包含源码编译工具。在Windows平台上，Node.js采用gyp来生成Visual Studio Solution文件，最终通过VC++的编译器将其编译为二进制文件。

* 虽然pomelo是用Javascript写成，但是pomelo依赖的库中，有使用了C++语言写的扩展，因此安装pomelo的过程中会使用到C++编译器。 所以，在安装之前请确保你的Windows系统满足以下两个条件：
     - [python](http://python.org/)(2.5<version<3.0)。
     - VC++ 编译器，包含在[Visual Studio 2010](http://msdn.microsoft.com/en-us/vstudio/hh388567)中（VC++ 2010 Express亦可）。对于windows8的用户，需要安装Microsoft Visual Studio C++ 2012。

* 如果你使用的是`Mac OS X`系统, 则需要安装[Xcode Command Line Tools](https://developer.apple.com/downloads/index.action?q=xcode)或者[Xcode](https://developer.apple.com/xcode/)的完整包以及make工具.


安装pomelo
===========

使用npm(node包管理工具)全局安装pomelo: 

    $ npm install pomelo -g

可以通过如下命令下载源代码的方式安装

    $ git clone https://github.com/NetEase/pomelo.git
    $ cd pomelo
    $ npm install -g

其中-g表示全局安装，关于npm的使用问题，可以参考[npm的文档](https://npmjs.org/doc/ "npm的文档")，里面有详细的npm使用的介绍。如果安装过程中没有报错误，说明安装成功。

windows下安装经验：

    1. node,vs2010 和 python(2.5<v<3) 都是32位或者都是64位的。
    2. 配置  PYTHON=d:\Python27\python.exe(设置成你自己的路径)。注意不是path里面,而是和path同级的，直接在全局或者当前用户下配置。
    3. 保证环境变量path里面有 %SystemRoot%\system32;%SystemRoot%;%SystemRoot%\System32\Wbem;
      注： 这三个环境变量中貌似只有%SystemRoot%\system32这个环境变量有用，没具体试（没有他会报CreateProcessW找不到的错误)。
    4. 如果在命令行界面安装pomelo失败，可以在Visual Studio的命令行界面安装。

下面我们将通过一个[HelloWorld项目](pomelo的HelloWorld "HelloWorld")来检验我们的安装是否成功。
pomelo是一个游戏服务器框架，与以往单进程的游戏框架不同, 它是高性能、高可伸缩、分布式多进程的游戏服务器框架，并且使用很简单。它包括基础开发框架和一系列相关工具和库，可以帮助开发者省去游戏开发中枯燥的重复劳动和底层逻辑工作，免除开发者的重造轮子，让开发者可以更多地去关注游戏的具体逻辑，大大提高开发效率。pomelo强大的可伸缩性和灵活性使得pomelo也可以作为通用的分布式实时应用开发框架，用于一些高实时应用的开发，而且pomelo在很多方面的表现甚至超越了现有的开源实时应用框架。pomelo支持所有主流平台的客户端，并提供了客户端的开发库，使得客户端的开发变得很友好。

pomelo组成
===============

pomelo 是由一系列相互之间弱耦合的部分组合而成的，包括：

* #### 框架
框架是pomelo最核心的部分;

* #### 库
pomelo提供了很多库，有些是跟游戏逻辑完全相关的，如AI，AOI，寻路等；也有与游戏逻辑无关但比较通用的，如定时任务执行， 数据同步等等；

* #### 工具
pomelo提供了服务器管理控制工具、命令行工具、压力测试工具等一系列工具；

* #### 客户端库
pomelo提供了各类平台的客户端开发库，包括js, C, C#，Android, iOS, Unity3D等等，几乎支持涵盖了目前所有的主流平台，由于pomelo的协议是开放的，架构耦合松散，对于没有支持的客户端平台，用户也可以很容易地开发出自己需要的库，定制自己的通信协议；

* #### demo
一个框架需要强大的demo来展示功能并为开发者提供示例，pomelo提供了全平台的聊天demo和基于HTML5的捡宝demo，系统还提供了一个强大的基于HTML5开发的MMO游戏demo[Lordofpomelo](http://pomelo.netease.com/lordofpomelo/ "Lordofpomelo")（[源码](https://github.com/NetEase/lordofpomelo "Lordofpomelo源码")）。

为什么使用pomelo？
==================

高并发、高实时的游戏服务器的开发是很复杂的工作。跟web应用一样， 一个好的开源容器或开发框架可以大大减少游戏服务器开发的复杂性，让开发变得更加容易。遗憾的是目前在游戏服务器开发领域一直没有太好的开源解决方案。 pomelo将填补这个空白， 打造一款完全开源的高性能高并发游戏服务器框架。 pomelo的优势有以下几点：

* #### 架构的可伸缩性好
采用多进程单线程的运行架构，扩展服务器非常方便， node.js的网络io优势提供了高可伸缩性，写好的应用只需要简单地修改一下配置就能轻松地伸缩扩充；

* #### 易用
pomelo基于轻量级的nodejs，其开发模型与web应用的开发类似，基于convention over configuration的理念， 几乎零配置， api的设计也很精简，很容易上手，开发快速；

* #### 框架的松耦合和可扩展性好
遵循node.js微模块的原则， 框架本身只有很少的代码，所有component、库、工具都可以用npm module的形式扩展进来，任何第三方都可以根据自己的需要开发自定义module，并把它整合到pomelo的框架中。

* #### 完整的demo和文档
pomelo提供了完整的中英文文档，pomelo还提供一个完整的开源MMO游戏demo--[Lordofpomelo](http://pomelo.netease.com/lordofpomelo/ "Lord of pomelo线上")（[源码](https://github.com/NetEase/lordofpomelo "Lordofpomelo源码")），一个超过1万行代码的游戏demo，使开发者可以随时借鉴demo的设计与开发思路。

pomelo的定位
=============

pomelo是一个轻量级的服务器框架，它最适合的应用领域是网页游戏、社交游戏、移动游戏的服务端，开发者会发现pomelo可以用如此少的代码达到强大的扩展性和伸缩性。当然还不仅仅是游戏，用pomelo开发高实时web应用也如此合适， 而且伸缩性比其它框架好。

不推荐将pomelo用于大型的MMORPG游戏开发，尤其是大型3D游戏， 还是需要象Bigworld这样的商用引擎来支撑。

好了，是不是有迫不及待了，那就赶快[安装pomelo](安装pomelo "pomelo 安装")来试试吧。

pomelo的通信协议是开放的，又是可定制的，因此，理论上pomelo可以与使用任意协议的任意平台的客户端进行通信。当用户开发客户端时，可以根据相应的通信协议完成与服务端的通信。

为了方便开发者，目前pomelo提供了一些常见客户端平台的开发库。这些平台包括web，iOS， java & android, unity3d, flash以及C语言的库libpomelo等。基本上每种平台都提供了基于socket.io和使用socket/websocket的开发库版本。也欢迎大家提供一些客户端开发库，供大家使用。

下面是这些开发库的链接概述:

* **Javascript**

   * websocket version: [pomelonode/pomelo-jsclient-websocket](https://github.com/pomelonode/pomelo-jsclient-websocket) 

   * socket.io version: [pomelonode/pomelo-jsclient-socket.io](https://github.com/pomelonode/pomelo-jsclient-socket.io) 

* **C**

   * socket vesion: [NetEase/libpomelo](https://github.com/NetEase/libpomelo/)

* **iOS**

   * socket.io version: [NetEase / pomelo-iosclient](https://github.com/NetEase/pomelo-iosclient)

   * socket version: [ETiV / PomeloClient-iOS-WebSocket](https://github.com/ETiV/PomeloClient-iOS-WebSocket)

* **Android & Java**

   * [NetEase / pomelo-androidclient](https://github.com/NetEase/pomelo-androidclient)

   * [jzsues / pomelo-websocket-java-client](https://github.com/jzsues/pomelo-websocket-java-client)

* **unity3d**

   * socket.io version: [NetEase / pomelo-unityclient](https://github.com/NetEase/pomelo-unityclient)

   * socket version: [NetEase / pomelo-unityclient-socket](https://github.com/NetEase/pomelo-unityclient-socket)

* **flash**

   * socket.io version: [stokegames / pomelo-flashclient](https://github.com/stokegames/pomelo-flashclient)

   * socket version: [D-Deo / pomelo-flash-tcp](https://github.com/D-Deo/pomelo-flash-tcp)

* **cocos2dx**

  * c++: [NetEase / pomelo-cocos2dchat](https://github.com/NetEase/pomelo-cocos2dchat)

热身
====================

* 本教程适用于对pomelo零基础的用户，如果你已经有过一定的pomelo开发基础，请跳过这个教程，你可以阅读开发指南，那里会对一些话题作较为详细的探讨。

* 由于pomelo是基于node.js并使用javascript开发的，因此希望你在阅读本教程前对node.js和javascript有一些了解。

* 本教程的示例源码放在github上，对于教程的不同部分，使用了不同的分支，因此希望你在使用本教程之前对github有个简单的了解，能帮助你更好地使用本教程。

* 本教程将以一个实时聊天应用为例子，通过对这个应用进行不同的修改来展示pomelo框架的一些功能特性,让用户能大致了解pomelo，熟悉并能够使用pomelo进行应用程序的开发。

* 本教程假定你使用的开发环境是类Unix系统，如果你使用的Windows系统，希望你能够知道相关的对应方式，比如一些.sh脚本，在Windows下会使用一个同名的bat文件，本教程中对于Windows系统，不做特殊说明。

为什么是聊天?
=================

Pomelo是游戏服务器框架，本质上也是高实时、可扩展、多进程的应用框架。除了在提供的库部分有一部分游戏专用的库，其余部分框架完全可用于开发高实时的应用。而且与现在有的node.js高实时应用框架如derby、socketstream、meteor等比起来有更好的可伸缩性。

由于游戏在场景管理、客户端动画等方面有一定的复杂性，并不适合作为pomelo的入门应用。对于大多数开发者而言，node.js的入门应用都是一个基于socket.io开发的普通聊天室， 由于它是基于单进程的node.js开发的， 在可扩展性上打了一定折扣。

因此，我们也选择做一个聊天应用来作为教程的例子，而基于pomelo框架开发的聊天应用天生就是多进程的，可以非常容易地扩展服务器类型和数量。

教程内容
==============

在之前的章节中，我们已经看到了HelloWorld项目，对如何使用pomelo开发应用程序应该有了一个初步的印象。在这个教程里面，我们将以一个使用pomelo开发的实时聊天应用为示例，来依次展示如何在pomelo增加一个filter、进行route压缩、rpc调用和使用protobuf等。这些例子仅仅是为了展示pomelo框架的特性，所以并不具有很强的实用性, 只是希望用户通过对这些例子的学习，可以熟悉pomelo各个特性的使用，给用户一个直观的认识,使得用户也能按照例子的方式，使用pomelo提供的功能。其大致内容包括以下部分：

* 我们首先会对pomelo中常见的一些术语进行一个简要的解释;
* 从github获得一个现成的分布式聊天应用，我们对其源码进行分析，然后让其运行起来;
* 对我们的聊天应用的服务器进行扩展，使用多个服务器来完成我们的应用; 
* 给原来的应用增加一个filter，来实现我们想要的功能，同时学会filter在pomelo中的使用;
* pomelo提供了route压缩，尝试在我们的应用里使用route压缩，同时学会如何在pomelo中使用route压缩功能;
* pomelo提供了基于protobuf的消息压缩，尝试将其运用到我们的项目中,同时学会如何在pomelo中使用基于protobuf的消息压缩;
* 增加一个获取时间的rpc服务，当然功能上纯粹属于“画蛇添足”，不过这里是出于演示如何使用rpc的目的;
* 尝试给pomelo增加一个HelloWorld component，目的同上，只是为了演示如何给pomelo扩展组件，从而学会给pomelo扩展自定义组件;
* 增加一个admin-module，以演示如何使用admin-module来扩展pomelo的服务器管理监控框架;
* 最后是关于pomelo的一些杂项以及总结。

当完成上面的教程后，相信你已经能够熟练使用pomelo提供的各项特性做一些开发了，这也是本教程要达到的目的。更深入的探讨可以参阅开发指南，或者直接阅读源码都是可以的。下面进入[下一步](术语解释 "术语解释")，我们将对pomelo中的一些术语进行简单的解释。

当我们的应用只有很少人用的时候，往往只需要一台服务器就可以支撑。但是随着用户的增加，一台服务器可能就无法承受同一时刻巨大的访问量，这需要我们对服务器进行伸缩扩充。

多服务器版本的聊天应用在分支`tutorial-multi-server`上，你需要执行如下命令来切换到多服务器分支上：
     
    $ git checkout tutorial-multi-server

配置修改
=========

在pomelo中，对服务器的扩充非常简单，只需要修改一下配置文件，多添几台服务器配置就行了，对于我们的聊天例子来说，如下下面所示，在config/servers.json中的配置：

```json
{
 "development":{
      "connector":[
           {"id":"connector-server-1", "host":"127.0.0.1", "port":4050, "clientPort": 3050, "frontend": true},
           {"id":"connector-server-2", "host":"127.0.0.1", "port":4051, "clientPort": 3051, "frontend": true},
           {"id":"connector-server-3", "host":"127.0.0.1", "port":4052, "clientPort": 3052, "frontend": true}
       ],
      "chat":[
           {"id":"chat-server-1", "host":"127.0.0.1", "port":6050},
           {"id":"chat-server-2", "host":"127.0.0.1", "port":6051},
           {"id":"chat-server-3", "host":"127.0.0.1", "port":6052}
      ],
      "gate":[
       {"id": "gate-server-1", "host": "127.0.0.1", "clientPort": 3014, "frontend": true}
    ]
  },
  "production":{
    "connector":[
      {"id":"connector-server-1", "host":"127.0.0.1", "port":4050, "clientPort": 3050, "frontend": true},
      {"id":"connector-server-2", "host":"127.0.0.1", "port":4051, "clientPort": 3051, "frontend": true},
      {"id":"connector-server-3", "host":"127.0.0.1", "port":4052, "clientPort": 3052, "frontend": true}
    ],
    "chat":[
      {"id":"chat-server-1", "host":"127.0.0.1", "port":6050},
      {"id":"chat-server-2", "host":"127.0.0.1", "port":6051},
      {"id":"chat-server-3", "host":"127.0.0.1", "port":6052}
    ],
    "gate":[
      {"id": "gate-server-1", "host": "127.0.0.1", "clientPort": 3014, "frontend": true}
    ]
  }
}

```

router配置
============


与前面的每个服务器类型仅有一台服务器的例子相比，这里我们的connector和chat都具有多台服务器。因此需要考虑对用户请求的服务器分配问题。

对于gate服务器来说，在前面的例子中，由于只有一个connector服务器，所以直接返回仅有的一个服务器就行了，而这里有多台服务器，所以需要从中选择一个服务器的信息进行返回，这里我们增加了一个工具函数dispatch,它完成具体的分配运算，他使用用户的uid的crc32的校验码与connector服务器的个数取余，从而得到一个connector服务器，大致代码如下:

```javascript
// util/dispatcher.js
module.exports.dispatch = function(key, list) {
    var index = Math.abs(crc.crc32(key)) % list.length;
      return list[index];
};

// gateHandler.js
handler.queryEntry = function(msg, session, next) {
  // ...

  // get all connectors
	var connectors = this.app.getServersByType('connector');

  // ...
  
  var res = dispatcher.dispatch(uid, connectors); // select a connector from all the connectors
  // do something with res
};

```

当客户端请求到来时，因为有多台chat服务器，需要选择由哪台chat服务器来服务，也就是前端服务器把这个客户端请求路由到哪个后端服务器上。配置路由使用application的route调用，这里我们也使用了前面提到的工具函数dispatch，使用同样的服务器分配策略，示例如下：

```javascript
// app.js

// route definition for chat server
var chatRoute = function(session, msg, app, cb) {
  var chatServers = app.getServersByType('chat');

	if(!chatServers || chatServers.length === 0) {
		cb(new Error('can not find chat servers.'));
		return;
	}

	var res = dispatcher.dispatch(session.get('rid'), chatServers);

	cb(null, res.id);
};

app.configure('production|development', function() {
  app.route('chat', chatRoute);
});

```

其中chatRoute就是路由函数，他接受四个参数，返回一个其选择的后端服务器id，四个参数中，第一个是专门用作路由计算的参数，前端服务器路由请求给后端服务器发rpc调用时，会使用session作为计算路由的参数，但是当用户自定定义rpc的时候，用户完全可以自己定义这个参数的含义，当然也可以使用session。第二个参数msg描述了当前rpc调用的所有信息，包括调用的服务器类型，服务器名字，具体的调用方法等信息。第三个参数是一个上下文变量，一般情况下会由app来充当，第四个是一个获得到后端服务器id后的回调函数。

一些说明
============

* 通过修改服务器的配置文件，并增加具体的路由选择配置，就可以很轻易地实现服务器的扩充。 对于我们这个应用来说，如果我们还想继续扩充我们的服务器，那么只需在servers.json里面继续增加服务器的配置就行了。

* 如果我们一开始实现时就考虑以后的扩充，实现所有的路由选择函数的话，那么以后当需要扩充服务器的时候，只需要在servers.json里面增加相应的配置就行了。

* 关于客户端请求的路由，你可能会问，为什么我们在单服务器的那个例子里，没有给chat定义router。那是因为如果我们不定义router的话，pomelo会使用一个默认的router完成路由，因为只有一台chat服务器，那么pomelo总会把所有的对其的请求路由给这个服务器，所以，我们在前一个例子中，就省略掉了chat的路由配置。

* 实际应用中，我们一般都要自己实现router,而不使用pomelo默认的。使用多台服务器要考虑负载平衡，同时要尽量使得服务器的服务是无状态的。我们chat的例子中，定义的router就是使用了用户的rid的crc校验码作为键值对当前的所有chat服务器个数做了一个简单的hash运算，以使得所有的chat服务器的负载尽可能平衡。

小结
============

在这部分，我们实现了对服务器的扩充，它是如此的简单，只需要修改相应的服务器配置即可。下面我们将尝试使用pomelo的[filter机制](增加filter "增加filter")继续完善我们的聊天应用。


使用pomelo框架的话，有pomelo自己的术语，这里先对术语做一些简单的解释，给读者一个直观的概念，不至于看到相应术语时产生迷惑。

常见术语
=============

### gate服务器

一个应用的gate服务器，一般不参与rpc调用，也就是说其配置项里可以没有port字段，仅仅有clientPort字段，它的作用是做前端的负载均衡。客户端往往首先向gate服务器发出请求，gate会给客户端分配具体的connector服务器。具体的分配策略一般是根据客户端的某一个key做hash得到connector的id，这样就可以实现各个connector服务器的负载均衡。

### connector服务器

connector服务器接收客户端的连接请求，创建与客户端的连接，维护客户端的session信息。同时，接收客户端对后端服务器的请求，按照用户配置的路由策略，将请求路由给具体的后端服务器。当后端服务器处理完请求或者需要给客户端推送消息的时候，connector服务器同样会扮演一个中间角色，完成对客户端的消息发送。connector服务器会同时拥有clientPort和port，其中clientPort用来监听客户端的连接，port端口用来给后端提供服务。

### 应用逻辑服务器

gate服务器和connector服务器又都被称作前端服务器，应用逻辑服务器是后端服务器，它完成实际的应用逻辑，提供服务给客户端，当然客户端的请求是通过前端服务器路由过来的。后端服务器之间也会通过rpc调用而有相互之间的交互。由于后端服务器不会跟客户端直接有连接，因此后端服务器只需监听它提供服务的端口即可。

### master服务器

master服务器加载配置文件，通过读取配置文件，启动所配置的服务器集群，并对所有服务器进行管理。

### rpc调用

pomelo中使用rpc调用进行进程间通信，在pomelo中rpc调用分为两大类，使用namespace进行区分，namespace为sys的为系统rpc调用，它对用户来说是透明的，目前pomelo中系统rpc调用有：
* 后端服务器向前端服务器请求session信息
* 后端服务器通过channel推送消息时对前端服务器发起的rpc调用
* 前端服务器将用户请求路由给后端服务器时也是sys rpc调用
除了系统rpc调用外，其余的由用户自定义的rpc调用属于user namespace的rpc调用，需要用户自己完成rpc服务端remote的handle代码，并由rpc客户端显式地发起调用

### route,router

route用来标识一个具体服务或者客户端接受服务端推送消息的位置，对服务端来说，其形式一般是<ServerType>.<HandlerName>.<MethodName>,例如"chat.chatHandler.send", chat就是服务器类型，chatHandler是chat服务器中定义的一个Handler，send则为这个Handler中的一个handle方法。对客户端来说，其路由一般形式为onXXX，当服务端推送消息时，客户端会有相应的回调。
一般来说具体的同类型应用服务器都会有多个，当客户端请求到达后，前端服务器会将用户客户端请求派发到后端服务器，这种派发需要一个路由函数router，可以粗略地认为router就是根据用户的session以及其请求内容，做一些运算后，将其映射到一个具体的应用服务器id。可以通过application的route调用给某一类型的服务器配置其router。如果不配置的话，pomelo框架会使用一个默认的router。pomelo默认的路由函数是使用session里面的uid字段，计算uid字段的crc32校验码，然后用这个校验码作为key，跟同类应用服务器数目取余，得到要路由到的服务器编号。注意这里有一个陷阱，就是如果session没有绑定uid的话，此时uid字段为undefined，可能会造成所有的请求都路由到同一台服务器。所以在实际开发中还是需要自己来配置router。

### Session, FrontendSession, BackendSession， SessionService， BackendSessionService

在pomelo框架中，有这三个session的概念，同时又有两个service： `SessionService`和`BackendSessionService`，也是最令人迷惑的地方，这里尝试给出一些说明，让你的理解更清晰一些：
Session的是一个客户端连接的抽象，它的大致字段如下：

```javasript
{
    id : <session id> // readonly
    frontendId : <frontend server id> // readonly
    uid : <bound uid> // readonly
    settings : <key-value map> // read and write  
    __socket__ : <raw_socket>
    __state__ : <session state>

    // ...
}
```

* id是这个session的id，是全局唯一的，一般使用自增的方式来生成;
* frontendId是维护这个session的前端服务器的id；
* uid是这个session所绑定的用户id;
* \_\_socket\_\_是底层原生socket的引用;
* \_\_state\_\_用来指明当前session的生命周期状态。
* settings维护一个key-value map，用来描述session的一些自定义属性，比如聊天应用中的房间号就可以看作是session的一个自定义属性。

从上面的分析看，一个session一旦建立，那么id， frontendId，\_\_socket\_\_, \_\_state\_\_, uid都是确定的，都应该是只可读不可写的。而settings也不应该被随意的修改。
因此，在前端服务器中，引入了FrontendSession, 可以把它看作是一个内部session在前端服务器中的傀儡，FrontendSession的字段大致如下:

```javascript
{
    id : <session id> // readonly
    frontendId : <frontend server id> // readonly
    uid : <bound uid> // readonly
    settings : <key-value map> // read and write  
}
```

其作用：
* 通过FrontendSession可以对settings字段进行设置值，然后通过调用FrontendSession的push方法，将设置的settings的值同步到原始session中;
* 通过FrontendSession的bind调用，还可以给session绑定uid;
* 当然也可以通过FrontendSession访问session的只读字段，不过对FrontendSession中与session中相同的只读字段的修改并不会反映到原始的session中。

SessionService维护所有的原始的session信息,包括不可访问的字段，绑定的uid以及用户自定义的字段。

下面再说BackendSession，与FrontendSession类似，BackendSession是用于后端服务器的，可以看作是原始session的代理，其数据字段跟FrontendSession基本一致。

BackendSession是由BackendSessionService创建并维护的，在后端服务器接收到请求后，由BackendSessionService根据前端服务器rpc的参数，进行创建。对BackendSessionService的每一次方法调用实际上都会生成一个远程调用，比如通过一个sid获取其BackendSession。同样，对于BackendSession中字段的修改也不会反映到原始的session中，不过与FrontendSession一样，BackendSession也有push，bind，unbind调用，它们的作用与FrontendSession的一样，都是用来修改原始session中的settings字段或者绑定/解绑uid的，不同的是BackendSession的这些调用实际上都是名字空间为sys的远程调用。

### Channel

channel可以看作是一个玩家id的容器，主要用于需要广播推送消息的场景。可以把某个玩家加入到一个Channel中，当对这个Channel推送消息的时候，所有加入到这个Channel的玩家都会收到推送过来的消息。一个玩家的id可能会被加入到多个Channel中，这样玩家就会收到其加入的Channel推送过来的消息。需要注意的是Channel都是服务器本地的，应用服务器A和B并不会共享Channel，也就是说在服务器A上创建的Channel，只能由服务器A才能给它推送消息。

### request, response, notify, push

pomelo中有四种消息类型的消息，分别是request，response，notify和push，客户端发起request到服务器端，服务器端处理后会给其返回响应response;notify是客户端发给服务端的通知，也就是不需要服务端给予回复的请求;push是服务端主动给客户端推送消息的类型。在后面的叙述中，将会使用这些术语而不再作解释。


### filter

filter分为before和after两类，每类filter都可以注册多个，形成一个filter链，所有的客户端请求都会经过filter链进行一些处理。before filter会对请求做一些前置处理，如：检查当前玩家是否已登录，打印统计日志等。after filter是进行请求后置处理的地方，如：释放请求上下文的资源，记录请求总耗时等。after filter中不应该再出现修改响应内容的代码，因为在进入after filter前响应就已经被发送给客户端。

### handler

handler是实现具体业务逻辑的地方，在请求处理流程中，它位于before filter和after filter之间，handler的接口声明如下：

```javascript
handler.methodName = function(msg, session, next) {
  // ...
}
```

参数含义与before filter类似。handler处理完毕后，如有需要返回给客户端的响应，可以将返回结果封装成js对象，通过next传递给后面流程。

### error handler

error handler是一个处理全局异常的地方，可以在error handler中对处理流程中发生的异常进行集中处理，如：统计错误信息，组织异常响应结果等。error handler函数是可选的，如果需要可以通过
```javascript
app.set('errorHandler', handleFunc);
```
来向pomelo框架进行注册，函数声明如下：

```javascript
errorHandler = function(err, msg, resp, session, next) {
  // ...
}
```
其中，err是前面流程中发生的异常；resp是前面流程传递过来，需要返回给客户端的响应信息。其他参数与前面的handler一样。

### component

pomelo 框架是由一些松散耦合的component组成的，每个component完成一些功能。整个pomelo框架可以看作是一个component容器，完成component的加载以及生命周期管理。pomelo的核心功能都是由component完成的，每个component往往有start，afterStart，stop等调用，用来完成生命周期管理。

### admin client, monitor, master

在对pomelo服务器进行管理的时候，有三个概念admin client， monitor， master。

* monitor运行在各个应用服务器中，它会向master注册自己，向master上报其服务器的信息，当服务器群有变化时，接收master推送来的变化消息，更新其服务器上下文。

* master运行在应用服务器中，它会收集整个服务器群的信息，有变化时会将变化推送到各个monitor；同时，master还接受admin client的请求，按照client发出的命令，执行对应的操作，如查询整个服务器群的状态，增加一个服务器等。

* client独立运行自己的进程，它会发起到master的连接，然后通过对master发出请求或者命令，来管理整个服务器群。目前工具[pomleo-cli](https://github.com/NetEase/pomelo-cli)就是这样的一个客户端。

### admin module

在pomelo中，module特指服务器监控管理模块，与component类似，不过在module中实现的是监控逻辑，比如收集进程状态等。用户在使用时，可以通过`application`的`registerAdmin`注册管理模块，实现用户自己定制的监控管理功能。每一个module中都会定义下面四种回调函数，不过都是可选的：
* masterHandler(agnet, msg, cb) 当有应用服务器给master发监控数据时，这个回调函数会由master进程进行回调，完成应用服务器的消息处理;
* monitorHandler(agent, msg, cb) 当有master请求应用服务器的一些监控信息时，由应用服务器进行回调，完成对master请求的处理;
* clientHandler(agent, msg, cb）当由管理客户端向master请求服务器群信息时，由master进程进行回调处理客户端的请求。
* start(cb) 当admin module，注册加载完成后，这个回调会被执行，在这里可以做一些初始化工作。

### plugin

plugin是pomelo 0.6加入的全新的扩展机制，一个plugin由多个component以及一些事件响应处理器组成。它提供了一种很灵活的机制来扩展pomelo。不仅可以提供component的功能，还可以对整个框架的全局事件作出响应处理。

小结
============

上面简要地介绍了pomelo中的一些术语，因为在下面的例子中，会涉及到这些术语，不至于当出现这些术语时一头雾水。下面我们就正式进入我们的例子，[获取源码并安装我们的例子应用](chat源码下载与安装 "chat源码下载与安装")。

在实际的应用中，我们往往需要在逻辑服务器处理请求之前需要对用户请求做一些前置处理，而当请求被处理后，又需要做一些善后处理，由于这是一种很常见的情形，pomelo对其进行了抽象，也就是filter。在pomelo中，filter分为before filter和after filter。在一个请求到达Handler被处理之前，可以经过多个before Filter组成的filter链进行一些前置处理，比如对请求进行排队，超时处理。当请求被Handler处理完成后，又可以通过一个after filter链进行一些善后处理。这里需要注意的是在after filter中一般只做一些清理处理，而不应该再去修改到客户端的响应内容，因为此时，对客户端的响应内容已经发给了客户端。

本例是一个聊天应用，在聊天室里，当有人说脏话时，往往需要进行屏蔽。我们在这里就以加一个脏话屏蔽的filter来示范如何使用pomelo的filter。具体的代码请切换到`tutorial-abuse-filter`分支，使用如下命令：

    $ git checkout tutorial-abuse-filter

Filter结构
================

Filter是一个对象，定义一个Filter的大致代码如下:

```javascript
var Filter = function (<args>) {
  // ....
};

Filter.prototype.before = function(msg, session, next) {
	// ...
}

Filter.prototype.after = function(err, msg, session, resp, next) {
 // ...
}

```

如果定义了before，那么就可以作为一个before filter使用，如果定义了after，就是一个after filter。

对于before filter来说，其有两个参数msg和session，这里msg可能是用户请求原始内容，也可能是经过了前面filter链处理后的内容。如果在后端服务器上，session在这里是BackendSession，如果在前端服务器上，则是FrontendSession，用户对其的直接修改都只会在整个请求处理链的后面处理过程中有效，而不会对前端的session有任何影响，更不会影响原始的session信息了。当然如果确实有需要修改session的话，比如绑定uid的话，可以通过BackendSessionService的相关调用达到目的。

在after中，err是当前面有错误的错误信息，resp是对客户端的相应内容。当定义好Filter后，通过application的filter，before或after调用将其挂到对应的逻辑服务器处理的处理链上。这是只是一个简单教程，不做深入探讨。


定义我们自己的Filter
=========================

我们这里需要的一个脏话过滤Filter，为了简单期间我们只对`fuck`进行过滤。在before filter里，如果用户发言里有`fuck`字眼，那么就将其替换为`****`,并在其session里增加一个标记。在after filter里，我们检查session的这个标记，如果是脏话，那么就将这个用户的名字记录下来，同样为了简单起见，我们将其记录的方式仅仅是打到console中。我们的abuseFilter 代码如下:

```javascript
// abuseFilter.js
module.exports = function() {
  return new Filter();
}

var Filter = function() {
};

Filter.prototype.before = function (msg, session, next) {
  if (msg.content.indexOf('fuck') !== -1) {
    session.__abuse__ = true;
    msg.content = msg.content.replace('fuck', '****');
  }
  
  next();
};

Filter.prototype.after = function (err, msg, session, resp, next) {
  if (session.__abuse__) {
    var user_info = session.uid.split('*');
    console.log('abuse:' + user_info[0] + " at room " + user_info[1]);
  }
  next(err);
};

```

在定义完filter后，我们需要把其配置到chat服务器中，在app.js中增加代码如下：

```javascript

// app.js
var abuseFilter = require('./app/servers/chat/filter/abuseFilter');
app.configure('production|development', 'chat', function() {
	app.filter(abuseFilter());
}

```

好了，让我们按照前面所讲的部分，重新运行我们的chat应用，在聊天内容里面输入what a fucking day，看看是不是已经被****替换了，效果图如下：

![abuse](images/abuse.png)

一些说明
=============

* 需要指出的是，这里使用filter来做脏话替换，可能不是很合理，但仅仅为了示例filter的使用，还是可以的。一般情况下，在before filter里，可以做一些请求排队，超时处理, 而在after filter里做一些清理记录的处理。比如，为了统计Handler的处理请求时间，可以在before filter里给session记录一个时间戳，在after filter里取出刚才的时间戳，跟当前时间做运算，就能得到Handler处理请求的时间。pomelo内置提供了几个filter，有toobusy，timeout等，这里不再深入。

* 一个filter里可以只定义before，可以只定义after，也可以两者都定义。application中与filter相关的调用为filter，after和before。如果一个filter既定义了before又定义了after，那么就可以调用filter，这样，application就会将其after和before都加载进去，否则，就只能调用after或者before了。

小结
==============

在这部分，我们使用了pomelo 提供的filter机制实现了我们聊天应用的脏话过滤。当然我们的实现非常得简陋而且并不一定很合理，但是仅仅是为了说明Filter的使用方式，还是可行的。下一步我们来使用[基于dict的route压缩](试试route压缩 "route压缩")来继续完善我们的聊天应用。

在实际编程中，网络带宽的有效数据负载率是一个值得考虑的问题。对于移动客户端来说，网络资源往往不是很丰富，为了尽可能地节省网络资源，往往需要尽大可能地增加数据包的有效数据率。

以我们的聊天应用为例，当客户端发起聊天时，需要指定处理其请求的服务器的路由信息，示例如下：

```javascript

pomelo.request('chat.chatHandler.send', 
  // ...
);

```
这个路由信息指出，处理这个请求的应该是chat服务器的chatHandler的send方法。当服务器给客户端推送消息的时候，同样也需要指明客户端的路由信息，在例子聊天应用中有onAdd，onLeave等。考虑当用户发起聊天的信息很短的时候，比如用户仅仅发了一个字，而我们在传输的时候一样要加上一个完整的路由信息，这样将造成实际传输中，有效数据率极低，网络资源被大量的额外信息浪费。最直接的想法就是缩短路由信息，对服务端的路由信息来说，由于当服务器确定后，其路由信息就确定了，对于客户端来说，虽然可以起很短的名字，但是很容易造成程序不可读。

针对这种情况，pomelo提供了基于字典的路由信息压缩。

* 对于服务端，pomelo会扫描所有的Handler信息
* 对于客户端，用户需要在config/dictionary.json中声明所有客户端使用的路由。

通过这两种方式，pomelo会拿到所有的客户端和服务端的路由信息，然后将每一个路由信息都映射为一个小整数，从1开始映射，累加。目前pomelo的路由信息压缩仅仅支持使用hybridconnector的方式，使用sioconnector的方式，暂不支持。在hybridconnector的实现中，如果使用了路由信息压缩，在客户端与服务器建立连接的握手过程中，服务器会将整个字典传给客户端，这样在以后的通信中，对于路由信息，将全部使用定义的小整数进行标记，大大地减少了额外信息开销。

chat中使用
===========

下面我们就将route压缩用到我们的chat示例中，具体的代码在分支`tutorial-dict`中，使用下面命令切换分支：

    $ git checkout tutorial-dict

首先看看客户端有哪些路由信息，我们把它放到config/dictionary.json里:

```javascript

// dictionary.json
[
  'onChat',
  'onAdd',
  'onLeave'
]

```

然后我们在connector配置选项里面增加useDict设置为true。

```javascript

app.configure('production|development','connector', function() {
  app.set('connectorConfig', {
    connector: pomelo.connectors.hybridconnector,
    heartbeat: 3,
    useDict: true // enable dict
  });
});

app.configure('production|development','gate', function() {
  app.set('connectorConfig', {
    connector: pomelo.connectors.hybridconnector,
    useDict: true // enable dict
  });
});

```

* 好了，现在我们就已经开启了pomelo的路由压缩，现在的所有的数据包的路由信息都变成小整数了。
* 对于dictionary中添加的客户端路由，会使用路由压缩。如果有客户端的推送路由没有加入到dictionary中，会怎么样呢？不用怕，对于在dictionary中找不到的路由信息，pomelo还是会使用原来不压缩的路由。

小结
=========

到目前位置，我们客户端与服务器之间使用的消息传输格式一直都是json。实际上，虽然json很方便，但是由于其还带了一些字段信息，在客户端和服务端数据包格式统一的情况下，这些字段信息是可以省略的，可以直接传输具体的消息，也就是说不再以字符串作为通信格式了，直接发送有效的二进制数据将会更好地减少额外开销，下面我们会使用pomelo提供的[protobuf 实现](Protobuf压缩 "Protobuf压缩")应用到我们的聊天应用中，以使得我们的应用更完善。


在多进程应用中，进程间通讯是不可或缺的。在pomelo中，借助javascript的语言特性，实现了对开发者非常友好的一个rpc框架。下面，我们将在我们的chat应用中，实践一个rpc调用。为了保持简单，而又能说明问题，我们“画蛇添足”地实现一个时间服务器，当gate服务器接受到用户的查询请求时，我们让gate服务器向时间服务器请求当前的时间，并将其打印在console上。当然这个例子没有啥实际意义，你也可以认为它有意义，因为一个统一的时间服务器可以提供统一的时间信息。这里仅仅是为了示例rpc调用的使用方式，并向用户展示pomelo中rpc调用的方便性。

实际上在我们的聊天应用中，已经有了rpc调用的实现，那就是当有用户连接connector或者离开时，connector会向chat发起rpc，chat会根据相应的用户离开和加入，对应操作其Channel信息。由于在前面我们并没有很详细地对其进行分析，所以干脆重新实现一个全新的rpc，同时，我们也可以展示如何在pomelo应用中增加一个服务器类型。

chat中增加rpc
==============

下面将给我们的聊天应用增加一个rpc调用和一个time类型的服务器，具体的代码在分支 `tutorial-rpc` 上，使用如下命令切换分支:

    $ git checkout tutorial-rpc

首先，我们在servers下建立时间服务器类型time，建立服务名称timeHandler,获取时间方法getCurrentTime(arg1, arg2, cb)，其中arg1, arg2没有实际意义，纯属于示例的目的，在servers/time/remote/timeRemote.js 里面，定义方法：

```javascript

// timeRemote.js
module.exports.getCurrentTime = function (arg1, arg2, cb) {
  console.log("timeRemote - arg1: " + arg1+ "; " + "arg2: " + arg2);
  var d = new Date();
  var hour = d.getHours();
  var min = d.getMinutes();
  var sec = d.getSeconds();
  cb( hour, min, sec);
};

```

这里，首先将客户端传来的两个参数打印到console上，然后获取到当前的时间，然后取出其时分秒信息，将其发到客户端。
客户端的调用：

```javascript

// gateHandler.js
var routeParam = Math.floor(Math.random()*10);
app.rpc.time.timeRemote.getCurrentTime(routeParam, arg1, arg2,  function(hour, min, sec) {
  // ...
});

```

在客户端的rpc调用中，getCurrentTime的第一个参数是用来做路由计算的，arg1, arg2...为调用参数示例，这里的参数arg1, arg2实际上没有啥实际用途，仅仅是为了示例，我们在远程调用的服务端也仅仅是将其打印到console而已。当然实际的rpc调用的时候，就可以使用多个参数，从客户端给服务端传参数。最后的回调应与服务端最后的回调签名保持一致。对于routeParam，我们在这里不再使用session，而是使用一个0-10之内的随机整数，然后直接让其与服务器的个数做hash，得到一个具体的时间服务器。

当有多个time服务器的时候，我们还要为每一次对time服务的请求配置相应的路由，rpc路由函数的第一个参数为rpc调用时的第一个参数，对于本例来说，就是随机数routeParam。在pomelo中很多时候是使用session作为路由参数的，这里示例了一个不一样的路由参数，具体示例代码如下：

```javascript

// app.js
var router = function(routeParam, msg, context, cb) {
  var timeServers = app.getServersByType('time');
  var id = timeServers[routeParam % timeServers.length].id;
  cb(null, id);
}

app.route('time', router);

```

这样我们就定义了对time服务器的路由函数。路由函数的参数routeParam就是rpc调用时的第一个参数，msg中封装了rpc调用的详细信息，包括namespace，servertype，等等。context是rpc客户端的上下文，一般由全局的application充当,cb是一个回调，第一个参数是当有错误发生时的错误信息,第二个参数是具体的服务器id。

在服务器配置config/servers.json中增加time服务器如下：

```javascript

"time":[
  {"id": "time-server-1", "host":"127.0.0.1", "port" : 7000},
  {"id": "time-server-2", "host":"127.0.0.1", "port" : 7001}
]

```

好了，这样就为聊天应用增加了一个时间服务器，时间服务器提供一个远程时间，当gate接收到查询请求时，会向time服务器发一个请求，time服务器会为其提供一个时间。gate服务器会向console打印出其得到的远程时间，time服务器会向console打印出gate发起rpc请求时提供的两个参数arg1,arg2,虽然这两个参数没有啥实际意义，但是还是演示了如何在远程调用中传参数。最后的两个回调函数，我们保持了回调函数的签名一致即可。回调函数可以有多个参数，说明我们的rpc调用实际上是可以返回多个结果的。

一些说明
============

* 你可能注意到了我们在time服务器的timeRemote.js和chat服务器的chatRemote.js中，定义远程调用方式的不同了。在timeRemote.js中，直接在``module.exports``上面挂载``getCurrentTime``，而在chatRemote.js中，则是另一种方式，示例如下:

```javascript

// chatRemote.js
module.exports = function(app) {
	return new ChatRemote(app);
};

// timeRemote.js
module.exports.getCurrentTime(arg1, arg2, cb) {
  // ...
};

```
实际上这两种方式都是可以的，pomelo在加载具体的remote的时候，如果发现加载到的不是一个对象而是一个函数，那么将认为其是一个工厂方法，它将使用一个全局的上下文（一般是唯一的一个application实例）作为参数，调用这个函数，并使用其结果。chatRemote就是使用这种方式，最终加载到的remote对象实际上是一个ChatRemote对象; 而对于timeRemote来说，require调用返回的就是一个对象，这个对象有一个方法getCurrentTime，所以这个时候，就不需要进行一次函数调用了。

当remote需要当前的application实例的时候，往往可以使用第一种chatRemote的那种方式，而当remote跟app完全没关系时，也可以使用timeRemote的这种实现方式，这在pomelo中是没有差别的。

不仅仅是remote，对于handler也是一样，也就是说定义handler的时候也可以使用这两种方式中的一种，只不过到目前为止，我们这个例子中使用的都是类似于chatRemote中的那种实现方式。

* 当前端服务器接受客户端请求，将请求路由给后端服务器时，pomelo使用的是发起一个系统级远程调用的方式，这个时候会使用session作为rpc请求的路由参数，这也是我们看到的前面在给chat配置路由的时候，路由函数的第一个参数总是session。在time中，我们使用了一个随机整数作为路由参数，因此time的路由函数的第一个参数也就是这个随机整数了。实际上pomelo的rpc框架对于路由参数的使用是没有限制的，并不仅限于一直使用session。

* rpc调用的返回值是通过回调的形式获得的，回调函数也就是我们上面看到的rpc调用的最后一个参数。这个回调函数可以有多个参数，表示远程调用可以返回多个值，在我们这个例子中，返回了时分秒三个值。

* 0.8版本以后，当进行rpc调用的时候，可以跳过路由计算而直接将调用发送到一个具体的服务器或者广播到一类服务器的调用方式，代码示例如下：
```javascript
// route
var routeParam = session;
app.rpc.area.playerRemote.leaveTeam(routeParam, args..., cb);

// to specified server 'area-server-1'
app.rpc.area.playerRemote.leaveTeam.toServer('area-server-1', args..., cb);

// broadcast to all the area servers
app.rpc.area.playerRemote.leaveTeam.toServer('*', args..., cb);
```
小结
==========

在这部分，我们给聊天应用增加了一个time服务器并实现了一个rpc调用，并对pomelo的rpc调用进行了一些说明。下一步，我们将[增加一个component](给pomelo加个组件 "增加组件")。

pomelo的核心是由一系列松耦合的component组成，同时我们也可以实现我们自己的component来完成一些自己定制的功能。对于我们的chat应用，我们尝试给其增加一个component，目的是展示如何增加一个component，以及component的生命周期管理，而不会特别关注这个component的实际功能。我们现在就给其增加一个component HelloWorld，这个component仅仅在master服务器上加载运行,在master服务器的话，它将每隔一段时间在console上打印出来一个HelloWorld，具体的时间间隔由opts配置来指定。

chat中应用
=============

具体的代码在分支`tutorial-component`上，使用如下命令切换分支：

    $ git checkout tutorial-component

* 首先，在app下建立components/HelloWorld.js文件, 大致代码如下：

```javascript

// components/HelloWorld.js
module.exports = function(app, opts) {
  return new HelloWorld(app, opts);
};

var DEFAULT_INTERVAL = 3000;

var HelloWorld = function(app, opts) {
  this.app = app;
  this.interval = opts.interval | DEFAULT_INTERVAL;
  this.timerId = null;
};

HelloWorld.name = '__HelloWorld__';

HelloWorld.prototype.start = function(cb) {
  console.log('Hello World Start');
  var self = this;
  this.timerId = setInterval(function() {
    console.log(self.app.getServerId() + ": Hello World!");
    }, this.interval);
  process.nextTick(cb);
}

HelloWorld.prototype.afterStart = function (cb) {
  console.log('Hello World afterStart');
  process.nextTick(cb);
}

HelloWorld.prototype.stop = function(force, cb) {
  cosole.log('Hello World stop');
  clearInterval(this.timerId);
  process.nextTick(cb);
}

```

我们看到每一个component一般都要定义start，afterStart，stop这些hook函数，供pomelo管理其生命周期时进行调用。对于component的启动，pomelo总是先调用其加载的每一个component提供的start函数，当全部调用完后，才会去调用其加载的每一个component的afterStart方法，这里总是按顺序调用的。在afterStart中，一些需要全局就绪的工作可以放在这里完成，因为调用afterStart的时候，所有component的start已经调用完毕。stop用于程序结束时对component进行清理时使用。虽然我们这个例子非常简单，但是足以说明如何在pomelo中定制自己的component，并使用。我们在HelloWorld的start里面启用了一个定时器，每隔一段时间就向console打印一个HelloWorld。然后在stop里关闭它。

* 然后，我们让master服务器来加载我们的这个component，具体代码如下：

```javascript
// app.js
var helloWorld = require('./app/components/HelloWorld');

app.configure('production|development', 'master', function() {
  app.load(helloWorld, {interval: 5000});
});

```
好了， 我们通过实现一个简单的component，明白了如何实现自己的定制component，当然这个component很简单，也没有啥实际意义，但是它是一个完整的component，有完整的生命周期管理，我们通过这个例子已经了解到了component的创建以及加载。

一些说明
==========

* 这里定义的HelloWorld component中，往外导出的是一个工厂函数，而不是一个对象。当app加载component时，如果是一个工厂函数，那么app会将自己作为上下文信息以及后面的opts作为参数传给这个函数，使用这个函数的返回值作为component对象。同样，也可以直接给module.exports赋予一个对象，那样的话，就可以直接使用而不用调用工厂函数，不过这样的话丧失了使用app和具体配置参数， 不够灵活，因此，使用工厂方法的方式是一个好选择。

* 对于start和afterStart的执行，pomelo总是会先按顺序执行完所有component的start后，才会按顺序执行所有component的afterStart，因此可以在afterStart里执行一些需要其他component执行了start后才可以执行的逻辑。

* 实际上，pomelo应用的整个运行过程可以认为是管理其component的生命周期过程，pomelo的所有功能都是通过其内建的component来实现的。用户可以轻松地定制自己的component，然后将其load进去，这样就很轻松地实现了对pomelo的扩展。

小结
===========

在这部分，我们给聊天应用“画蛇添足”般地添加了一个HelloWorld component，使得可以更好地理解如何定制自己的component，并加载它。pomelo的框架非常灵活，有很好的可扩展性，从我们的例子中，我们可以看出，可以很容易地对pomelo进行扩展。pomelo不仅可以扩展component，pomelo还提供了一个灵活的可扩展的服务器监控管理框架，[下一步](增加admin-module "增加admin-module")，我们将给我们的聊天应用增加一个监控模块，让应用服务器自动向master上报自己的本地时间，以此来示例如何在pomelo中定制自己的监控管理模块。

一个pomelo的应用，一般是由一个服务器群来支持，对于这些应用服务器的管理以及监控就显得尤为重要。比如监控这些应用服务器的进程状态，系统状态，杀死某个服务器等等。

对服务器的监控和管理有三个主体：master，monitor，client。服务器的管理和监控由master服务器加载的master component和普通的应用服务器加载的monitor component，还有服务器管理客户端共同完成，下面的叙述中将不加区分地使用monitor与应用服务器，master与master服务器。

master负责收集所有服务器的信息，下发对服务器的操作指令。monitor负责上报服务器状态，并对master的命令作出反应。client是第三方监视的客户端，它注册到master上，通过给master发请求获得服务器群信息，或者给master发指令，管理操作应用服务器群。pomelo中内建实现并使用了console和watchdog这两个admin module，它们是pomelo核心的一部分,这里不再详述。

由于对于具体的应用来说，需要监控和管理的信息也是各不相同的，因此，pomelo并没有实现固定的监控模块，而是提供了一个可插拔的监控框架机制，用户只需要定义一个监控模块所需要的回调方法，并完成相应的配置即可。

一组相关的供不同主体调用的回调函数构成一个admin module，一个admin module中一般包括四个回调方法，monitorHandler，masterHandler，clientHandler, start。其中monitorHandler是monitor收到master的请求或者通知时由monitor回调，masterHandler是master收到monitor的请求或者通知时回调，clientHandler是master收到client的请求或通知时回调的, start是当admin module加载完成后，用来执行一些初始化监控时调用。

为了演示admin module的用法，我们将给聊天应用增加一个监控模块，我们让monitor每隔5秒钟向master上报一下自己的当前时间。当然，上报时间没有太多的实际意义，不过为了保持示例的简单化，选择上报时间还是可取的。实际使用中，可以上报任何信息，使用方式都是与上报时间的方式是一样的，这里使用上报时间仅仅是为了使得示例尽可能简单，更容易抓住如何使用admin module。

chat中使用
=============

下面我们将给我们的聊天应用增加一个监控管理模块，具体的代码在分支`tutorial-admin-module`上，使用如下命令切换分支：
  
    $ git checkout tutorial-admin-module

* 首先，我们在app目录下建立文件modules/timeReport.js, 在其中定义monitorHandler，masterHandler和clientHandler，代码如下：
```javascript

module.exports = function(opts) {
    return new Module(opts);
}

var moduleId = "timeReport";
module.exports.moduleId = moduleId;

var Module = function(opts) {
    this.app = opts.app;
    this.type = opts.type || 'pull';
    this.interval = opts.interval || 5;
}

Module.prototype.monitorHandler = function(agent, msg, cb) {
    console.log(this.app.getServerId() + '  ' + msg);
    var serverId = agent.id;
    var time = new Date().toString();

    agent.notify(moduleId, {serverId: serverId, time: time});
};

Module.prototype.masterHandler = function(agent, msg) {
    if (!msg) {
      var testMsg = 'testMsg';
      agent.notifyAll(moduleId, testMsg);
      return;
    }

    console.log(msg);
    var timeData = agent.get(moduleId);
    if (!timeData) {
        timeData = {};
        agent.set(moduleId, timeData);
    }
    timeData[msg.serverId] = msg.time;
};


Module.prototype.clientHandler = function(agent, msg, cb) {
    cb(null, agent.get(moduleId));
}

```

* 这里我们没有定义start回调，因为我们这里用不到。在定义完上面的admin module后，需要将其注册到我们的应用中，使用Application.registerAdmin调用，在app.js中增加如下代码：

```javascript

var timeReport = require('./app/modules/timeReport');
app.registerAdmin(timeReport, {app: app});

```

这里registerAdmin可以接收两个或三个参数，如果是三个参数的话，第一个必须是字符串来指定moduleId。如果是两个参数的话，moduleId将使用第一个参数，也就是module的工厂函数的moduleId属性。这里由于我们给timeReport定义了moduleId属性，因此我们就省略掉了第一个moduleId参数了。最后一个参数是配置选项，可以配置监控数据获取是pull还是push方式，以及获取周期。在我们这个例子中，由于注册时没有传入任何关于type和interval的配置，将使用默认值，也就是使用拉模式，每隔5秒获取一次数据。


一些说明
=========

* 在导出一个module的时候，一般需要指定一个moduleId，在这里，我们指定的moduleId是`timeReport`。当然我们如果这里不指定moduleId的话，在调用Application.registerAdmin的时候再指定moduleId也是可以的。

* 一个module有两个属性很重要，type和interval，type指出的是数据所采用的方式，有两种pull和push。pull方式是让master定时给monitor发请求，monitor给其上报信息。push的方式则是monitor定时上报自己的信息。interval就是这个信息上报的时间周期了。我们例子中使用的是方式通过opts传入，如果opts中没有配置的话，默认使用pull方式，上报周期为5秒，而实际上，我们就是使用了这样的两个参数值，即使用pull方式，让master主动拉数据，每5秒拉一次。

* 还有一个要注意的地方是masterHandler的实现，可能会让人感到迷惑。实际上，由于使用pull的方式，masterHandler会在两种情况下被回调，一种是每隔5秒产生的一次拉数据事件，一种是monitor向master上报信息。这两种情况，可以通过参数msg区分。

    - 如果是定时器产生的周期性的拉数据事件导致的回调，此时msg参数是undefined，因此此时只是简单的调用notifyAll，参数moduleId使用来区分到底是哪个监控模块；testMsg参数在这里仅仅用来示例如何传参,在monitorHandler中也仅仅把其打印到console上而已，实际应用中，可以用其传递更有意义的参数；

    - 如果是monitor在收到master的通知后，上报自己的时间信息的话，此时msg将会是一个对象，这个时候，master将这个时间值打印到console，并缓存其值，当然这个值没什么意义，仅仅是为了示例。因此这段代码通过对msg的判断区分了这两种情况。

    - 实际应用中，也经常使用判断msg来区分两种情况的方式。考虑另一种情况，假如使用的不是pull方式，而是push方式的话，那么monitor将会遇到两种情况，与master类似，一种是定时器的周期事件，一种是master给其发了通知或请求，此时也可以通过判断msg进行两种情况的区分，只不过此时将会在monitorHandler中进行判断了。关于这种使用push方式并在monitorHandler中通过判断msg的值进行区分两种情况的实现方式，读者可以自行尝试。

* monitorHandler的实现中，当收到master的通知后，取出了master传来的参数，这里的参数就是testMsg，实际应用中可以使用更复杂的更有实际意义的参数。然后通过对参数进行分析，执行相应的逻辑。这里的逻辑很简单，就是获取自己当前的时间，然后通知给master。

* clientHandler是当有第三方监控客户端给master发请求时，由master进行回调的。为了保持简单，我们这里不再对client做过多的介绍,在开发指南部分会有详细的介绍。

小结
==========

在这部分里，我们使用了pomelo提供的监控管理框架完成了monitor向master上报其本地时间的功能。实际上，通过定制自己的admin module可以实现上报任何我们需要的上报的数据。比如，在实际应用中，connector服务器可以向master报告登录到其服务器上的用户信息，monitor可以向master上报其进程相关的信息等等。在pomelo-admin中还实现了另外几个admin module，这些admin module可以通过对Application调用`app.enable('systemMonitor')`完成开启，这里不再详述，可以直接阅读相关代码。到此为止，我们基本上就介绍完了pomelo的所有基本功能，下面会有一个简单的[总结还有一些没有涉及到的内容](总结 "总结")。

到这里为止，pomelo的基本核心特性都已经进行了示例，虽然都没有很深入。还有一些前面教程没有涉及到的地方，我们把它放到这里进行一些简单的介绍。

未涉及到的
==========

### 服务器监控与管理

pomelo提供了一个命令行工具，通过这个命令行工具，可以进行初始化一个pomelo项目，启动一个pomelo项目，查看当前已经启动的服务器信息，以及关闭服务器群。从pomelo 0.6.0开始，使用这个工具在进行服务器的查看以及关闭时，将需要一个身份验证,需要提供用户名和密码，其命令行格式如下：
    
    $ pomelo [list|stop|kill] [-u <username>][-p <password>]

如果不提供用户名和口令的话，会使用默认的，默认的用户名和口令都是admin。目前命令行工具仅仅保留了初始化项目，启动项目，关闭项目，以及查看启动的服务器信息。更多的服务器管理操作可通过使用[pomelo-cli](Pomelo-cli使用)来完成，pomelo-cli提供了强大的服务器管理功能，支持动态增加关闭服务器，支持更详细的服务器信息监控等。

### 插件机制

pomelo提供了基于插件的扩展机制，一个插件中可以包含一些相关的 component以及对pomelo事件的响应处理，关于插件的更多介绍，请参阅[plugin的参考文档](https://github.com/NetEase/pomelo/wiki/plugin%E6%96%87%E6%A1%A)。

### IDE选择

在开发中，往往需要一款顺手的IDE。对于pomelo来说，[这里](https://github.com/NetEase/pomelo/wiki/%E4%BD%BF%E7%94%A8-WebStorm-IDE-%E8%B0%83%E8%AF%95-Pomelo-%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F)详细介绍了一款javascript的IDE的使用。

### 服务器的配置

在配置服务器信息的时候，我们看到，对于前端服务器，要给frontend配置为true，同时除了要配置rpc使用的端口port外，还要配置供客户端连接的端口clientPort。对于后端的服务器，则仅仅需要配置rpc调用的端口即可,后面的开发指南部分会有详细的介绍。

### connector的选择

本教程中与客户端的连接使用了hybridconnector，实际上pomelo的connector的是可定制的，目前还支持基于socket.io的版本，基于socket.io版本的chat例子在[这里](https://github.com/NetEase/chatofpomelo)。

### 多客户端支持

本教程中，客户端的选择了基于websocket的web客户端，理论上pomelo可以支持任何客户端，下面有部分chat客户端demo的链接:

* unity客户端的chat:
 [socket 版本](https://github.com/NetEase/pomelo-unitychat-socket) 
 [socket.io 版本](https://github.com/NetEase/pomelo-unitychat)

* Flash客户端的chat Demo:
  [PomeloFlashDemo](https://github.com/mani95lisa/PomeloFlashDemo)

* Android客户端

[https://github.com/NetEase/pomelo-androidchat](https://github.com/NetEase/pomelo-androidchat)

* IOS客户端

[https://github.com/NetEase/pomelo-ioschat](https://github.com/NetEase/pomelo-ioschat)

* cocos2d-x客户端

[https://github.com/NetEase/pomelo-cocos2dchat](https://github.com/NetEase/pomelo-cocos2dchat)

总结
=========

通过chat这个例子，我们从最初的chat例子开始，一步一步对其进行更改，展示了pomelo的一些特性的用法，这里都没有涉及特别深，只是让用户明白如何去增加一个filter，如何去增加一个rpc调用，如何启用route压缩和使用protobuf编码，如何定制自己的 component并让pomelo加载，如何定制一个admin module等。这些功能都是pomelo的核心功能。

通过这些个例子的学习，相信会对pomelo有更详细的了解，更加了解pomelo提供的功能，以及具体的使用方式。同时这个例子也可以作为用户使用pomelo的一个简单参考，它基本上涉及到了pomelo的所有方面。


下面将呈现pomelo框架中，较为核心的非正规的类关系图,先来看一下对类图的一些说明:

* 由于javascript中实际上没有类的概念，有的只是一个pseudo-class的概念，因此这个类关系图中的类并不是与实际的pomelo框架中所定义使用的pseudo-class一一对应。比如，HandlerFilter，在我们这个类图中，它是一个抽象类，是所有HandlerFilter的基类。而在pomelo框架中，往往只是定义有after和before方法的类即可，而不用关心其所继承的抽象类。

* 在类图中，所有的组件，我们都冠以Co进行命名，以表示其是一个组件。

* 在类图中，定义了一个RawSocket，是把其作为了对通信层socket的一个抽象。在实际应用中，可能是WebSocket，TCP的socket或者socket.io等等。所有与RawSocket相关的类，都是表示这个类在实际应用中会直接参与通信，无论是与客户端通信，还是与其他的服务器通过rpc进行通信。

下面是我们的类图：

![pomelo框架类图](images/pomelo.png)

下面对类图进行一些简要的分析:

* 整个框架的核心为两个类Pomelo和Application,Application实例由Pomelo创建。Pomelo实际上由一系列的组件以及一个全局的上下文Application组成。

* 所有的以Co开头的都是相应的组件，他们都是抽象类Component的子类，每一个组件都完成其相应的功能,不同的服务器将加载不同的组件。这个类图里面的组件都是pomelo内建的组件，它们是为了完成pomelo的核心功能不可获缺的组件，用户可以通过定义自己的组件对pomelo进行扩展。

* 为了更好地展示pomelo中使用的各个类之间的关系，这个类图中展示的相关类，不仅仅是pomelo这一个项目中定义的类，还包括[pomelo-admin](https://github.com/NetEase/pomelo-admin)和[pomelo-rpc](https://github.com/NetEase/pomelo-rpc)中的相关类。

* 从类图中可以看出，与通信相关的类有MasterAgent，MonitorAgent；MailBox，Acceptor以及connector。实际上，MasterAgent与MonitorAgent是对等的，MasterAgent充当”服务端“，MonitorAgent充当“客户端”，MasterAgent会监听master配置的port，MonitorAgent会发起连接，它们之间的通信完成master服务器对应用服务群的监控和管理。MailBox和Acceptor的关系也与此类似，只不过它们之间的通信完成了框架的rpc调用。connector是用来接受客户端连接的，因此connector会监听clientPort。





我们知道，pomelo的应用程序执行的全部过程，就是对其相应组件的生命周期的管理，实际的所有逻辑功能均有pomelo组件提供。pomelo内建提供了十多个组件，这些组件适用于不同的服务器，提供不同的功能。有些组件提供的功能比较复杂，有些则比较简单。下面我们将以提供的功能为主线来阐述pomelo提供的内建组件。

### master组件

master组件仅仅由master服务器加载，它主要的功能包括启动所有的应用服务器、管理和监控所有的应用服务器和接受管理客户端的请求与响应。

在master组件的start方法里，会根据用户提供的服务器配置信息，启动用户配置的所有的具体应用服务器。

当master组件start结束后，他将开启一个socket监听端口，接受应用服务器和监控客户端的连接和注册，收集应用服务器上报的监控信息，给应用服务器推送一些消息，并对管理客户端发出的管理请求给予响应。管理客户端如[pomelo-cli](Pomelo-cli使用)可能发出的请求包括查看某个服务器进程状态，增加一个服务器，停掉一个服务器等。以增加一个服务器为例，当管理客户端发出增加服务器请求时，会提供相应的服务器参数，如服务器类型，主机ip，开启的端口等。此时，master组件接受后，会启动相应的服务器，并将新增加的服务器信息广播通知给其他已经启动的服务器。

master组件无配置项。

### monitor组件

monitor组件由所有的包括master服务器在内的服务器都会加载，它的主要功能就是与master建立连接进行通信，从而对整个应用服务器群进行管理和监控。master服务器本身也会加载monitor服务器，因为master服务器也会收集其本身自己的监控信息。

可以认为monitor服务器与master服务器是对等组件，monitor会通过master接受一些命令，比如关闭整个服务器等。对于一些周期性监控的信息，pomelo提供了两种收集方式，即pull方式和push方式。pull方式要求master周期地去与monitor通信，拉取相应的监控信息；push方式，则是由monitor周期地主动地向master报告其监控信息。

monitor组件无配置项。

### connector组件

connector组件是一个重量级的组件，它会依赖于session组件，server组件,pushScheduler组件和connection组件。connector组件仅仅被前端服务器加载，它主要用来管理客户端的连接。connector组件会加载底层的connector，创建端口监听，绑定事件响应。当有客户端连接请求时，connector组件会请求session组件，获得当前连接的session，如果session组件中没有相应的session的话，session组件会为这个新连接创建新的session，并维护相应的连接；然后connector组件还会向connection组件上报连接信息，供统计使用；最后，将拿到的session以及客户端的请求，一起抛给server组件，由server组件进行请求处理。当server组件处理完请求后，又会通过connector组件将响应返回给客户端。在返回响应给客户端的时候，connector组件做了一个缓存选择，这个缓存实现依赖于pushScheduler组件，也就是说connector组件并不是直接将相应发给客户端，而是将响应给pushScheduler组件。pushScheduler组件根据相应调度策略，可能不缓存直接通过session组件维护的连接，将响应发出去，也可能进行缓存，并按时flush。这是可以配置的。

connector组件支持如下配置项:
* connector: 底层使用的通信connector，不配置的话，会默认使用sioconnector;
* useProtobuf: 目前仅仅支持connector配置使用hybridconnector的情况，配置其为true，将开启消息的protobuf功能；
* useDict： 目前仅仅支持connector配置使用hybridconnector的情况，配置其为true时，将会开启基于字典的路由消息压缩；
* useCrypto： 目前仅仅支持connector配置为hybridconnector的情况，配置其为true时，将会启用通信时的数字签名；
* encode/decode： 消息的编码解码方式，如果不配置的话，将会默认使用connector配置中，底层connector提供的相应的编码解码函数。
* transports：这个配置选项是用于sioconnector的，因为socket.io的通信方式可能会有多种，如websocket，xhr-polling等等。通过这个配置选项可以选择需要的方式。

配置connector组件，通过调用如下方式进行:

    app.set('connectorConfig', opts);

### session组件

session组件跟connector相关，也是仅仅被前端服务器加载，为sessionService提供一个组件包装, 加载session组件后，会在app的上下文中增加`sessionService`，可以通过`app.get('sessionService')`获取。它主要用来维护客户端的连接信息，以及生成session并维护session。如果与经典TCP进行类比的话，那么session中维护的连接就可以粗略地认为就是`TCP服务器端accept返回的socket句柄`。一个连接与一个session对应，同时session组件还维护具体登录用户与session的绑定信息。一个用户可以有多个客户端登录，对应于多个session。当需要给客户端推送消息或者给客户端返回响应的话，必须通过session组件拿到具体的客户端连接来进行。

session组件支持如下配置项:
* singleSession： 如果这个配置项配置为true的话，那么将将不允许一个用户同时绑定到多个session，在绑定用户一次后，后面的绑定将会失败。


配置session组件，通过调用如下方式进行:
   
    app.set('sessionConfig', opts);

### connection组件

connection组件是一个功能相对简单的组件，也是仅仅被前端服务器加载,为connectionService提供一个组件包装,他主要进行连接信息的统计,connector组件接收到客户端连接请求以及有客户端离线时，以及用户登录下线等等情况，都会向其汇报。

connection组件无配置项。

### server组件
 
server组件也是一个功能比较复杂的组件，它被除master外的服务器加载。server组件会加载并维护自身的Filter信息和Handler信息。server组件会从connector组件的回调里获得到相应的客户端请求或者通知，然后会使用自己的before filters对其消息进行过滤，再次调用自己的相应Handler进行请求的逻辑处理，然后将响应通过回调的方式发给connector处理。最后调用after filters进行一些清理处理。

当然，如果客户请求的服务本来就是前端服务器提供的话，会是上面的那种处理流程。如果客户请求的服务是后端服务器提供的服务的话，则将不是上面的那种处理流程，此时会出现sys rpc调用。前面那种前端服务器自己处理的情况具体调用为doHandle，而发起rpc调用的情况则为doForward。这两种处理流程的不同点是，对于自身的请求，调用自己的filter-handler链进行处理，对于不是前端服务器自己提供的服务，则是发起一个sys rpc，然后将rpc调用的结果作为响应，发给connector进行处理。关于这个rpc调用则是pomelo内建的msgRemote实现的。

对于后端服务器来说，其客户请求不是直接来源于真实的客户端，而是来源于前端服务器对其发起的sys rpc调用，这个rpc调用的实现就是pomelo内建的msgRemote，在msgRemote的实现里，会将来自前端服务器的sys rpc调用请求派发给后端服务器的server组件，然后后端服务器会启用filter-handler链对其进行处理，最后通过rpc调用的返回将具体的响应返回给前端服务器。

在前端服务器将客户端请求向后端服务器分派时，由于同类型的后端服务器往往有很多，因此需要一个路由策略router，一般情况下用户通过Application.route调用为后端服务器配置router。

server组件无配置项。

### pushScheduler组件

pushScheduler组件也是一个功能较为简单的组件，它仅仅被前端服务器加载，与connector组件的关系密切。当connector组件收到server组件的对客户端请求的响应后，connector并不直接将此响应返回给客户端，而是将这个给客户端发送响应的操作调度给scheduler组件。pushScheduler组件完成最后通过session组件拿到具体的客户端连接并将请求的响应发送给客户端的任务。因此，通过pushScheduler组件可以对发给用户的响应进行缓冲，从而提高通信效率。pomelo实现了两种调度策略，一种是不进行任何缓冲，直接将响应发送给客户端，一种是进行缓冲，并定时地将已缓冲的响应发送给对应的客户端。

pushScheduler配置项:
* scheduler： scheduler组件的具体调度策略配置，默认的是直接将响应发给客户端，同时pomelo还提供了有缓冲并且定时刷新的调度策略。用户也可以自定义自己的调度策略。

配置pushScheduler组件，通过调用如下:

    app.set('pushSchedulerConfig', opts);

如果要启用使用缓冲的scheduler的话，可以在app.js中增加:

    app.set('pushSchedulerConfig', {scheduler: pomelo.pushSchedulers.buffer, flushInterval: 20});

flushInterval是刷新周期，默认为20毫秒。

### proxy组件

proxy组件是一个重量级的组件，它被除master外的所有服务器加载。proxy组件会扫描具体应用服务器的目录，抽取其中的remote部分，由于javascript语言的动态性，可以很轻易地获得到remote中的关于远程调用的元信息，生成stub，并将这些调用都挂到app.rpc下面，当用户发起rpc调用时，proxy组件会查看其扫描到的stub信息，以此决定此远程调用是否合法。同时，proxy又会创建一个RpcClient，当发起远程调用时，负责与远端的remote进行通信，并得到远程调用的结果供调用者使用。当进行远程调用时，由于同类型的远程服务器可能有多个，所以这里同样需要配置相应的router。

proxy的配置项： 
* cacheMsg, 配置cacheMsg为true的话，将开启rpc调用时的对消息的缓冲，而不是直接一旦有rpc请求就发出。
* interval, 与配置参数cacheMsg配合使用，设置flush缓存的周期
* mailBoxFactory, rpc底层实现需要的，用户可以定义自己的mailBoxFactory,我们将在rpc原理里面详述。

另外，可以开启rpc的调用日志，通过如下的调用:

    app.enable('rpcDebugLog');

配置proxy使用：

    app.set('proxyConfig', opts);

### remote组件

remote组件是与proxy组件对等的组件，它用来提供rpc调用服务。rpc组件完成对当前服务器的remote的加载，并开启监听端口，等待rpc客户端的连接及相应的rpc调用。当接收到具体的调用请求时，会根据调用请求中描述的调用请求信息，调用相应的remote中的相应方法。然后再将具体的处理结果返回给rpc客户端。rpc服务端还支持对调用请求的filter，也就是说跟server组件处理客户端请求一样，rpc服务端处理具体请求时也会使用filter-remote链进行处理。

remote组件配置项:
* cacheMsg, 与proxy组件的含义相同
* interval， 与proxy组件的含义相同
* acceptorFactory, rpc底层实现需要的,可以认为跟proxy配置中的mailBoxFactory是对等的，我们将在rpc原理里面详述。

跟proxy组件一样，用户可以开启rpcDebugLog来得到所有的rpc调用过程的日志。
配置remote组件使用：

    app.set('remoteConfig', opts);

### dictionary组件

dictionary组件是一个可选组件，不会被默认加载，只有当connector组件的配置中开启了useDict的时候，此组件才会被加载。此组件会遍历所有handler的route字符串，还会从config/dictionary.json中读取客户端的route字符串，然后对这些字符串进行编码，给予每一个路由赋予一个唯一的小整数，实现route信息压缩，当客户端与前端服务器通信时需要路由信息时，将不会再使用很长的那个字符串，而仅仅使用一个小整数。

dictionary的配置项:
* dict, 客户端路由字符串文件的位置，默认使用的是config/dictionary.json
配置dictionary组件使用:

    app.set('dictionaryConfig', opts);

### protobuf组件

protobuf组件也是一个可选组件，不会被默认加载，只有当connector组件的配置中开启了useProtobuf的时候，此组件才会被加载。此组件会加载对应的proto文件，并完成消息的基于protobuf的编解码。默认的proto文件的配置信息在config/serverProtos.json和config/clientProtos.json中。具体会在详细介绍pomelo-protobuf中详细介绍。

protobuf组件无配置项。

### channel组件

channel组件维护channel信息，可以被除了master之外的服务器加载。channel组件可以看作是channelService的组件包装,加载该组件后，会在app上下文中加入`channelService`，可以通过`app.get('channelService')`获取。可以认为一个channel就是一个用户的集合，每一个用户大致对应于前端服务器中的一个session，用户可以通过channel组件向一个channel里面的所有用户推送消息。当然，由于后端服务器并不与客户端直接相连，故后端服务器会发起一个sys rpc来表示向客户端推送消息，接受这个远程调用的是pomelo已经实现的ChannelRemote。

channel组件的配置项：
* broadcastFilter， broadcast的过滤函数。会在执行channel的broadcast的时候，在前端服务器上，在消息发送给每个session之前，进行一个过滤。其函数签名为 

    broadcastFilter(session, msg, filterParam)

其中filterParam参数由在channelService的broadcast调用时传入，如下:

    channelService.broadcast(type, route, {filterParam: param}, cb);

可以通过如下方式对Channel组件进行配置：

    app.set('channelConfig', opts)

### backendSession组件

BackendSession组件可以看作是BackendSessionService的组件包装，加载该组件后，会在app的上下文中加入`backendSessionService`，可以通过`app.get('backendSessionService')`调用获取。可以被除了master之外的服务器加载。它主要为后端服务器提供BackendSession信息，并通过远程过程调用完成一些比如对原始session绑定uid等操作。

backendSession组件无配置项。

使用pomelo开发应用时，我们一直关注的是给框架填入相应的回调，给app配置一些上下文。而没有太多关心整个框架的驱动力量。 在我们启动应用的时候，我们会在game-server目录下执行pomelo start，然后就能看到很多log信息，这样就启动了很多服务器。但是我们并没有太多关心框架是如何做到这一点的，在这部分，将试图向你讲述pomelo框架是如何驱动的。

首先看下图:

![ps_tree](images/ps_tree.png)

这张图是以chat为例，当chat应用启动后，使用命令
    
    pstree -au

得到的进程树的一部分，我们从图上可以清楚地看出，`pomelo start`调用进程会创建子进程，子进程执行的是`node app.js env=development`,然后这个子进程又会创建很多子进程，这些子进程执行的跟原进程同样的文件，只是多了更多的参数，它们后面会有一些诸如id，serverType，port等这样的参数。

好了，现在我们可以做一些简单的解释了，`pomelo start`的进程直接创建的那个子进程，实际上就是我们的master服务器进程，而由master服务器创建的那些子进程，他们执行的是类似于
    
    `node <BasePath>/app.js env=development id=chat-server-1 ...`
    
这样命令的则是由master服务器创建的子进程，这些子进程也就是我们的应用服务器。当然，这里的进程都在一台主机上，所以会有父子关系，也就是说master进程是其他应用服务器的父进程。如果各个进程分布在不同的物理主机上的话，pomelo默认会使用ssh的方式远程启动相应的服务器，那样的话，master进程与应用程序进程就不会再有父子关系了。
下面我们从pomelo.createApp调用开始，来梳理pomelo的启动过程。
首先我们使用`pomelo start`，此时命令行工具pomelo会检测start后面有没有其他参数，比如是否需要daemon的形式启动，后面的参数是否指定了env等，在这里，我们仅仅使用了`pomelo start`，后面没有跟任何其他参数，此时命令行工具将会为其添加一个默认的env参数，即 `env=develpment`，然后就启动了node.js进程，如下：

    `node <BasePath>/app.js env=development`

此时`pomelo start`就以没有过多参数的方式启动了app.js。

Application的初始化
=========================

接下来我们来分析app.js的执行:

![init_app](images/app_init.png)

如上面的时序图所示：
*  pomelo调用createApp()
*  pomelo的createApp调用中会调用app的init方法，完成对app的初始化
*  app会使用appUtil提供的defaultConfiguration来完成自己的初始化配置
*  appUtil的defaultConfiguration会调用app的一些初始化方法，这些方法包括setEnv，loadMaster，loadServers，parseArgs，configLogger。这里setEnv操作会将当前的env设定为development， loadMaster调用会加载master服务器的配置信息，loadServers会加载所有的应用服务器的配置信息。parseArgs是一个很关键的操作，由于我们在启动参数中仅仅指定了env，其他的参数并没有指定，此时pomelo认为目前启动的不是应用服务器，而是master服务器。这样，当前的进程将使用master的配置信息，并将其自己的serverId，serverType等参数，均设置为master服务器所有的。实际上，对于应用服务器来说，如我们在上面进程树图中看到的那样，如果启动的是应用服务器的话，其`node app.js`后面将会带有很多参数，包括id，serverType，port，clientPort等参数，这些参数在parseArgs这一步将会被处理，从而确定当前服务器的id，当前服务器的类型以及其他所必须的配置信息。
* 在执行完上面的操作之后，app进入到INITED状态，同时pomelo的createApp返回。

在pomelo的createApp()返回后，我们在app.js里，往往会对app进行一些配置，比如调用app.set设置一个上下文变量的值，app.route调用配置个路由等。

Master服务器启动
====================

当执行完上面的用户编辑的代码后，将会进入到的是 app.start()调用, 当app.start调用时，首先会加载默认的组件，对于master服务器来说，其加载的默认组件为master组件和monitor组件。下面主要分析master组件在启动中的作用，分析一下master组件的启动过程：

![init_app](images/sd_master.png)

如上面的时序图所示:

* 首先app.start()首先会加载默认组件，由于没有指定服务器类型，此时会默认为master类型，拿到master的配置信息，加载Master组件，由于Master组件是以工厂函数的方式导出的，故会创建Master组件，Master组件的创建过程会创建MasterConsole，MasterConsole会创建MasterAgent，MasterAgent会创建监听Socket,用来监听应用服务器的监控和管理请求的。

* 在加载完所有的组件包括Master组件后，会启动所有的组件，对于Master服务器来说，会启动Master组件和Monitor组件，也就是调用相应组件的start方法，这里先讨论Master组件。Master组件会注册默认的Module，这是通过Application的registerAdmin实现的，这里多说一句，如果用户自定义了Module，可以在app.start调用之前调用registerAdmin，将自定义的Module挂到app上。

* 在将所有默认的Module都挂到app上后，Master组件会启动MasterConsoleService。在启动MasterConsoleService时，MasterConsoleService会从app处拿到所有挂到其上面的Module，然后将Module注册到自己的Module仓库中，这一步实际上就是Module放到一个以ModuleId做键的Map中，以使得后来有请求时，可以直接进行查询回调。

* 然后，开启MasterAgent的监听，这个时候，Master组件就已经可以接受监控管理请求了。
* 在开启监听后，下一步就是enable所有的Module, 主要就是根据Module的参数type和interval，来确定Module的回调触发方式，是周期性的由Master来拉，还是周期性的由Monitor来推，还是不是周期性的触发，使用其他的事件触发方式。如果使用了周期性的触发的话，将会对周期性的事件进行调度，调度是由pomelo-schedule提供的。
* 下一步，将启动所有的Module，如果有Module定义了start方法的话，将在这步被回调，pomelo核心中的Module console就提供了start方法。到这一步为止，Master组件已经开启了请求监听，挂在好了每一个Module相应的回调函数，并且对需要周期执行的监控任务已经完成了调度。
* 是时候启动所有的应用服务器了。当Master组件完成了所有的其自身的Module的初始化和开启任务后，Master会委托Starter来完成整个服务器群的启动。需要注意：由于每一个服务器一旦启动，就会向Master报告其状态，所以Master组件必须在启动应用服务器之前就准备好对来自服务器的监控数据作出回应，因此，这也是为什么Master组件在完成很多其自身的操作后，才去启动应用服务器。
* 我们知道，在app初始化的时候，master服务器已经加载了所有服务器的配置信息，每一个服务器要启动的地址，服务器的类型，服务器应该监听的端口等信息。Starter在启动这些服务器的时候将会分析服务器是在本地启动还是远程启动，如果在本地启动的话，将会起一个子进程，如果在远程启动的话，会使用ssh的方式远程启动相应的进程。这个时候的启动命令行，将会附带更多的参数，对于chat例子中来说，其chat-server启动命令行大概如下面的样子:

    `node <BasePath>/app.js env=development id=chat-server-1 host=127.0.0.1 port=6050 serverType=chat`

* 此后，应用服务器将会被启动。
* 在调用了Master组件的start方法后，由于Master方法没有定义afterStart方法，故此时Master组件的启动过程已经完毕，Master组件将会监听来自其他服务器的Monitor发出的请求或者给其他的Monitor推送通知，当然这些操作都是在对应的Module定义的回调中进行的。

应用服务器启动
====================

* 对于应用服务器来说，与master服务器一样，会执行app.js,也会创建app，加载一些配置信息，setEnv等。应用服务器与Master服务器在App init阶段唯一的不同就是，Master服务器的启动命令行中，没有具体服务器参数，使得pomelo会把其当作Master服务器启动，而应用服务器的启动命令行，则包含了全部的应用服务器参数，因此pomelo会按照他们具体的配置信息为其默认加载不同的组件，对于master服务器来会加载Master组件，对于应用服务器来说，则会根据应用服务器的配置不同，默认加载相应的组件。

* 在创建完app，并完成初始化后，app.js中的对app进行配置的代码会执行，这里包括app.route调用，app.set调用等等。

* 在执行完用户的配置代码后，app.js进入到Application.start调用，在这里pomelo框架会针对每一种服务器将默认加载不同的组件。 对于pomelo来说，所有服务器的执行都可以看作是对其组件进行生命周期管理的过程。每一个pomelo的组件都会定义start，afterStart，stop方法，用来框架进行生命周期管理时候回调。下面展示了其调用顺序:

![app](https://github-camo.global.ssl.fastly.net/cc8061f334e3d953f731be4c9327b275abc84e4d/687474703a2f2f706f6d656c6f2e6e6574656173652e636f6d2f7265736f757263652f646f63756d656e74496d6167652f636f6d706f6e656e74732e706e67)

* pomelo框架总是先顺序地调用所有组件的start方法后，才去顺序的调用每个组件的afterStart方法。设置afterStart方法的原因是，可能有组件互相依赖的时候，某些组件的某些启动过程依赖于另外某个组件的启动过程时，可以将有依赖的部分放到afterStart方法里面，这样可以使得在有依赖的部分执行时，其所依赖的组件已经完成初始化。或者还有一些需要等待全局就绪的工作也可以放到这里来做。

* 不同的组件在启动时会开启不同的功能，关于应用服务器加载的组件的具体启动过程，由于涉及到其提供的功能细节，将在后面介绍，这里关注的不是组件的细节功能，而是整个应用程序的驱动方式。

* 当所有组件的afterStart方法都调用完毕后，应用服务器启动完成。此时，由于其加载的组件开启了监听接口，应用服务器将接受外来的请求，然后进入相应的回调。

服务器的关闭
===============

当我们调用了`pomelo start`启动了master服务器，master服务器又启动了所有的应用服务器后，所有的服务器都进入到自己的事件循环中，接受外来的请求事件或者是自身的定时器事件执行相应的回调方法。

当我们想关闭服务器时候，我们可以很暴力地使用`Ctrl+C`直接结束掉所有的进程，也可以优雅地通过命令行工具执行`pomelo stop`进行关闭。实际上，命令行工具是作为pomelo管理框架中的client角色的，它使用的Module是pomelo内建的console，通过console Module给master服务器发出关闭服务器请求，master会给每一个服务器发出停止通告。每个应用服务器接收到stop通告后，回调函数里面会调用app.stop, app.stop则会如上面图中那样，按照加载的逆序分别调用每一个组件的stop回调方法。当所有的组件的stop调用完后，服务器完成关闭。master在发出停止通告后，自己稍作等待也调用app.stop,stop掉自己加载的组件完成关闭。

总结
==========

我们在这里阐述了pomelo应用从启动到关闭的整个流程，pomelo应用的整个流程实际就是对其所加载的组件的生命周期的管理过程，pomelo的核心功能都由其组件提供。每一个组件在导出的时候，往往导出的都是一个工厂函数，通过工厂函数，app在加载的时候才会创建相应的组件。app在整个pomelo应用中，并不执行逻辑业务，它仅仅被当作一个全程驱动的入口以及一个上下文环境。对整个应用其关键性的调用为app的start调用和app.stop调用，其中app.start启动服务器，app.stop关闭服务器。app.start一般都是在app.js中由用户来调用，而app.stop一般都是系统的某个组件接受到停止服务器请求时进行的异步回调。关于具体加载的一些组件的功能，将在相关部分进行详述。


pomelo 有自己的风格以及一些约定，下面对其进行了简单的总结：

* pomelo是一个框架，因此我们在编写的代码都是用来配置框架，以及定义一些被框架进行回调的方法。

* 在pomelo中，无论是component，handler，filter，module，remote等等，它们在导出的时候，往往都会导出一个工厂函数，而不是直接导出对象，这样的话，就能够进行上下文的注入，或者在加载时传入一些配置参数。比起直接导出一个对象，更为灵活好用。在pomelo中也大量使用这种方式。

* pomelo中，很多情况下，框架会从特定的地方读取配置和代码，因此代码组织要遵循pomelo的规范。在game-server/app/servers目录下书写服务器的代码。每一个服务器代码分到两个目录，为handler和remote，分别描述了这个服务器作为接受客户端请求以及作为rpc服务端的逻辑。因此，在pomelo中目录结构很重要。

* pomelo中命名风格基本上与常见的java中命名风格相同。用于创建对象的函数采用全部首字母大写，普通或者对象的方法采用首单词小写字母开头，后面单词大写字母开头，不使用下划线，常量使用全大写，单词间使用下划线隔开。这种风格是非常常见的命名风格。

* 其他，关于编码风格以及编程模式方面,欢迎贡献

在前面的介绍中，我们知道pomelo支持动态地增加以及删除某一个服务器，于是我们会问当增加一个应用服务器的时候，已经启动的应用服务器是怎么知道新增加了一个服务器的；当停止某个服务器时，其他服务器又是怎样获知这些消息，并使得以后的rpc或者消息不路由到已经停止的服务器的。还有，如果查看整个服务器群的信息，或者整个服务器群的运行状态。诸如此类的问题，pomelo提供了一个管理框架，通过对这个框架进行扩展，用户将可以自己定制一些需要监控的信息，下面将对此进行介绍。

pomelo管理框架
===============

* pomelo的管理框架中，将对应的主体分为三种角色，分别为master，monitor，client。其中master可以认为对应于master服务器的Master组件，monitor可以认为是所有服务器都加载的Monitor组件。而client，可以认为是第三方的管理工具，pomelo提供的命令行工具，pomelo-cli以及admin-console-web都扮演了client角色。

* 一般情况下，监控管理模型大致可以分为两类：
    - master向monitor发出请求某些监控信息，monitor向master上报其信息，master获得到信息后进行缓存。第三方的client会连接到master上，请求整个服务器群的监控信息，master将缓存的监控信息返回给client。
    - client连接到master上后，给master发送一条命令，比如请求关服务器命令，master获得这个命令后，也就是关闭服务器命令后，master会向monitor广播此关闭命令，每一个monitor收到关闭命令后，关闭自身。

* 下面展示了监控框架相关的类图,这个是从前面的整个框架的类图中取出来的，与管理框架相关的类:

![pomelo框架类图](images/admin.png)

在上面类图中，Master组件，Monitor组件，AdminClient分别扮演我们上面提到的master，monitor和client角色，下面的叙述中将对这些术语不加区分的混用。

* 对于Master端，MasterConsoleService会管理所有已注册的Module，生成以ModuleId为主键的Module的map。MasterAgent监听端口，承受来自monitor和client的连接与注册，接受monitor和client的request/notify，向monitor发送request/notify，需要注意的是，master不会向client发出request/notify,只会针对client的request进行response。

* 对于Monitor端，MonitorConsoleService会管理所有已注册的Module，维护Module的map。所有的服务器通过配置文件都能获知到master服务器的监听地址和端口，MonitorAgent会主动发起连接到master,并维护对应的连接，然后通过此连接与master端通信。

* 对于client端，要求使用一个用户名和口令主动发起到master的连接及注册，验证通过后，AdminClient会维护到master的连接，然后就可以向master发送request/notify了。

* 所有与通信相关的类，都为维护自己的socket信息，对于Master来说，不仅仅有连接的socket，还有监听的socket。在整个管理框架中，通信层使用的socket.io。

* 每一个Module会定义四个回调monitorHandler，masterHandler，clientHandler，start，对于不同用途的Module，可能会省略掉一些用不着的回调函数定义，也就是说这四个回调都是可选的。每一个回调函数的签名为`XXXHandler(agent, msg, cb)`,第一个参数指出调用的Agent，可以是MonitorAgent或者MasterAgent，第二个参数是request/notify中的请求体，第三个是回调函数，如果是请求的话，最后结果通过回调第三个参数返回结果，否则的话，忽略第三个参数。

下面我们用一个类时序图，来说明整个框架的控制流程:


![pomelo框架类图](images/sd_admin.png)

实际上，控制流程是多个，这里为了省事，将所有流程都画到一个图中了，对于后面的一些行为实际上是可以没有先后顺序的，希望读者能够甄辨。

#### master组件的启动
master服务器总是率先启动，Master组件在其start调用的最后才会调用Starter.start,Starter.start才会启动所有的应用服务器，因此Master组件总是最先start。在Master组件的start调用中，会完成以下几步:

- 加载注册Module到MasterConsoleService，Module的导出方式有两种，可以导出工厂函数，也可以导出对象，如果导出工厂函数的话，其签名应该是 FacFunc(opts, ConsoleServicee),其中opts是用户调用app.registerAdmin的时候传入的，ConsoleService则是具体的加载注册Module的MasterConsoleService。

- 在加载注册完所有的Module后，会开启MasterAgent对端口的监听，此时，master就已经可以接收来自monitor和client的request和notify了。

- 开启监听后，MasterConsoleService会enable所有的module，这步操作主要是看看有没有module配置了周期性地拉去monitor信息，也就是module的配置中有type选项和interval选项，且type的值为'pull'，interval指定了周期，则认为其配置了周期性监控操作，此时会完成周期性事件的调度，使得master可以周期性地获取监控信息。

- 最后如果有Module定义了start回调，将会在这里调用，一般在start回调里会做一些初始化信息。
经历了这些步骤后，master完成启动。

#### monitor组件的启动

由于应用服务器是在Master组件启动后期才创建，因此monitor总是后于master启动。monitor的启动过程与master类似，唯一不同的就是，monitor会发起到master的连接，而不是监听接口。monitor中同样也会使用与master完全相同的方式，加载注册Module，如果有Module配置了周期性地推送监控数据到master的话，即其配置type的值为'push',这里也会调度对应的事件，使得能够周期地推送数据。最后如果有Module定义了start的话，则会回调start。Monitor的启动过程与master基本一致。

#### client的连接注册
client会连接注册到master上，因此，client需要在master开始监听端口后，才能成功连接上，在连接到master上后，基于安全的缘故，master需要使用用户名和密码对其进行验证，具体的客户端验证的配置文件为config/adminUser.json，例子程序里有相应的配置示例。如果master提供的用户名和密码，通过了验证，那么客户端就在master上注册成功，就可以给master发request/notify了。

#### 周期触发

对于配置了type和interval的Module，它们被认为是需要周期性进行回调的，在前面的enable module阶段，已经对其进行了调度。如果配置的type为'pull',那么每隔interval秒，在master端，其对应的masterHandler将会被回调，回调的时候，不会传入参数。

#### 主动请求

* 当有monitor向master发出request/notify的时候，请求参数会指出相应的ModuleId以及回调调用的参数，在master端，对应的Module的masterHandler将会被回调，此时回调会使用monitor请求中携带的参数。因此，通过对masterHandler请求的参数进行判断就可以区分到底是周期性任务还是monitor请求。

* 对于monitor端，与master类似，当某个Module配置了type为'push'的时候，其对应的monitorHandler将会被回调，当master给monitor发送request/notify的时候，其对应的monitorHandler也同样会被回调。与master一样，可以通过调用是否有参数进行区分是周期性的任务还是接收到了master的消息。当然，即使是master的消息，也可能没有携带任何参数，这种情况只能由用户自己处理了，一般来说，为了便于区分，不要发送不带参数的request/notify。

* client在连接到master上后，client可以向master发送request/notify，请求信息中带有ModuleId和对应的回调参数。master接受后，对应Module的clientHandler将会被回调。这里要注意的是master不会主动向client发送request/notify,只会对client的消息进行响应。

以上的用例行为基本上描述了pomelo的管理框架的执行流，下面会对pomelo内建的两个module做一些分析。

watchdog分析
==================

我们知道对于服务器配置的静态信息可以从配置文件中直接读取，但是由于服务器可以在运行时增加和停止，而整个服务器群的其他服务器也需要获知具体的服务器的动态信息，就需要一种机制来实现这一切。

pomelo是通过内建的Module watchdog实现这一切的,下面继续通过选取典型的用例场景，使用非正式的时序图来说明其流程:

![pomelo框架类图](images/sd_watchdog.png)

#### 绑定连接/断开事件
在加载watchdog这个module时，在master端，除了会监听端口外，还做了一件很重要的工作，就是将底层socket的事件由MasterAgent捕捉后，重新抛出，由MasterConsoleService捕捉后进行处理，这些事件为：
   - register事件，即一旦有MonitorAgent发起到MasterAgent的连接时触发，MasterConsoleService会在这个事件的处理中，发起广播通知增加的服务器信息。
   - disconnect事件，即一旦有MonitorAgent断开连接时触发，MasterConsoleService会在这个事件处理中，发起广播通知有服务器离开的消息。
   - reconnect事件，是当有应用服务器重连时触发，MasterConsoleService会在这个事件处理中，发起广播通知有服务器重连的消息。

#### 新增服务器

用例行为4展示了在monitor端，加载watchdog这个module的时候，会在start阶段，执行watchdog的start，在这里，monitor会向master发起一个订阅请求，也就是说此时monitor请求订阅所有的服务器变化信息，当MasterAgent接收到请求时，masterHandler会回调，通过检查参数，获知是一个subscribe操作，masterHandler的回调中会返回所有目前已经启动的服务器的信息给这个新启动的服务器，并将其加入到监听者列表，以后每次再有服务器变动的时候，也会将具体的服务器变动消息发送给此服务器。


用例行为3展示了，当新增一个服务器的时候的交互行为，有monitor发起到master的注册请求，从而激发了master端的register事件处理，其行为为通过MasterAgent广播新增服务器的notify到所有已经订阅注册的服务器，这些服务器收到notify后，其monitorHandler被回调，在monitorHandler中会调用app.addServers方法，这样所有的服务器群都会获知新增的服务器。

#### 停止服务器

用例行为5展示了当有应用服务器断开的情况，当有服务器断开的时候，会激发MonitorAgent的disconnect事件，在这个事件处理中，MasterConsoleService会发起广播notify到所有的服务器，其他的服务器收到此notify后，monitorHandler会被回调，在回调中，通过判断参数，获知是有服务器停止工作，调用app.removeServer删除相应的服务器。同时，在master端，watchdog的监听者列表里也会将这个服务器的信息删除。

#### 服务器重连

用例行为6展示了当有应用服务器断开重连的情况，具体行为跟前面的服务器加入和离开类似，读者可以结合源码自行分析。



watchdog是pomelo内部很核心的一个module，用来完成服务器状态信息交换。因此在这个module中仅仅涉及到master，monitor角色，没有client角色,因此省略了与client有关的clientHandler回调函数的定义。其事件是由底层socket连接来激发的，而不是周期性地由定时器激发,所以在module的定义中并没有指定其type和interval配置。

console分析
==============

这里在简单分析一下console组件，console组件主要为pomelo命令行工具服务，


![pomelo框架类图](images/sd_console.png)

图中所示的用例为一般情况下，用户通过一个命令来管理整个服务器群的方式。我们以命令行工具的list命令为例子来说明：

* 用户执行`pomleo list [options]`,此时，命令行工具会创建一个AdminClient，然后向master发出注册请求，后面的参数用来指定master的位置，端口号以及向master注册所使用的用户名和口令，master用此来进行校验身份，给予不同的权限。其具体的参数以及参数默认值，在pomelo命令行工具里面会有详细的介绍。

* 当AdminClient向Master注册成功后，给其发送请求，参数部分指定了moduleId和具体要做的操作，在我们这个例子中，moduleId就是console，具体的操作为list命令。

* 在master端，收到请求后，其console module的clientHandler被回调，在回调中，通过判断其操作是list，于是向所有与其连接的monitor请求服务器信息。

* 在monitor端，收到master发出的请求后，其console module的monitorHandler被回调，在回调中会获得自己的服务器信息，包括pid，heapused等信息响应给master。

* master在收集完所有monitor的响应后，将获得到的服务器信息数据响应给AdminClient，也就是会由命令行工具收到，并显示出来。


大部分的客户端执行命令流程都是如上面所示，一般情况下，如果配置了周期性地由master去拉取或者由monitor主动推送消息的话，那么当客户端发出请求时，master就可以直接返回其缓存的东西，而不需要一旦客户端发起请求，就向所有的服务器轮询，我们在前面的教程里实现的timeReport module就是使用了周期拉取，当客户端请求时，直接返回缓存的方式。

在console这个module中，由于没有monitor给master发request/notify，所以console的masterHandler回调可以省略，同样console还省略了start回调，因为这里没有什么需要在正常的请求响应之前要执行的东西。

需要注意： 在命令行工具中，add命令现在已经过时了，也就说console module中关于处理add方法的部分现在已经过时，当需要add服务器的时候，推荐使用pomelo-cli，那是一个更强大的交互式命令行工具，pomelo-cli使用的module定义在pomelo-admin中，包括watchServer等。读者可以按照前面的分析方式，自行分析pomelo-cli以及pomelo-admin中定义的module。在pomelo应用中，通过`app.enable('systemMonitor')`，将会使得应用默认注册pomelo-admin中定义的module，否则，仅仅有console和watchdog会被默认注册。还有一个基于web的监控工具pomelo-admin-web,它提供了通过web页面来看服务器管理监控信息的方式，它也是一个监控管理的客户端。

权限管理
==============

在客户端连接到master上的时候，需要对客户端进行身份验证，验证使用用户名和口令，用户的权限分为三个等级，他们分别对应不同的权限。用户的配置信息在adminUser.json中，其中level 1的权限可以执行任何操作，其他level的权限的控制权限收到限制。关于权限控制以及用户信息的配置，可以参考[pomelo-cli的相关文档](pomelo-cli使用)。

小结
========

本部分详细介绍地介绍了pomelo的监控管理框架的工作流程，分析了pomelo核心的两个module Watchdog和console的工作原理。结合前面教程中关于module的例子，用户可以很容易地完成自己特殊需要的module的定制。


在这部分，我们继续讨论与用户请求相关的内容。后端服务器中是用来处理用户请求的具体逻辑的地方，当前端服务器接收到来自客户端的请求时，通过分析请求的路由，并做简单的校验表明路由是合法的，那么前端服务器就会根据路由策略配置，选择某一后端服务器，发起rpc调用。后端服务器的所有调用请求均来自前端服务器的rpc调用。


当后端服务器发起filter-handler链对前端服务器分派过来的请求进行处理时，如果仅仅需要给用户端响应，那么仅仅通过rpc的回调返回具体的响应即可。但是，很多情况下，具体的请求处理逻辑需要给其他用户推送消息。比如，在一个聊天应用中，当有一个用户发起聊天请求时，其聊天的所有内容都需要推送给同一房间的其他用户。当然，消息推送逻辑并不仅仅在后端服务器中使用，前端服务器也可能会有类似的场景。

CoBackendSession组件和CoChannel组件一般是用在后端服务器中的，它们一起来完成给特定的用户推送消息。我们知道，BackendSession可以看作前端原始session在后端服务器的一个代理，CoBackendSession包装的BackendSessionService就是用来创建并管理后端的BackendSession，并可以通过相应的bind以及push调用，可以给前端原始的session绑定uid，以及设置一些属性。

CoChannel包装的ChannelService中维护了Channel的信息，每一个Channel可以看作是一系列绑定用户的uid集合，通过Channel的相应调用即可向客户端推送消息。以下是对后端服务器来说，相应的类关系图:

![server2](images/server2.png)

* 后端服务器的所有请求都是从前端服务器的rpc请求中获得的，也就是说后端服务器的CoServer组件的请求是MsgRemote派发的。

* 当前端服务器发出rpc请求时，会携带用来创建BackendSession的信息。在后端服务器中，会创建对应的session信息，这个session就是backendSession，对backendSession所做的任何更改不会影响原始的前端服务器中的session。当遇到用户的登录请求时，可能需要给原始的session绑定uid，并且设定一些自定义属性。以聊天为例，后端服务器处理登录请求时，就需要给session绑定uid，并且给其设置属性room_id等。这些可以通过使用BackendSession的bind以及push操作。在后端服务器求处理链上的所有session参数，其类型均是BackendSession，对其的直接修改不会直接反映到原始的前端服务器的session上。

* 有时候，需要对用户进行分组，以便更好地推送消息。还以聊天为例，一个聊天室的成员应分为一组，当有人说话时，直接将消息推送到这一组即可。pomelo中的Channel就是应用这种场景的，每一个Channel中维护一个uid列表，当调用Channel的pushMessge方法时，会给所有的在这个Channel中的用户推送消息。

* ChannelService还提供了pushMessageByUids方法，使得推送消息的时候，不用通过Channel，直接传入一个用户列表即可，这样使得消息推送更加灵活。同时，ChannelService还提供了broadcast方法，可以针对某一类型的前端服务器，给其所维护的所有已经绑定uid的session广播消息。

* 以上的对BackendSession以及Channel操作，无论是给session绑定id，还是通过Channel发送消息,还是通过ChannelService进行广播，实际上都涉及到与客户端的通信，由于后端服务器是无法与客户端进行通信的，这些操作实际上都是对前端服务器的rpc调用。因为在前端服务器发起rpc调用给后端服务器派发请求的时候，已经携带了前端服务器id等信息，在BackendSession中会维护此session所在的前端服务器的id，因此，此时后端服务器向前端服务器发起rpc调用时，不再需要路由计算，直接使用相应的frontendId即可。

以下是一些典型用例行为的时序图：

![server2](images/sd_server2.png)

* 上面的图中展示了后端服务器中的调用流程，从MsgRemote获得请求，然后分派给CoServer，Server会发起Filter-Handler链对用户请求进行处理，在Filter-Handler链中的session参数，均为BackendSession。当调用了session的bind，push，kick等操作时，CoBackendSession会向对应的前端服务器发起rpc调用，这个rpc调用由SessionRemote提供服务，完成对应session的bind，push，unbind,kick等操作。

* 如果在Handler-Filter链中处理时需要给用户推送或者广播消息，就可以使用Channel了。可以通过Channel的pushMessage给一个Channel推送消息，也可以使用ChannelService的pushMessageByUids。这些操作实际上也是对前端服务器的rpc调用,为这些操作提供rpc服务的是ChannelRemote。

注意事项
============

* BackendSession是前端服务器中的session在后端服务器中的代理，当后端服务器需要给前端的原始session绑定uid或者设置自定义属性时，需要使用调用bind和push，解绑uid绑定使用unbind。如果仅仅调用了BackendSession的set/get，而没有调用push的话，那么对BackendSession的属性的修改，只在后端服务器的处理链中后面部分有效，而不对其他任何地方的Session产生影响。比如，内建的Filter timeout，在before filter中，开启一个定时器，并把定时器id作为一个属性set到BackendSession中，这个定时器id属性将会在处理请求链的后面部分可以被访问，因此，在after filter中，就通过取得定时器id进行了定时器的清理工作。这种对BackendSession修改仅仅在后端服务器里有效，不会对前端的原始session造成任何影响。

* 对于前端服务器维护的Session信息，可以认为，一个客户端连接就对应一个Session，Session可以看作与客户端连接一一对应。当用户登录的时候，会使用uid绑定对应的session，也可以理解为这个用户通过哪个session进行了登录。在sessionService里有选项singleSession，如果设置为true的话，那就表示一个uid只允许一个session登录，当有新的session建立登录的时候，以前的登录会被踢掉。否则，是允许一个uid绑定多个session的，也就是说一个uid允许维持多个连接。这在实际中是很有意义的，比如，用户的客户端可能有多个设备，那么这样的话，多个设备就可以同时在线。

* 关于Channel，Channel中维护着一组uid，每一个uid会对应多个session，每个session由sessionid以及serverid来指定其前端的连接信息，一个uid可以加入多个Channel中。Channel是后端服务器本地的，也就是说两个后端服务器A和B不会共享Channel信息，当出现跨服务器访问Channel的时候，会出现Channel找不到的错误。当确实需要进行共享Channel信息时，可以考虑使用pomelo提供的global-channel插件，那里使用了redis来维护Channel信息，而不再把Channel信息放在服务器本地，后端服务器通过redis即可查询Channel中的uid信息，然后就可以发起调用了。

总结
==========

对客户端请求的处理是pomelo较为复杂的部分，它由pomelo的多个组件共同完成，前端服务器上的CoConnector会加载connector并开启请求监听，当有客户端连接的时候，其对应的连接事件会触发，从而会新的连接创建并维护session，这些操作由CoSession完成。当用户请求具体的服务的时候，前端服务器的CoServer会完成相应的服务器路由，后端服务器的Remote接收到请求后完成请求派发，后端服务器的CoServer会启动Filter-Handler链对请求进行处理，当处理过程中需要给session设置自定义属性以及绑定uid时，可以通过CoBackendSession来完成，当需要给客户端推送消息的时候，可以使用CoChannel提供的功能。当用户的请求通过了Filter-Handler链处理后，对应的响应会通过rpc调用的回调，再次返回到前端服务器的rpc发起者CoServer，然后CoConnector会将后端的响应或者后端推送的消息调度给CoPushScheduler，由CoPushScheduler实现具体的消息发布调度。当可以发布消息的时候，CoPushScheduler会通过CoSession获得到客户端连接的socket，然后通过socket将消息发送出去,完成整个消息处理流程。如果是用户的notify，将不会发送响应。

在实际编程中，为了减少数据传输带宽的消耗，提高传输效率，pomelo提供了对消息的压缩，包括基于字典的对route的压缩和基于protobuf的对具体传输数据的压缩。

route压缩
==========

在实际编程中，网络带宽的有效数据负载率是一个值得考虑的问题。特别地，对于移动客户端来说，网络资源往往并不是很丰富，为了尽可能地节省网络资源，往往需要尽大可能地增加数据包的有效数据率。

#### route问题

在pomelo编程中，pomelo中的route是用来确定消息的分发路径，将其交给相应的服务器和服务处理的。route分为两类，由客户端发给服务端消息时使用的route和服务端向客户端广播时使用的route。

* 前一种route是由服务器自动生成的，其中的字段就代表了对应的方法在服务端的位置。如“area.playerHandler.attack”则表示在“area”类型的服务器上的“playerHandler”提供的“attack”方法，其格式为"<ServerType>.<HandlerName>.<MethodName>"。 路由信息过长，使得有效消息数据负载率大大降低。例如，在聊天应用中，如果用户的发言仅仅是一个字符，结果不得不携带一个route,"chat.chatHandler.send",这样使得有效数据负载率大大降低。

* 后一种route是服务端想客户端推送消息时使用，是客户端的路由信息，如“onMove”，“onAttack”等，其格式一般为"on<XXX>"这些字段是由用户自己定义的。虽然可以定义很短的路由，但是那样会造成可读性变差，不利于代码阅读。

一般来说，当应用固定后，具体路由就不会再变动，因此可以考虑通过一种简单替换的方式对路由信息进行压缩。 

#### 基于dict的压缩

pomelo中实现了基于字典的route压缩，目前route压缩功能仅仅支持hybridconnector，sioconnector目前无法使用route压缩。其实现原理如下：

* 对于系统生成的route，也就是服务端的路由信息，即格式为"<ServerType>.<HandlerName>.<MethodName>"的路由信息，在系统启动时由CoDictionary组件进行服务端路由信息扫描，然后会对每一个route生成唯一的字典项，由一个无符号小整数标识。

* 对于用户自定义的route，也就是客户端的路由信息，即格式为"on<XXX>"，则需要用户提供一个自定义的route列表，会根据这一个列表对每个用户自定义的route生成一个对应的字典项，即也就是一个无符号小整数。

* 在开启字典功能的状态下，使用hybridconnector的时候，当协议握手的时候，服务端会将整个字典的消息发送给客户端，这样客户端和服务端都会拥有相同的具体route无符号整数的对应关系。

* 当有消息传递时，其中的route在发送时会被替换为在字典项,而接收端会自动还原，这一过程对于用户而言是完全透明的。

#### 使用route压缩

目前仅仅在hybridconnector中实现了支持，启用此功能只需在app.js中配置开启即可，示例如下：
```javascript
	app.set('connectorConfig',
		{
			connector : pomelo.connectors.hybridconnector,
			heartbeat : 3,
			useDict : true // enable route compression
			}
		});
```

客户端的路由信息，也就是用户自定义的路由信息，需要用户自己通过配置文件配置，具体的配置文件为config/dictionary.json，在这个文件中加入一个字符串列表即可，示例如下:

```javascript
[
	"onDropItem",
	"onAttack",
	"onDied",
	"onMove",
	"onRevive",
	"addEntities",
	"onRemoveEntities",
	"onPathCheckout"
]
```
``注意``：对于没有加入到这个列表中的客户端路由信息，依然会使用原始的路由，而不会使用整数，pomelo在打包消息的时候会进行判断，如果字典项里有相应的路由信息，那么会使用字典项，如果没有的话，会使用原始的路由信息。这一切对用户是透明的，用户只需要配置好就行，不用关心其具体实现。

基于protobuf的传输数据压缩
===========================

在进行消息传输时，pomelo实现了基于protobuf的数据编码协议，与其他的编码协议如xml，json相比，protobuf有着更好的传输效率和压缩比率。在我们的lordofpomelo项目中，使用protobuf进行数据编码后的消息大小只有基于Json的编码的20%左右。

#### protobuf协议介绍

protobuf协议是由google制定的，主要用于其内部的rpc调用和文件编码。原生的protobuf包括两部分内容：基于二进制的数据编码协议和基于proto元数据的代码生成器。首先，需要根据每条消息来编写对应的proto文件，然后使用google提供的代码生成器，基于proto文件来生成相应的编码器和解码器，然后使用生成的编/解码器来进行编/解码操作，对应的流程如下图：

![protobuf](images/proto-orig.png)

这种方式的优势是代码静态生成，运行时不需要proto文件信息，而且可以根据具体的信息内容对代码进行优化，编解码的时候不需要类型元信息，效率很高。但缺点也十分明显：使用复杂（涉及到代码生成，编译，部署），改动成本高昂（需要重新生成，编译代码，并对代码进行部署），需要生成大量新代码（每个消息都需要一个独立的编码/解码器）。
关于protobuf协议的更多内容，可以参见其官网[protobuf项目](https://code.google.com/p/protobuf/)。

#### pomelo中的protobuf

原生的带有代码生成器的protobuf过于重量级，缺乏灵活性，任何消息的修改都会是一个非常重量级的操作，而这个在pomelo中，由于pomelo是能够快速开发的，因此也必须要求代码不能有编译阶段，所有的类型信息应该在运行时进行评估。因此，我们没有采用生成代码的方式，而是根据proto文件的定义，对消息进行即时的解析。

在pomelo中，我们实现了一个通用的protobuf编/解码器，以及一个proto文件解析器。通过分析proto文件内容，实现了对消息的编码/解码。这样，当修改/添加消息类型时，只需要修改对应的proto文件就可以了。具体的运行流程如下图：

![pomelo protobuf](images/proto-pomelo.png)

从上图可以看出，与原生的protobuf生成代码的方式相比，pomelo中的解决方案要更将灵活，轻量。不需要生成任何代码，在运行时通过proto文件中对消息的定义，实现对消息的动态编码/解码功能。

#### proto 文件定义

原生的protobuf中，每一个消息都与一个proto中的message定义对应，而在生成编码/解码器之后，这些message的定义不再被使用。而在pomelo中，因为我们需要proto的内容来动态的对消息进行编码/解码，因此需要维护一个完整的protos信息表, 我们将所有的proto定义放在一个json文件中，通过key来进行区分，在pomelo中，key就是消息的route。我们的proto文件使用了类似与原始proto的语法，不过是使用了json格式，示例如下：

```json
"onMove" : {
  "required uInt32 entityId" : 1,
  "message Path": {
    "required uInt32 x" : 1,
    "required uInt32 y" : 2
  },
  "repeated Path path" : 2,
  "required uInt32 speed" : 3
},
"onAttack" : {
  "required uInt32 attacker" : 1,
  "required uInt32 target" : 2
}
```
在pomelo中，对于同样route的消息，如'area.playerHander.attack'，在客户端和服务端的格式可能完全不同，这就意味着对于客户端的编码器和解码器对于同样route的消息需要不同的定义。因此，我们需要两套protos文件，server protos和client protos，具体的关系如下图：
![pomelo protobuf protos](images/ser_cli_proto.png)

#### 使用protobuf
  
虽然protobuf的实现看上去十分复杂，但由于这一层对用户是完全透明的，使用会非常简单。用户只需要通过简单的两步定义就可以在原有的项目中开启protobuf功能。

* 首先，需要在connector组件上打开protobuf开关，在app.js中的配置如下：
```javascript
	app.set('connectorConfig',
		{
			connector : pomelo.connectors.hybridconnector,
			heartbeat : 3,
			useProtobuf : true
		});
```
* 实际上需要加入的就是“useProtobuf：true”这一项。当设置这一标识后，pomelo会在客户端握手时将protos内容同步到客户端，并默认开启protobuf压缩功能。

* 在protobuf功能开启用，用户还需要加入protos定义来实现对具体消息的编码/解码。protos文件默认在/game-server/config目录下，包括两个文件：serverProtos.json和clientProtos.json，分别表示服务端->客户端消息的protos和 客户端->服务端消息的protos。只要在其中加入有效的proto定义，就可以开启对应消息的protobuf编码功能，CoProtobuf组件会自动加载这两个proto文件。

* 当然pomelo中的protobuf实现对原有项目是完全兼容的，你可以直接在老的项目中打开protobuf开关而不会引起任何问题。只是当proto定义是空的，默认所有的消息都不会经过protobuf压缩，而是采用默认的二进制编码进行传输。

* 当你想对某个消息进行protobuf编码时，只需要在对应的protos文件（serverProtos.json或clientProtos.json）中加入对应的protobuf项，pomelo在启动时就会自动识别并对消息进行压缩，而不会对其他未定义的消息产生任何影响。

总结
==========

在这部分，介绍了pomelo中实现的对数据的压缩。通过对数据的压缩提高了带宽的有效数据利用率，使得在一些带宽以及流量敏感的环境中，pomelo能够更好地工作。目前pomelo的route以及基于protobuf的数据压缩仅仅支持hybridconnector，对于sioconnector，是使用json作为通信格式的，目前不支持对其进行压缩。
pomelo 提供了一系列的工具和库供开发者使用，这些工具和库能够协助开发者更好地完成应用开发、调试以及部署等工作。这些工具和库涵盖全面，有管理控制工具，有用来做压力测试的工具，也有一些比较通用的库。

* **命令行工具pomelo**

pomelo框架提供的一个较简单的工具，该工具可以帮助开发者更便捷、更有效地进行应用开发，包括创建项目、启动应用、停止应用、关闭应用等等，请参考[pomelo命令行工具使用](pomelo命令行工具使用)。

* **pomelo-cli**

pomelo-cli是一个pomelo服务器群的管理客户端，通过连接注册到master服务器，可以对服务器群进行较为高级的管理，如运行时动态的添加关闭服务器，查看服务器的状态等等。请参考[pomelo-cli更详细的文档](pomelo-cli使用)。

* **pomelo-robot**

pomelo-robot是一个用来对pomelo游戏框架进行性能测试的工具，可以帮助开发者做一些压力测试，请参考[pomelo-robot更详细的文档](https://github.com/NetEase/pomelo/wiki/pomelo-robot%E4%BD%BF%E7%94%A8%E6%96%87%E6%A1%A3)

* **pomelo-daemon**

pomelo-daemon 提供了一个 daemon 服务，可以用这个服务来进行分布式部署以及日志收集。请参考[pomelo-daemon的使用](pomelo-daemon的使用)。

* **pomelo-admin-web**

pomelo-admin-web 是 pomelo 框架中基于[pomelo-admin](https://github.com/NetEase/pomelo-admin)开发的web端监控的模块，可以通过 web 端的方式来对游戏服务器集群的运行状态，性能，日志等进行实时的监控。请参考[pomelo-admin-web工具的使用](pomelo-admin-web工具的使用)。

* **pomelo-sync**

pomelo-sync 模块是用来管理游戏进程中需要持久化的数据在内存与存储系统之间同步的。请参考[pomelo sync 使用文档](https://github.com/NetEase/pomelo/wiki/pomelo-sync%E4%BD%BF%E7%94%A8%E6%96%87%E6%A1%A3)

* **pomelo-protobuf**

pomelo-protobuf 是对google protobuf的一个实现，借助javascript的语言特性，实现了类.proto文件的运行时解析，并用在pomelo框架中，完成对要传输消息的压缩。protobuf不仅可以用在服务端，也同样可以用于web客户端。具体请参考[pomelo-protobuf](https://github.com/pomelonode/pomelo-protobuf)。


一个真正高可扩展的游戏运行架构必须是多进程的。google的[gritsgame](http://code.google.com/p/gritsgame/),  mozilla的[browserquest](https://github.com/mozilla/BrowserQuest) 都采用了node.js作为游戏服务器开发语言， 但它们都采用了单进程的node.js服务器，缺乏扩展性，这使它们可以支撑的在线用户数量是很有限的（这两个游戏主要是作为HTML5游戏的demo）。而多进程的架构可以很好的实现游戏服务器的的扩展性，达到支撑较多在线用户、降低服务器压力等要求。

游戏服务器的运行架构
=======================

一个典型的多进程MMO运行架构， 如下图所示：

<center>
 ![MMO运行架构](images/mmo-arch.png)
</center>

一些说明：

* 上图中的方块表示进程， 定义上等同于“服务器”;
* 客户端通过websocket长连接连到connector服务器群;
* connector负责承载连接，并把请求转发到后端的服务器群;
* 后端的服务器群主要包括按场景分区的场景服务器(area)、聊天服务器(chat)和状态服务器(status)等， 这些服务器负责各自的业务逻辑。真实的案例中还会有各种其它类型的服务器;
* 后端服务器处理完逻辑后把结果返回给connector， 再由connector服务器broadcast/response回给客户端;
* master负责统一管理这些服务器，包括各服务器的启动、监控和关闭等功能。

pomelo的框架介绍
====================

#### pomelo架构组成

pomelo框架的组成如图所示：

<center>
 ![pomelo框架](images/pomelo-arch.png)
</center>

下面对架构图的一些说明:

* server management

pomelo是个真正多进程、分布式的游戏服务器。因此各游戏server(进程)的管理是pomelo很重要的部分，框架通过抽象使服务器的管理非常容易。server management 部分维护服务器的监控信息，对服务器进行管理等功能;

* network 

pomelo中的通信，包括服务器与客户端的通信，也包括服务器群中各个服务器进程之间的通信，也就是服务器间的rpc调用。请求、响应、广播、rpc、session管理等构成了整个游戏框架的脉络，所有游戏流程都构建在这个脉络上。

* application

应用的定义、component管理、上下文配置，这些使pomelo framework的对外接口很简单， 并且具有松耦合、可插拔架构。

pomelo的架构设计目标
======================

* 服务器（进程）的抽象与扩展

在web应用中， 每个服务器是无状态、对等的， 开发者无需通过框架或容器来管理服务器。
但游戏应用不同， 游戏可能需要包含多种不同类型的服务器，每类服务器在数量上也可能有不同的需求。这就需要框架对服务器进行抽象和解耦，支持服务器类型和数量上的扩展。

* 客户端的请求、响应、广播

客户端的请求、响应与web应用是类似的， 但框架是基于长连接的， 实现模式与http请求有一定差别。
广播是游戏服务器最频繁的操作， 需要方便的api， 并且在性能上达到极致。

* 服务器间的通讯、调用

尽管框架尽量避免跨进程调用，但进程间的通讯是不可避免的， 因此需要一个方便好用的rpc框架来支撑。

* 松耦合、可插拔的应用架构。

应用的扩展性很重要，pomelo framework支持以component的形式插入任何第三方组件, 也支持加入自定义的路由规则， 自定义的filter，自定义admin module等。

下面分别对这些目标进行分析：

### 服务器（进程）的抽象与扩展介绍

#### 服务器的抽象与分类

该架构把游戏服务器做了抽象， 抽象成为两类：前端服务器和后端服务器， 如图：

<center>
![服务器抽象](images/serverAbst.png)
</center>
 
前端服务器(frontend)的职责：
 * 负责承载客户端请求的连接
 * 维护session信息
 * 把请求转发到后端
 * 把后端需要广播的消息或响应发送到客户端

后端服务器(backend)的职责：
 * 处理业务逻辑， 包括RPC和前端请求的逻辑
 * 把消息推送回前端或者将对客户端请求的响应发送到前端服务器

#### 服务器的鸭子类型

动态语言的面向对象有个基本概念叫鸭子类型。
服务器的抽象也同样可以比喻为鸭子， 服务器的对外接口只有两类， 一类是接收客户端的请求， 叫做handler， 一类是接收RPC请求， 叫做remote， handler和remote的行为决定了服务器长什么样子。
因此我们只要定义好handler和remote两类的行为， 就可以确定这个服务器的类型。

#### 服务器抽象的实现

利用目录结构与服务器对应的形式， 可以快速实现服务器的抽象。

以下是示例图：

<center>
![目录结构](images/serverAbsDir.png)
</center>

图中的connector, area, chat三个目录代表三类服务器类型， 每个目录下的handler与remote决定了这个服务器的行为（对外接口）。 开发者只要往handler与remote目录填代码， 就可以实现某一类的服务器。这让服务器实现起来非常方便。
让服务器动起来， 只要填一份配置文件servers.json就可以让服务器快速动起来。
配置文件内容示例如下：
 
```json
{
  "development":{
    "connector": [
      {"id": "connector-server-1", "host": "127.0.0.1", "port": 3150, "clientPort":3010, "frontend":true},
      {"id": "connector-server-2", "host": "127.0.0.1", "port": 3151, "clientPort":3011, "frontend":true}
    ],
    "area": [
      {"id": "area-server-1", "host": "127.0.0.1", "port": 3250, "area": 1},
      {"id": "area-server-2", "host": "127.0.0.1", "port": 3251, "area": 2},
      {"id": "area-server-3", "host": "127.0.0.1", "port": 3252, "area": 3}
    ],
    "chat":[
      {"id":"chat-server-1","host":"127.0.0.1","port":3450}
    ]
   }
}
```

###  客户端请求与响应、广播的抽象介绍

所有的web应用框架都实现了请求与响应的抽象。尽管游戏应用是基于长连接的， 但请求与响应的抽象跟web应用很类似。
下图的代码是一个request请求示例：
 
<center>
![请求示例](images/req-resp.png)
</center>

请求的api与web应用的ajax请求很象，基于convention over configuration的原则， 请求不需要任何配置。 如下图所示，请求的route字符串：chat.chatHandler.send， 它可以将请求分发到chat服务器上chatHandler文件定义的send方法。
 
pomelo的框架里还实现了对request的filter机制，广播/组播机制，以及Channel的支持等，更详细的内容可以参考后面的开发指南部分的相关内容。

###  服务器间rpc调用的抽象介绍

架构中各服务器之间的通讯主要是通过底层rpc框架来完成的，该rpc框架主要解决了进程间消息的路由和rpc底层通讯协议的选择两个问题。
服务器间的rpc调用也实现了零配置。实例如下图所示：
 
<center>
![rpc调用](images/rpc.png)
</center>

上图的remote目录里定义了一个rpc接口： chatRemote.js，它的接口定义如下：
```javascript
chatRemote.kick = function(uid, player, cb) {
}
```
其它服务器（RPC客户端）只要通过以下接口就可以实现rpc调用：
```javascript
app.rpc.chat.chatRemote.kick(session, uid, player, function(data){
});
```
这个调用会根据特定的路由规则转发到特定的服务器。（如场景服务的请求会根据玩家在哪个场景直接转发到对应的server）。rpc框架目前在底层采用socket.io作为通讯协议，但协议对上层是透明的，以后可以替换成任意的协议。

### 可插拔的component扩展架构

component是pomelo的核心，pomelo的核心功能都是由component完成，开发者可定制自己的component，并加载到框架中，以完成其功能。component在开发指南部分将有更深入的讨论。
以下是component的生命周期图：
<center>
![components](images/components.png)
</center>

用户只要实现component相关的接口： start, afterStart, stop, 就可以加载自定义的组件：

```javascript
app.load([name], comp, [opts])
```

总结
==========

在本部分，讲述了pomelo框架的整体架构，以及其设计目标。pomelo框架完成了对服务器的抽象，对用户请求响应以及服务器端主动推送消息的抽象，服务器间rpc调用的抽象，可插拔的components抽象。这些抽象使得pomelo非常灵活以及易于使用，易于扩展。

老传统，让我们也先从HelloWorld这个例子开始吧。

新建项目
=========

使用pomelo的命令行工具可以快速创建一个项目，命令如下：

    $ pomelo init ./HelloWorld

或者你也可以使用下面的三个命令：

    $ mkdir HelloWorld
    $ cd HelloWorld
    $ pomelo init

这两种创建方式是等价的，更多关于pomelo命令行使用的文档，请参阅[pomelo命令行工具使用](pomelo命令行工具使用)。在初始化项目的时候，用户需要选择其底层使用的通信协议，分为socket.io和websocket。

然后，进入到HelloWorld文件夹，安装依赖包：

    $ sh npm-install.sh

windows用户，可以直接运行 `npm-install.bat`

项目目录结构
================

让我们来看看一个pomelo项目的大致结构

新建立的项目结构如下图所示：

![项目目录结构](images/HelloWorldFolder.png)

该目录结构很清楚地展示了游戏项目的前后端分层结构，分别在各个目录下填写相关代码，即可快速开发游戏。下面对各个目录进行简要分析：

#### game-server
game-server是用pomelo框架搭建的游戏服务器，以文件app.js作为入口，运行游戏的所有逻辑和功能。在接下来的开发中，所有游戏逻辑、功能、配置等都在该目录下进行。

* app子目录

这个目录下放置所有的游戏服务器代码的地方，用户在这里实现不同类型的服务器，添加对应的Handler，Remote等等。


* config子目录

game-server下config包括了游戏服务器的所有配置信息。配置信息以JSON文件的格式进行定义，包含有日志、master、server等服务器的配置信息。该目录还可以进行扩展，对数据库配置信息、地图信息和数值表等信息进行定义。总而言之，这里是放着所有游戏服务器相关的配置信息的地方。

* logs子目录

日志是项目中不可或缺的，可以对项目的运行情况进行很好的备份，也是系统运维的参考数据之一，logs存放了游戏服务器所有的日志信息。

#### shared

shared存放一些前后端、game-server与web-server共用代码，由于都是javascript代码，那么对于一些工具或者算法代码，就可以前后端共用，极大地提高了代码重用性。

#### web-server

web-server是用[express](http://expressjs.com)框架搭建的web服务器，以文件app.js作为入口，当然开发者可以选择Nginx等其他web服务器。如果游戏的客户端不是web的话，如Android平台的话，这个目录就不是必须的了。当然，在这个例子中，我们的客户端是web，所以web服务器还是必须的。

启动项目
==============

对于我们这个例子来说，由于客户端是web，所以必须启动game-server(游戏服务器)和web-server(web服务器)

启动game-server服务器：

    $ cd game-server
    $ pomelo start

启动web-server服务器：

    $ cd web-server
    $ node app 


在启动过程中可能会有端口号冲突导致启动不成功，只需在config里面修改使用的端口号即可。如果上面的启动都没有问题的话，我们就可以对我们的HelloWorld进行测试了。用浏览器(推荐使用chrome)访问 `http://localhost:3001`或者 `http://127.0.0.1:3001` 即可, 点击Test Game Server，提示 *game server is ok* 说明运行成功，如下图所示：

![test](images/helloworld_test_snapshot.png)

查看服务器
================

可以使用`pomelo list`查看已经启动的服务器，如下图所示：

![test](images/list_snapshot.png) 

服务器状态可以查看5种状态信息：

* serverId：服务器的serverId，同config配置表中的id。
* serverType：服务器的serverType，同config配置表中的type。
* pid：服务器对应的进程pid。
* headUsed：该服务器已经使用的堆大小（单位：兆）。
* uptime：该服务器启动时长（单位：分钟）。

关闭项目
==============

可以使用以下两种方式关闭项目：

    $ cd game-server
    $ pomelo stop

或者

    $ cd game-server
    $ pomelo kill

其中`pomelo stop`比较优雅，`pomelo kill`比较粗暴，安全性低，开发环境下可以使用，产品环境慎用，更详细的pomelo命令行用法请参阅[pomelo命令行工具使用](pomelo命令行工具使用)。

小结
==========

到这里为止，我们已经成功安装了pomelo，并成功运行了HelloWorld。接下来，建议你看一下pomelo整体的一个较详细的概述。
如果你已经迫不及待地想写代码，可以去pomelo例子教程, 那里以一个chat应用为例，一步一步地向你展示如何来使用pomelo进行一个实际应用的开发，以及pomelo的一些API的使用方式等。

pomelo最初的设计初衷是为了游戏服务器， 不过在设计、开发完成后发现pomelo是个通用的分布式实时应用开发框架。下面将结合实际，从游戏服务器的需求，以及开发中面临的问题等方面阐述pomelo的设计动机。

游戏服务器概述
=====================

没开发过游戏的人会觉得游戏服务器是很神秘的东西。但事实上它并不比web服务器复杂，无非是给客户端提供网络请求服务，本质上它只是基于长连接的socket服务器。当然在逻辑复杂性、消息量、实时性方面有更高的要求，下面从web服务器与游戏服务器的对比中来说明游戏服务器的一些特点：

### 复杂的socket服务器

如果说web服务器的本质是http服务器，那么游戏服务器的本质就是socket服务器。 它利用socket通讯来实现服务器与客户端之间的交互。事实上有不少游戏是直接基于原生socket来开发的。 相对于简单的socket服务器，它承受着更加繁重的任务：

* 后端承载着极复杂的游戏逻辑。
* 网络流量与消息量巨大，且实时性要求高。
* 通常一台socket服务器无法支撑复杂的游戏逻辑，因此往往使用一个服务器集群来提供服务。

### 长连接和实时响应

web应用都是基于request/response的短连接模式,占用的资源要比一直hold长连接的游戏服务器要少很多，因此web应用可以使用基于http的短连接来达到最大的可扩展性，Web应用能使用短连接模式的原因如下：

* 通讯的单向性，普通web应用一般只有拉模式
* 响应的实时性要求不高，一般web应用的响应时间在3秒以内都算响应比较及时的。

而游戏应用只能使用长连接，原因如下：

* 通讯的双向性，游戏应用不仅仅是推拉模式，而且推送的数据量要远远大于拉的数据量
* 响应的实时性要求极高，一般游戏应用要求推送的消息实时反应，而实时响应的最大时间是100ms。

### 分区策略与负载均衡

普通的web应用在交互上没有相邻性的概念，所有用户之间的交互都是平等，交互频率也不受地域限制。 而游戏则不然，游戏交互跟玩家所在地图（场景）上的位置关系非常大，如两个玩家在相邻的地方可以互相PK或组队打怪。这种相邻的交互频率非常高，对实时性的要求也非常高，这就必须要求相邻玩家在分布在同一个进程里。于是就有了按场景分区的策略，如图所示：

![area](images/processArea.png)

一个进程里可以有一个场景，也可以有多个场景。这种实现带来了游戏的可伸缩性受到场景进程的限制，如果某个场景过于烦忙可能会把进程撑爆，也就把整个游戏撑爆。场景服务器是有状态的，每个用户请求必须发回原来的场景服务器。服务器的有状态带来一系列的问题：场景进程的可伸缩，高可用性等都比不上web服务器。目前只能通过游戏服务器的隔离来缓解这些问题。

web应用的分区可以根据负载均衡自由决定， 而游戏则是基于场景(area)的分区模式， 这使同场景的玩家跑在一个进程内， 以达到最少的跨进程调用。

### 可伸缩性与分布式开发

不管是web应用还是游戏服务器，可伸缩性始终是最重要的指标，也是最棘手的问题，它涉及到系统运行架构的搭建，各种优化策略。 只有把可伸缩性设计好了，游戏的规模、同时在线人数、响应时间等参数才能得到保证。最初的网络服务器是单进程的架构，所有的逻辑都在单台服务器内完成， 这对于同时在线要求不高的游戏是可以这么做的。由于同时在线人数的上升， 单服务器的可伸缩性必然受到挑战。随着网络游戏对可伸缩性要求的增加，分布式是必然的趋势的。
下面是一个web服务器和游戏服务器架构对比的示意图： 

![game_server_arch](images/webGameComp.png)

可以看到由于web服务器的无状态性，只需要通过前端的负载均衡器可以导向任意一个进程，因此运行架构相对简单， 而且很少需要分布式开发。

而游戏服务器是蜘蛛网式的架构，每个进程都有各自的职责，这些进程的交织在一起共同完成一件任务。因此游戏服务器是一个标准的分布式开发架构。

开发难点
===========

从上面的分析可知，游戏服务器是蜘蛛网式的架构，每个进程都有各自的职责，这些进程的交织在一起共同完成一件任务。这些需求也决定了游戏服务器开发的难度。这些难题有：

### 实时性保证
对实时游戏服务器来说，常见的实时性很高的任务有：

##### 实时Tick
实时游戏的服务端一般都需要一个定时tick来执行定时任务，为了游戏的实时性，一般要求这个tick时间在100ms之内。这些任务一般包括以下逻辑:

* 遍历场景中的实体(包括玩家、怪物等)，进行定时操作，如移动、复活、消失等逻辑。
* 定期补充场景中被杀掉的怪的数量。
* 定期执行AI操作，如怪物的攻击、逃跑等逻辑。

由于实时100ms的限制，这个实时tick的执行时间必须要远少于100ms。

##### 广播
由于玩家在游戏里的行动要实时地通知场景中的其它玩家， 必须通过广播的模式实时发送。这也使游戏在网络通信上的要求高于web应用。
游戏中广播的代价是非常大的。玩家的输入与输出是不对等的，玩家自己简单地动一下，就需要将这个消息实时推送给所有看到这个玩家的其他玩家。 假如场景里面人较少，广播发送的消息数还不多，但如果人数达到很密集的程度，则广播的频度将呈平方级增长。如图所示：

![broadcast](images/broadcast.png)

假如场景中1000个玩家，每人发1条消息，如果需要其它玩家都看到的话，消息的推送量将高达1,000,000条，这足以把任何服务器撑爆。

### 分布式开发

几乎在很多书、演讲和文章中都可以看到这样的观点： 分布式开发是很难的，分布式开发的难点主要有：

##### 多进程（服务器）的管理

通常的游戏服务器要由很多进程共同去完成任务。当这些进程交织在一起的时候，多进程的管理并不那么容易。

如果没有统一的抽象与管理，光把这些开发环境的进程启动起来就是非常复杂的工作， 进程的启动与重启就将严重影响开发效率。
重量级的进程消耗大量的机器资源，普通的开发机支撑不了那么多进程，可能一个人的开发环境就需要多台机器。
多进程间的调试并不容易， 我们发现一个bug就要跨好几个进程。

##### rpc调用

rpc调用的解决方案已经有n多年的历史了，但rpc在分布式开发效率上仍然没有明显提升。
以当前最流行的开发框架thrift为例，它在调用代码前需要经过以下步骤：
* 写一个.thrift文件
* 从.thrift文件生成源码

```
thrift --gen <language> <thrift_filename>
```

* 在程序中使用生成的源码
如果发生接口改动，我们又需要重新修改描述文件，重新生成stub接口。对于接口不稳定的开发环境， 这种方式对开发效率影响较大。要想让rpc调用的开发达到最简，不需生成stub接口， 无需描述文件， 我们需要一种很巧妙的方法。

##### 分布式事务、异步化操作

尽管我们尽量把逻辑放在一个进程里处理，但分布式事务仍然是不可避免的。两阶段提交的代码，异步化的操作在普通的开发语言里并不是容易的事。

##### 负载均衡，高可用

由于游戏服务器的有状态性，很多请求需要通过特定的路由规则导到某台服务器；对于有些无状态的服务器，我们则可以把请求路由到负载最低的服务器。通常对于无状态的服务器， 高可用是比较好做的。对于有状态的服务器，要做高可用会非常困难， 但也不是完全没有办法，常见的两招：
* 将状态引出到外存

例如redis， 这样进程本身就可以无状态了。但由于所有的操作都通过redis可能带来性能损耗，有些场景是不能承受这些损耗的。
* 通过进程互备

将状态通过日志等方式同步到另一进程， 但这可能存在着瞬间数据丢失的问题，这种数据丢失在一些应用场景可能毫无问题， 但在另外一些应用场景可能引起严重的数据不一致。

有状态的高可用并不是那么好实现的，pomelo在0.5版本提供高可用的实现机制，引入zookeeper和redis可以解决一些进程（如master）的高可用问题，但真正复杂的应用场景的逻辑只能由应用自己处理。

### 原生socket开发的问题

除了上述所讲的分布式开发方面存在的难点外，使用原生的socket开发也会有很多问题：

* 抽象程度

原生的socket抽象程度过低，接口过于底层，很多机制都需要自己封装，如Session、filter、请求抽象、广播等机制都要自已实现，工作量很大，容易出错，且有很多的重复劳动。

* 可伸缩性

高可伸缩性需考虑很多问题，消息密度、存储策略、进程架构等因素都需要考虑。用原生的socket要达到高可伸缩性，需要在架构上花费大量的功夫，而且效果也未必能达到开源框架的水准。

* 服务端的监控管理 

很多服务器的数据需要监控，例如消息密度、在线人数、机器压力、网络压力等，如果采用原生socket，所有这些都要自己开发，代价很大。 

基于框架的解决方案
======================

是的，我们需要一个框架来简化开发游戏服务器的工作。除了游戏自身的逻辑外，大部分的工作都可以用框架来解决。服务端的抽象，可伸缩性，可扩展性这些问题都可以通过框架来解决，避免了开发者重复实现一些通用的机制。游戏服务器框架也承担了应用服务器的功能，可以把框架看成容器，只要把符合容器标准的代码扔进去，容器就运行起来了。同时，它自然具备了抽象能力、可伸缩性和监控、管理等能力。

### 已有游戏服务器框架介绍

在开源社区里充斥了数不清的web服务器框架，游戏客户端的框架和库也有一大堆，但唯独游戏服务器框架少之又少，零星有一些类库，但完整的解决方案几乎没有。我们只好从商用的解决方案中拿出一些框架进行类比：

* Sun RedDwarf

RedDwarf是唯一一个能找到的完整的开源游戏服务器框架，由sun出品。可惜在它合并到Oracle以后已经停止开发了。 在设计上，RedDwarf是个分布式架构，它在分布式数据存储和任务管理上投入了太多精力，而且做的过于理想化，如动态任务迁移功能的实现非常复杂，但实际应用中根本用不到。而在可伸缩性和性能的设计上不太理想。因此RedDwarf夭折了。

* SmartfoxServer

SmartfoxServer是由意大利的一家游戏公司gotoAndPlay()推出的商用游戏服务器。 它是基于java开发的，与web应用服务器如Tomcat看上去很类似。Smartfox支持各种客户端，且有一些成功案例。它在服务端封装和监控管理方面实现得很完善。 但在可伸缩性上并不是太理想，尽管Smartfox也支持Cluster模式，但它的扩展方式是基于jvm内存复制的。也没有实现传统MMORPG基于场景分区的解决方案。 Smartfox有免费版本，但完全不开源。而且它的免费版本(达不到高并发用户要求)很大程度是为了吸引开发者最终购买它的收费版本。不限在线人数的收费版本价格达到3500美刀。

* BigWorld

Bigworld是澳大利亚Bigworld公司开发的全套3d MMORPG游戏解决方案，解决方案包含了客户端和服务端。Bigworld功能非常强大，在动态负载均衡和容错性做了很多工作。可扩展性非常强大。 它的缺点是过于重量级，对硬件要求高，且价格非常昂贵。Bigworld是专门为3d MMORPG游戏定制，但并不适用于中小型游戏的开发。

### pomelo解决方案

针对目前游戏服务器框架产品市场的情况，没有适用于中小型游戏开发的框架，我们推出了pomelo框架，它是基于node.js开发的高性能、可伸缩、轻量级游戏服务器框架，使用MIT开源协议发布。它基本解决了游戏服务器开发中的难点，使得游戏服务器的开发变得简单。与其他的类似的框架相比，它的主要优势有以下几点：

* 开发模型快速、易上手，基于convention over configuration的原则，让代码达到最大的简化。
* 架构的可伸缩性和可扩展性好，pomelo在服务器扩展和应用扩展上实现得非常方便。
* 轻量级，虽然是分布式架构，但启动非常迅速，占用资源少。
* 参考全面，框架不仅提供了完整的中英文档，还提供了完整的MMO demo代码(客户端使用了HTML5)，可以作为很好的开发参考。

##### 为什么选择node.js

在讲了这么多分布式开发的难点之后，引入node.js实在是太自然了，它天生的异步编程模型解决了分布式开发的很多问题：

* 天生的分布式

node.js之所以叫node就是因为它天生就是做多进程开发的， 多个节点(node)互相通讯交织在一起组成的分布式系统是node天生就应该这么干的。它的编程模式里天生就是这种模式，两阶段提交、异步化操作这些看似复杂的工作里在node.js只是一个正常的异步执行流程。例如前面提到的分布式事务、异步化操作在node.js里只是个正常的流程。

* 单线程的应用模型

node.js的单线程处理能力远比其它语言强大，而单线程处理游戏逻辑是最简单，最不容易出错，而且不可能出现死锁、锁竞争的情况。

* 网络io与可伸缩性的优势

游戏是非常io密集型的应用， 采用node.js是最合适的， 可达到最好的可伸缩性。虽然有很高的可伸缩性，却并没有因此损失性能。node.js生来就是为io而生的，而游戏服务器刚好是网络密集型的应用。node.js的网络编程接口简单，抽象程度高。

* 语言优势

javascript语言已经不是昔日的吴下阿蒙，使用javascript开发可以实现快速迭代。它不仅由于脚本语言的轻量、简单带来了开发效率的提升，还可以与一些类型的客户端共享部分代码，如html5，unity3d的js客户端等。另外，语言的动态性带来了很多框架设计的便利，如设计DSL，实现convention over configuration。尽管这方面比ruby稍差，但在pomelo框架中使用已经足够好了。

从游戏框架到实时应用框架
========================

当我们分析完pomelo框架的设计目标时， 我们发现核心框架的这件事情竟然与游戏没有任何关系。这是一个通用的实时分布式应用开发框架。官网上的聊天服务器demo就是一个实时应用。
事实上pomelo已经被应用在很多非游戏领域。 网易的消息推送平台是基于pomelo开发的，它承担了网易移动端和web端的消息推送， 目前已经上线使用。

总结
==========

本文首先分析了游戏服务器的特点，从而得出相对于web服务器来讲，游戏服务器由于其自身的复杂性所带了的开发难点，分析了现有游戏服务器框架的不足，阐述了设计pomelo的动机。下面是对[pomelo框架的介绍](Pomelo框架概述 "pomelo框架概述")。


* 上面我们使用了dictionary的方式对聊天应用中的路由信息进行了压缩，减少了很多通信中的额外开销。在这里，我们将使用pomelo提供的protobuf实现完成通信消息的基于protobuf的压缩。protobuf是google提出的数据交换格式，关于protobuf的更多信息请参阅[这里](https://code.google.com/p/protobuf/)。

* 原始的protobuf，首先需要定义一个.proto文件，然后调用protoc进行编译，根据不同的宿主语言，生成源码，然后将生成的源码应用到具体使用protobuf的应用中。这种使用方式比较笨重，因为涉及到了静态编译，应用程序无法在运行时动态地使用，一旦数据格式有变，就需要修改proto，编译，重新生成源码。

* pomelo的protobuf实现，借助了javascript的动态性，使得应用程序可以在运行时解析proto文件，不需要进行proto文件的编译。pomelo的实现中，为了更方便地解析proto文件，使用了json格式，与原生的proto文件语法是相通的，但是是不相同的。用户定义好客户端以及服务端的通信所需要的信息格式的proto文件，服务端的proto配置放在config/serverProtos.json中，客户端的proto配置放在config/clientProtos.json。如果在其配置文件里，配置了所有类型的proto信息，那么在通信过程中，将会全部使用二进制的方式对消息进行编码; 如果没有定义某一类消息相应的proto，pomelo还是会使用初始的json格式对消息进行编码。

chat中使用
============

下面将pomelo-protobuf应用到我们的聊天应用中，具体的代码在分支`tutorial-protobuf`中，使用下面命令切换分支：

    $ git checkout tutorial-protobuf

* 首先提取所有的数据格式，分为客户端使用的数据格式以及服务器端使用的数据格式，如下：

```javascript

// clientProtos.json
{
  "chat.chatHandler.send": {
    "required string rid": 1,
    "required string content": 2,
    "required string from": 3,
    "required string target": 4
  },

  "connector.entryHandler.enter": {
    "required string username": 1,
    "required string rid": 2
  },

  "gate.gateHandler.queryEntry": {
    "required string uid": 1
  }
}

// serverProtos.json
{
  "onChat": {
    "required string msg": 1,
    "required string from": 2,
    "required string target": 3
  },

  "onLeave": {
    "required string user": 1
  },

  "onAdd": {
    "required string user": 1
  }
}

```
* 然后将这两个配置文件分别命名为clientProtos.json和serverProtos.json中，并将这两个配置文件都放到config目录下;
* 在我们的程序中开启protobuf，在app.js的配置中，增加protobuf使用，在配置connector的时候，加入useProtobuf:

```javascript

app.configure('production|development', 'connector',  function() {
  app.set('connectorConfig', {
    connector: pomelo.connectors.hybridconnector,
    heartbeat: 3,
    useDict: true,
    useProtobuf: true //enable useProtobuf
  });
});

app.configure('production|development', 'gate', function(){
	app.set('connectorConfig', {
			connector : pomelo.connectors.hybridconnector,
			useDict: true,
      useProtobuf: true //enable useProtobuf
		});
});

```

这样，我们对我们的聊天应用进行了protobuf的压缩。当然，我们这里仅仅是为了示例，实际上，对于onAdd以及onLeave这样的，数据包本身就很小，而且又是字符串，对其使用proto压缩的效果不大，完全没必要进行使用proto压缩，而且使用protobuf压缩会造成编解码的效率开销，得不偿失。实际运用中，还是需要根据实际情况进行合理的选择，更多时候我们是在消息的压缩率和编解码的开销中达到一个平衡。

对于proto文件里面没有配置的通信数据类型，pomelo依然会使用原始的基于json的数据通信格式。

小结
============

到这里为止，我们已经实现了一个功能基本完善的聊天应用了，我们使用了pomelo提供的filter机制，基于dict的route压缩和基于protobuf的消息压缩。下面将给聊天应用增加一些纯属``“画蛇添足”``的一些功能，目的是为了继续展示pomelo的特性。下一步，[给聊天应用增加一个rpc调用](增加rpc调用 "rpc调用")。

在这部分，主要介绍pomelo是如何与客户端通信以及前端服务器是如何处理用户请求的。处理客户端的请求和响应是pomelo的核心之一，它涉及到了很多组件，包括session组件，server组件，connection组件，connector组件，proxy组件，remote组件等。在本部分，我们仅仅介绍与前端服务器相关的组件，以及他们的作用，对于rpc以及后端服务器以来的backendSession以及channel，这里不做深入介绍，将在其他部分进行介绍。

对于前端服务器来说，session组件是sessionService的包装组件，用来维护用户的session信息；connection组件是connectionService的包装组件，是用来做连接统计的；connector组件会开启监听接口，承受客户端的连接，这里对connector组件底层使用的具体的connector不做太多关注，只关心其抽象行为。

对于server组件来说，会维护服务器的Handler和HandlerFilter，当用户的请求到达前端服务器时，如果前端服务器定义了相应的Handler，那么前端服务器会使用filter-handler链对其进行处理，然后将处理后的结果返回；如果对请求路由检查发现请求是发向到后端服务器的，那么前端服务器会根据用户配置的router（也可能是默认的），计算出要发往的后端服务器id，然后发起rpc调用，后端服务器在接收到rpc调用时，从其中取出请求路由以及请求参数，发起filter-handler链对请求进行处理，完成调用，并将响应发给前端服务器，前端服务器再将响应发送到客户端，整个处理流程如下如所示:

<center>
![request-flow](images/requst-flow.png)
</center>

下面的类图粗略地展示了这些类之间的关系:

<center>
![pomelo](images/server.png)
</center>

下面通过类时序图的方式，选取典型的用例行为，来介绍框架的控制流程:

<center>
![server](images/sd_server.png)
</center>

#### 初始化

* 在CoConnector的afterStart回调中，会开启socket的监听，端口使用服务器配置中的clientPort，然后就可以接受用户的连接了，并绑定了connctor的connection事件。

* 在CoServer的start回调里，会扫描当前服务器应该加载的Handler和HandlerFilter，并完成Handler和Filter的加载。此时已经做好了接收客户端连接的准备。

#### 客户端连接

当客户端连接到前端服务器时，会触发connector的监听事件，在事件的处理中，会通过CoConnection增加连接信息，用来做统计。会对连接返回的用来数据通信的socket绑定message，close，error，disconnect等事件，然后创建session，session由CoSession包装的SessionService维护。每一个session都会维护与其相关的socket。此时，客户端已经完成了与服务器端的连接。

#### 客户端请求

* 当客户端连接完成后，客户端就会发起请求，请求会触发socket的message事件，在此事件处理中，首先会对message事件所携带的包进行解包,然后将请求交给CoServer处理。如果请求的是前端服务器的Handler，那么CoServer的doHandle中将会发起其filter-handler链，完成请求的处理，最常见的这种请求就是用户登录请求。如果请求的路由不是前端服务器的，那么CoServer的doFoward将会发起sys rpc给相应的后端rpc。当发起sys rpc调用时，由于同类型的后端服务器一般都有很多，故需要做一个路由选择。这个路由选择策略用户可以配置，通过app.route调用，如果用户不配置的话，pomelo会使用一个默认的路由配置。后端服务器接受到请求后，会执行其CoServer的doHandle，跟前端服务器一样，会使用filter-handler链，对用户的请求进行处理，然后将响应返回给前端服务器，并由前端服务器将响应发送到客户端。

* 前端服务器会调用connector的send函数将响应或者推送的消息发送给客户端，send调用不会直接将要发送的消息通过socket直接发送给客户端，而是将发送任务调度给CoPushScheduler，CoPushScheduler可以实现具体的发送策略。pomelo中提供了两种方式的pushScheduler，direct会立即将用户的响应发送给用户，buffer则会缓冲发送任务，并按时冲刷，pomelo默认使用的是direct的方式，如果想使用buffer的方式，可以通过如下的调用启用:
```javascript
    app.set('pushSchedulerConfig', {scheduler: pomelo.pushSchedulers.buffer, flushInterval: 20});
```
这里，flushInterval是定时冲刷的周期，我们也可以自己定制实现相应的scheduler，并配置到应用程序中。

* 当服务器的请求处理逻辑需要给客户端推送消息时，会通过用户的uid或者session id从SessionService里获得到对应的Session，session中会维护与客户端用来数据通信的socket，然后将要推送的数据通过session维护的socket连接发送到客户端。

#### 绑定/解绑用户

* 一般来说，当session连接完成后，都会有用户登录的请求，从而完成session与具体用户的绑定。一般在CoServer的处理中，当会将相应的用户绑定到session上，此时会调用CoSession包装的SessionService的操作bind完成对应的用户绑定操作。此外，还会调用CoConnection的addLoginedUser来增加用户，维护统计信息。

* 对于用户注销的请求，一般在CoServer的处理中，会完成session与uid的解绑，此时会调用CoSession包装的SessionService的操作unbind完成对应用户的解绑操作。此外，还会调用CoConnection的removeLoginedUser来减少登录用户，维护统计信息。


#### 客户端断开

当客户端断开连接时，connector监听的socket上会激发disconnect事件，在具体的事件处理中，会从SessionService中删除掉对应的Session，释放掉session维护的连接，还会调用ConnectionService上decreaseConnectionCount，维护统计信息。


上面选取了客户端与服务器交互的几个典型行为，说明了整个客户端请求中的控制流程。这里仅仅涉及到了前端服务器，对于后端服务器的具体处理，这里仅仅提到了会发起rpc调用，而没有具体地深入介绍。

Pomelo中的请求处理链
==========================

在pomelo中，HandlerFilter分为beforeFilter和afterFilter，对于beforeFilter来说,其方法签名为

    before(msg, session, next);

其中msg是请求，session表示当前请求的session，在前端服务器的话是FrontendSession，在后端服务器的话是BackendSession，next是用来组成请求链的，是用来指定下一步调用的。如果在具体的filter上没有错误的话，那么就直接调用next(), 否则，则调用next(err, resp),向后面传递具体的处理错误以及响应。在filter的具体实现中，在逻辑处理完后，必须调用next，否则将打断整个处理链。如果有任意一个beforeFilter的next调用中传递了err的话，此处理链将会立即被中断，直接会转入错误处理。在next传递err的时候，可以携带一个resp参数，作为对客户端错误的响应，即next(err, resp)。

具体Handler的签名一般为：

    <handler_Name>(msg, session, next);

msg是经过beforeFilter链处理过的msg，session是经过beforeFilter链处理后的session，next是下一步处理。如果需要给客户端响应的话，没有错误的话，使用next(null, resp),否则可以使用next(err, resp),向后面传递错误信息。这里，resp是给客户端的响应，一般来说客户端的响应都是在Handler的具体逻辑中生成。在具体Handler的实现中，也必须调用next。其next语义与前面的beforeFilter中的next语义一致。

对于afterFilter来说，其方法签名为:

    after(err, msg, session, resp, next);

afterFilter是做一些清理操作的，在执行afterFilter链的时候，具体的响应已经发送给了客户端，也就是说在afterFilter如果对resp做更改的话，将对客户端响应没有任何影响。同样，这里的next参数，也是指定了下一步的处理,其签名是next(err),不过与上面beforeFilter和Handler不同的是，由于在afterFilter中常做的是一些清理操作，而且此时具体的响应resp已经发送到了客户端，所以afterFilter中，处理链对err将不再敏感，无论是否有err，整个afterFilter链都会执行完毕。

ErrorHandler，是当在处理请求时产生异常时进行的处理，具体的签名为:

    <errorHandler_Name>(err, msg, resp, session, cb);

在beforeFilter或者Handler中，如果处理产生错误，那么将会转向错误处理，ErrorHandler就是用来进行错误处理的，具体的参数意义跟上面的一样，其中resp是由前面产生错误的next(err, resp)调用传递来的，cb的签名为cb(err, resp),cb会将resp发送给客户端。因此在ErrorHandler里面，是需要调用cb(err, resp), 否则，客户端将得不到服务器端的响应。在errorHandler中可以根据传入的resp以及err信息，重新生成要发送给客户端的resp。通过如下方式设置全局的ErrorHandler，

    var errorHandler = require('<path');
    app.set('errorHandler', errorHandler);

如果用户没有配置全局的errorHandler的话，默认的errorHandler会向客户端返回由beforeFilters或者Handler产生的resp。整个请求处理链的大致流程如下：

<center>
![handle-flow](images/handle-flow.png)
</center>



pomelo内建filter
=================

pomelo内建了常见的一些filter，用户可以通过如下的方式启用:

    app.filter(pomelo.filters.<filterName>(<args>));

下面介绍一下这几个fitler:

####  serial

这个filter是用来对用户请求做串行化的，可以使得用户的请求只有在第一个请求被处理完后，才会处理第二个请求。serial中使用了一个taskManager，当用户请求到来时，在beforeFilter中，将用户的请求放到taskManager中，taskManager中维护着一个task队列。在对应的afterFilter中，如果taskManager还有未处理的请求，将会处理其请求，即在一个请求的afterFilter里启动在taskManager中还没处理的下一个请求，这样就实现了请求的序列化。

#### timeout

这个filter是用来对服务端处理超时进行警告的，在beforeFilter中会启动一个定时器，在afterFilter中清除。如果在其定时器时间内，afterFilter被调用，定时器将会被清除，因此不会出现超时警告。如果定时器超时时，afterFilter还没有执行到，则会引发超时警告,并记录日志。默认的处理超时是3秒，可以在加载timeout的时候作为参数传入。

#### time

这个filter使用来记录服务器处理时间的，在beforeFilter中会记录一下当前的时间戳，在afterFilter中再次获取当前的时间戳，然后两个时间戳相减，得到整个处理时间，然后记录日志。

#### toobusy

这个filter中，一旦检测到node.js中事件循环的请求等待队列过长，超过一个阀值时，就会触发toobusy。一旦触发了toobusy，那么toobusy的filter中将终止此请求处理链，并在next调用中，传递错误参数。


总结
==========

在本部分，介绍了前端服务器与客户端的通信的相关内容，讲述了相关的类关系，以及典型用例行为的控制流程。对于请求响应链中的before filter，handler，after fitler，error handler等做了较为详细的分析，最后简单分析了一下pomelo内建提供的一些filter。

pomelo核心提供了两种connector，sioconnector和hybridconnector。其中sioconnector基于socket.io，使用json作为其通信格式，hybridconnector则用于tcp/websocket的通信，它底层使用的是二进制协议。虽然在sioconnector中，socket.io的实现很好，对于超时、握手等都做了处理，并且使用json作为通信格式，方便了协议的定制和修改，但同时也带来了较多的通讯冗余数据。hybridconnector则是使用了二进制版本通讯协议，同时提供了route字典压缩和protobuf压缩，提高带宽利用率，以满足诸如移动环境的需求，同时上层接口仍保持json格式的接口，对以前版本之前的代码不产生任何影响，保留兼容性。在本部分，主要介绍hybridconector实现的具体的通信协议。

pomelo的二进制协议包含两层编码：package和message。message层主要实现route压缩和protobuf压缩，message层的编码结果将传递给package层。package层主要实现pomelo应用基于二进制协议的握手过程，心跳和数据传输编码，package层的编码结果可以通过tcp，websocket等协议以二进制数据的形式进行传输。message层编码可选，也可替换成其他二进制编码格式，都不影响package层编码和发送。

Pomelo协议层的结构如下图所示：

<center>
![Pomelo Protocol](images/data-tran.png)
</center>

pomelo package
=======================

package协议主要用来封装在面向连接的二进制流的通讯协议（如：tcp）上的pomelo数据包。package分为控制包和数据包两种类型。前者用来实现pomelo应用层面的控制流程，包括客户端和服务器的握手，心跳和服务器主动断开连接的通知等控制信息。后者则是用来在客户端和服务器之间传输应用数据。

#### package格式

package分为header和body两部分。header描述package包的类型和包的长度，body则是需要传输的数据内容。具体格式如下：

<center>
![pomelo package](images/pomelo-pack.png)
</center>

* type - package类型，1个byte，取值如下。
	- 0x01: 客户端到服务器的握手请求以及服务器到客户端的握手响应
	- 0x02: 客户端到服务器的握手ack
	- 0x03: 心跳包
	- 0x04: 数据包
	- 0x05: 服务器主动断开连接通知
* length - body内容长度，3个byte的大端整数，因此最大的包长度为2^24个byte。
* body - 二进制的传输内容。

各个package类型的具体描述和控制流程如下。

#### 握手

握手流程主要提供一个机会，让客户端和服务器在连接建立后，进行一些初始化的数据交换。交换的数据分为系统和用户两部分。系统部分为pomelo框架所需信息，用户部分则是用户可以在具体应用中自定义的内容。

握手的内容为utf-8编码的json字符串（不压缩），通过body字段传输。

握手请求：

```javascript
{
  "sys": {
    "version": "1.1.1",
    "type": "js-websocket"
  }, 
  "user": {
  	// any customized request data
  }
}
```

* sys.version - 客户端的版本号。每个客户端SDK的每一个版本都有一个固定的版本号。在握手阶段客户端将该版本号上传给服务器，服务器可以由此来判断当前客户端是否合适与服务器通讯。
* sys.type - 客户端的类型。可以通过客户端类型和版本号一起来确定客户端是否合适。

握手响应：

```javascript
{
  "code": 200, 			// response code
  "sys": {
    "heartbeat": 3, 	// heartbeat interval in second
    "dict": {}, 		// route dictionary
    "protos": {}		// protobuf definition data
  }, 
  "user": {
  	// any customized response data
  }
}
```

* code - 握手响应的状态码。目前的取值：200代表成功，500为处理用户自定义握手流程时失败，501为客户端版本号不符合要求。
* sys.heartbeat - 可选，心跳时间间隔，单位为秒，没指定表示不需要心跳。
* dict - 可选，route字段压缩的映射表，没指定表示没有字典压缩。
* protos - 可选，protobuf压缩的数据定义，没有表示protobuf压缩。
* user - 可选，用户自定义的握手数据，没有表示没有用户自定义的握手数据。

握手的流程如下：

<center>
![handshake](images/pomelo-handshake.png)
</center>

当底层连接建立后，客户端向服务器发起握手请求，并附带必要的数据。服务器检验握手数据后，返回握手响应。如果握手成功，客户端向服务器发送一个握手ack，握手阶段至此成功结束。

#### 心跳

心跳包的length字段为0，body为空。

心跳的流程如下：

<center>
![heartbeat](images/pomelo-heartbeat.png)
</center>

服务器可以配置心跳时间间隔。当握手结束后，客户端发起第一个心跳。服务器和客户端收到心跳包后，延迟心跳间隔的时间后再向对方发送一个心跳包。

心跳超时时间为2倍的心跳间隔时间。服务器检测到心跳超时并不会主动断开客户端的连接。客户端检测到心跳超时，可以根据策略选择是否要主动断开连接。

#### 数据

数据包用来在客户端和服务器之间传输数据所用。数据包的body是由上层传下来的任意二进制数据，package层不会对body内容做任何处理。

#### 服务器主动断开

当服务器主动断开客户端连接时（如：踢掉某个在线玩家），会先向客户端发送一个控制消息，然后再断开连接。客户端可以通过这个消息来判断是否是服务器主动断开连接的。

pomelo message
===================

message协议的主要作用是封装消息头，包括route和消息类型两部分，不同的消息类型有着不同的消息头，在消息头里面可能要打入message id(即requestId)和route信息。由于可能会有route压缩，而且对于服务端push的消息，message id为空，对于客户端请求的响应，route为空，因此message的头格式比较复杂。

消息头分为三部分，flag，message id，route。如下图所示：

<center>
![Message Head](images/message-header.png)
</center>

从上图可以看出，pomelo消息头是可变的，会根据具体的消息类型和内容而改变。其中：
* flag位是必须的，占用一个byte，它决定了后面的消息类型和内容的格式; 
* message id和route则是可选的。其中message id采用[varints 128变长编码](https://developers.google.com/protocol-buffers/docs/encoding#varints)方式，根据值的大小，长度在0～5byte之间。route则根据消息类型以及内容的大小，长度在0～255byte之间。

### 标志位flag

flag占用message头的第一个byte，其内容如下

<center>
![flag](images/message-flag.png)
</center>

现在只用到了其中的4个bit，这四个bit包括两部分，占用3个bit的message type字段和占用1个bit的route标识，其中：
* message type用来标识消息类型,范围为0～7，现在消息共有四类，request，notify，response，push，值的范围是0～3。不同的消息类型有着不同的消息内容，下面会有详细分析。
* 最后一位的route表示route是否压缩，影响route字段的长度。
这两部分之间相互独立，互不影响。

### 消息类型

不同类型的消息，对应不同消息头，消息类型通过flag字段的第2-4位来确定，其对应关系以及相应的消息头如下图：

<center>
![Message Head Content](images/message-type.png)
</center>

上面的 **-** 表示不影响消息类型的bit位。

### route压缩标志位

route主要分为压缩和未压缩两种，由flag的最后一位（route压缩标志位）指定，当flag中的route标志为0时，表示未压缩的route，为1则表示是压缩route。route通过系统生成和用户自定义的字典进行压缩，具体内容见[pomelo压缩协议](消息压缩)。route字段的编码会依赖flag的这一位，其格式如下图:

<center>
![Message Type](images/route-compre.png)
</center>

上图是不同的flag标志对应的route字段的内容：
* flag的最后一位为1时，后面跟的是一个uInt16表示的route字典编号，需要通过查询字典来获取route;
* flag最后一位为0是，后面route则由一个uInt8的byte，用来表示route的字节长度。之后是通过utf8编码后的route字符串，其长度就是前面一位byte的uInt8的值，因此route的长度最大支持256B。

总结
=========

在本部分，介绍了pomelo提供的hybridconnector的线上协议，包括package层和message层。当用户使用hybridconnector的时候，可以根据这里提供的协议信息，在客户端可以依据此协议完成与服务端的通信。
在这部分，我们来介绍如果配置框架。我们知道在pomelo中，可以配置各个组件的选项，加载配置文件，开启pomelo的特性等等。这一切配置都是在game-server/app.js中进行的。实际上，在pomelo的应用中有两个app.js,一个在game-server目录下，一个在web-server目录下。其中game-server下的app.js是整个游戏服务器的入口和配置点，而web-server下的app.js则是web服务器入口。在这里，我们仅仅介绍如何在game-server/app.js中配置框架以及pomelo框架使用的服务器配置文件的格式。



app.js文件
===================

app.js是运行pomelo项目的入口，在app.js中，首先会创建一个app的实例，这个app作为整个框架的配置上下文来使用,用户可以通过这个上下文，设置一些全局变量，加载配置信息等等操作。app.js中的一般代码如下：
```javascript

var pomelo = require('pomelo');
var app = pomelo.createApp();

// some configuration

app.configure(<env>, <serverType>, function() {
 
});

app.configure(....);
app.set(...);
app.route(...);

// ...

// start app
app.start();

```
首先会创建一个app实例，然后是一些通过app这个上下文对框架的一些配置以及一些初始化操作，最后启动应用。这里我们将主要关注对框架的配置部分。

使用app.configure调用来配置
========================

服务器的配置主要由configure()方法完成，完整的app.configure配置参数如下：

```javascript
app.configure([env], [serverType], [function]);
```

前两个参数是可选的， 以下是参数说明：
* env: 运行环境， 可设成development, production或development|production
* serverType: 服务器类型，设置了这个参数只会对当前参数类型服务器做初始化，不设置则对所有服务器执行初始化function 
* function: 具体的初始化操作， 内部可以写任何对框架的配置操作逻辑。

以下是一些配置实例：

#### 实例一
```javascript
app.configure(function(){
    // do some configuration
});
```

这种配置将对所有模式(development/production)下的所有服务器生效，它等价于在app.js中，不调用configure，直接执行相关的配置，代码示例如下：

```javascript

app.configure(function() {
    doSomeConfiguration();
  });

// <==>

doSomeConfiguration(); // equivalent to above `app.configure`

```

#### 实例二
```javascript
app.configure('development', function(){
    // do some configuration just for development env only.
});
```

这种配置则只针对development模式下所有服务器生效，同样在这里可以填入任何配置。

#### 实例三
```javascript
app.configure('development', 'chat', function(){
    // do some configuration just for development env and chat server only.
});
```

这种配置则针对development模式下的chat服务器生效，这里同样可以填入任何配置。

#### 配置内容

在configure中用户可以根据应用的不同需求在不同的服务器中进行相关配置，例如在全局设置mysql参数：

```javascript
app.configure('development|production', function(){
     app.loadConfig('mysql', app.getBase() + '/config/mysql.json');
});
```
另外也可以选择在具体的服务器中进行应用的配置，例如可以做一些初始化操作：
```javascript
var initArea = function(){
   //area init
};
app.configure('development|production', 'area', function(){
     initArea();
});

```

而更多地，可以在configure中，针对不同的服务器，不同的环境，对框架进行不同的配置。这些配置包括设置一个上下文变量供应用使用，开启一些功能选项，配置加载一个自定义的component，针对不同的服务器，配置filter等等配置操作，如下所示:
```javascript
app.configure('development|production', 'chat', function() {
    app.route('chat', routeUtil.chat);
});

app.enable('systemMonitor');

app.configure('development|production','gate', function() {
    app.set('connectorConfig', {
       connector: pomelo.connectors.hybridconnector,
       heartbeat: 3
       });
    }); // configure connector for gate server
```

下面就对这些框架配置作些介绍。

上下文变量存取
==================

上下文对象app提供了设置和获取应用变量的方法，其签名为：
```javascript
app.set(name, value, [isAttach]);
app.get(name);
```
* 如上，对于set来说，有三个参数，分别是变量名，变量的值以及一个可选的参数isAttach。如果isAttach设置为true的话，那么表示将变量attach到app对象上，作为app的一个属性，以后对此变量的访问，可以直接通过app.name进行访问，这个参数默认为false。
* 对于get调用，就是一个很简单的通过变量名获取变量值。

示例代码如下:
```javascript
app.set('server',server);
var server = app.get('server');

app.set('service', service, true);
var service = app.service;
```

在pomelo中框架中，可以通过app.set给pomelo的组件配置相应的选项，也可以通过app.get获得到pomelo框架加载的服务，如backendSessionService，channelService等等，示例代码如下:

```javascript

app.set('connectorConfig', {
  // ...
}); // set opts for connector component

var backendSessionService = app.get('backendSessionService'); // get backendSessionService instance
```

如果用户需要自己设置一些自己的自定义变量，也可以通过app这个上下文实现获取和设置。

开启和关闭功能选项
===================

应用的功能选项配置可以通过enable和disable来打开和关闭。另外，用户可以通过enabled和disabled对相应的状态进行判断，如果该状态存在则返回true,反之返回false。例如要打开或者关闭应用的rpc debug log并查看其状态是否存在, 示例代码如下：

```javascript
app.enable('rpcDebugLog');
app.enabled('rpcDebugLog'); // return true
app.disable('rpcDebugLog');
app.disabled('rpcDebugLog'); //return true
```

在pomelo框架中，当需要做更详细的监控管理的时候，可以打开systemMonitor选项，打开systemMonitor选项会使得默认加载额外的admin-module，示例代码如下：

```javascript
app.enable('systemMonitor'); // enable system monitor
```

同样，用户可以设置自己应用的一些功能选项，并通过enable，disable，enabled，disabled来进行开启关闭以及检查。

加载配置文件
==============
用户可以通过loadConfig加载配置文件，加载后文件中的参数将直接挂载到app对象上。例如需要加载mysql.json文件，示例代码如下：

```json
{
  "development":
    {
      "host":"127.0.0.1",
      "port":"3306",
      "database":"pomelo" 
    }
}
```
然后，加载完成后，就可以直接通过app对象，访问具体的配置参数，示例代码如下：
```javascript
app.loadConfig('mysql', path.resolve('./config/mysql.json'));
var host = app.get('mysql').host; //返回 127.0.0.1
```
当然，用户可以使用loadConfig的调用加载任何json格式的配置文件，用于其他的目的，并能通过app进行访问。需要注意的是所有的json配置文件中都要指定具体的模式，也就是development或者production。

加载component
===================

pomelo的功能由其component提供，pomelo会默认根据服务器的类型加载不同的内建组件，另外用户可以根据应用需求自定义组件。组件的加载主要是使用load方法，示例代码如下：
```javascript
app.load(HelloWorldComponent, [opts]); //opts is optional
```

加载plugin
===========
pomelo还可以加载自定义的插件，一个插件由多个component和一组对应用的事件进行响应的事件处理组成，加载插件使用app.use, 示例代码如下：

```javascript
// app.use(<plugin>, <plugin options>);

var statusPlugin = require('pomelo-status-plugin');

app.use(statusPlugin, {
 status:{
  host: '127.0.0.1',
  port: 6379
 }
});
```

配置router
==============

router主要负责请求路由信息的维护，路由计算，路由结果缓存等工作，并能根据需要切换路由策略，更新路由信息等。用户可以自定义不同服务器的不同路由规则，然后进行配置即可。以下示例为chat服务器配置路由规则：

```javascript
//routeUtil.js
app.route('chat', routeUtil.chat);
```

在routerUtil中可以具体的定义不同服务器的路由规则，例如：

```javascript
routeUtil.chat = function(session, msg, app, callback) {
    var chatServers = app.getServersByType('chat'); 
    if (!chatServers) {
     	callback(new Error('can not find chat servers.'));
		return;
    }
    var server = dispatcher.dispatch(session.rid, chatServers);
    callback(null, server.id);
};
```
在路由函数中，通过最后的回调函数中返回服务器的id即可，这里使用dispatcher对session.rid进行hash处理从而完成服务器选择。用户可以根据自己的实际需求进行配置相应的router。


配置filter
=============

当一个客户端请求到达服务器后，经过filter链和handler处理，最后生成响应返回给客户端。handler是业务逻辑实现的地方，filter则是执行业务前进行预处理和业务处理后清理的地方。为了开发者方便，系统内建提供了一些filter，例如：serialFilter,timeFilter，timeOutFilter，另外用户可以根据应用的需要自定义filter。配置filter的调用示例如下：

```javascript
app.filter(pomelo.filters.serial()); // use builtin filter: serial filter

app.filter(FooFilter); // use FooFilter as a before & after filter

app.before(beforeFilter); // use beforeFilter as a before filter

app.after(afterFilter); // use afterFilter as an after filter
```

用户可以自定义自己的filter，然后通过app.filter调用，将其配置进框架。如果仅仅是before filter，那么就调用app.before，如果是after filter，就掉用app.after，如果既定义了before filter又定义了after filter，那么就可以使用app.filter调用了。

配置admin-module
=================

pomelo 提供了监控管理框架，可以给其配置不同的admin module，具体的配置使用调用app.registerAdmin，示例代码如下：

```javascript
    app.registerAdmin(require('../modules/watchdog'), {app: app, master: true});
```
用户也可以自定义自己的module，然后通过registerAdmin调用，加载到框架。

服务器配置文件格式
==================

pomelo的配置文件都在game-server/config目录下，其中有两个很重要的服务器配置文件servers.json和master.json。
所有的配置文件中，都分为development和production两种配置模式，以对应具体的是开发调试环境还是具体的产品环境，其配置字段如下:

master.json中:

* id: master 服务器的服务器id，是一个字符串;
* host: master 服务器的host，可以是一个ip或域名;
* port: master服务器开的端口，默认是3005;
* args: 可选的，在这里配置的参数选项，是用来给node/v8使用的，如你可以配置`"args": "--debug=5858"`,这样的话，就可以开启调试。


servers.json中:

* id: 应用服务器的服务器id，是一个字符串;
* host: 应用服务器的host，可以是一个ip或域名;
* port: 接受rpc请求时使用的端口号，对于后端服务器来说必须的，对于前端服务器来说，如果仅仅像gate服务器那样，并不维护具体的客户端连接，仅仅给客户端返回可以连接的前端服务器的地址信息的话，port则是可以省略的。一般来说，port不应该省略;
* frontend: 是一个boolean值，对于前端服务器，配置为true，如果省略的话，则默认为false。后端服务器不配置;
* clientPort: 这是前端服务器接受客户端连接启用的端口，对于后端服务器来说，不需要配置，对于前端服务器，则是必需的。
* max-connections: 可选的，用来说明前端服务器最多承受的连接数，如果超过了这个连接数，则后来的连接将会会connector拒绝;
* args: 可选的，同master中的语义一样。

总结
==========
在这部分，介绍了在app.js如何配置整个框架并在最后给出了服务器配置文件的格式。通过application的configure等调用，可以给不同的服务器完成不同的配置，比如，配置router，配置filter，为特定类型的服务器加载自定义的component等等。同样，在这里，也可以做一些初始化的加载操作，比如，当应用需要数据库时，可以加载mysql的配置文件，并将配置信息设置到app上下文中，这样在应用中，就可以通过app直接获取到对应的配置信息。
使用pomelo做服务端开发时，无论什么客户端，只要能遵循与服务端的线上协议，就能够与服务端建立通信。pomelo内建提供的sioconnector和hybridconnector都定义了自己的协议格式，其中sioconnector用于socket.io的通信，hybridconnector则用来处理websocket和tcp的连接通信。为了方便客户端的开发，pomelo提供了部分平台的客户端SDK，这里主要会介绍一下用于Web端的JavaScript的SDK以及基于C语言的libpomelo的使用。

Web端JavaScript开发库
=======================

对于浏览器来说，HTML5中已经支持了websocket，因此使用支持websocket的浏览器可以直接与服务端的hybridconnector建立通信。而对于比较旧的浏览器来说，还没有支持websocket的，可以使用基于socket.io的方式进行与服务端建立连接。因此，对于Web端，pomelo提供了两套开发库，分别适用于支持websocket的浏览器和不支持websocket的浏览器，这两套开发库的链接如下，适用于socket.io的[pomelo-jsclient-socket.io](https://github.com/pomelonode/pomelo-jsclient-socket.io)以及适用于websocket的[pomelo-jsclient-websocket](https://github.com/pomelonode/pomelo-jsclient-websocket)。

#### socket.io的客户端开发库

  对于使用socket.io的客户端SDK来说，其依赖[socket.io-client](https://github.com/learnboost/socket.io-client/), 由于这个库在使用[component](https://github.com/component/component/)进行管理时有bug，因此在使用的时候，是直接引用其提供的js文件，具体引用的js文件为[socket.io-client.js](https://github.com/LearnBoost/socket.io-client/blob/master/socket.io-client.js)。对于pomelo-jsclient-socket.io来说，同样也是直接使用引用其js文件，也即是[pomelo-client.js](https://github.com/pomelonode/pomelo-jsclient-socket.io/blob/master/lib/pomelo-client.js)。在直接引用这两个文件后即可使用pomelo的调用了。

#### websocket的客户端开发库

对于使用websocket的客户端SDK来说，使用了[component](https://github.com/component/component/)进行管理，因此只需要配置一个component.json文件，里面配置相应的依赖，然后运行

    $ component install
    $ component build

component会自动寻找依赖，完成客户端js的打包。用户只需要引用编译后的build.js即可，然后就可以使用pomelo的调用了。关于component的使用，请参考component的wiki。我们的例子[chatofpomelo-websocket](https://github.com/NetEase/chatofpomelo-websocket/tree/master/web-server/public/js/lib)，这里就是使用了component来管理前端js的，可以作为用户使用的一个参考。

<a name="clientAPI"/>
#### web端API简介

无论是socket.io的还是websocket的，都提供了统一的API，下面对这些API进行简单的介绍。

* pomelo.init(params, cb)

这是往往是客户端的第一次调用，params中应该指出要连接的服务器的ip和端口号，cb会在连接成功后进行回调;

* pomelo.request(route, msg, cb)

请求服务，route为服务端的路由，格式为"<ServerType>.<HandlerName>.<MethodName>", msg为请求的内容，cb会响应回来后的回调;

* pomelo.notify(route, msg)

发送notify，不需要服务器回响应的，因此没有对响应的回调，其他参数含义同request;

* pomelo.on(route, cb)

这个是从EventEmmiter继承过来的方法，用来对服务端的推送作出响应的。route会用户自定义的，格式一般为"onXXX";

* pomelo.disconnect()

这个是pomelo主动断开连接的方法。

libpomelo
===============

libpomelo 是 [pomelo](https://github.com/NetEase/pomelo) 的 c 客户端，支持pomelo 0.3版本以后的协议  

### 依赖
* [libuv](https://github.com/joyent/libuv) 跨平台开发库，主要使用了网络I/O和线程  
* [jansson](https://github.com/akheron/jansson) c 的 json 解析库  

### 使用
#### 创建客户端实例
```
// create a client instance.
pc_client_t *client = pc_client_new();
```

#### 添加事件监听
```
// add some event callback.
pc_add_listener(client, "onHey", on_hey);
pc_add_listener(client, PC_EVENT_DISCONNECT, on_close);
```

#### 监听器的定义
```
// disconnect event callback.
void on_close(pc_client_t *client, const char *event, void *data) {
  printf("client closed: %d.\n", client->state);
}
```

#### 连接到服务器
```
struct sockaddr_in address;

memset(&address, 0, sizeof(struct sockaddr_in));
address.sin_family = AF_INET;
address.sin_port = htons(port);
address.sin_addr.s_addr = inet_addr(ip);

// try to connect to server.
if(pc_client_connect(client, &address)) {
  printf("fail to connect server.\n");
  pc_client_destroy(client);
  return 1;
}
```

#### 发起一个 notify 请求
```
// notified callback
void on_notified(pc_notify_t *req, int status) {
  if(status == -1) {
    printf("Fail to send notify to server.\n");
  } else {
    printf("Notify finished.\n");
  }

  // release resources
  json_t *msg = req->msg;
  json_decref(msg);
  pc_notify_destroy(req);
}

// send a notify
void do_notify(pc_client_t *client) {
  // compose notify.
  const char *route = "connector.helloHandler.hello";
  json_t *msg = json_object();
  json_t *json_str = json_string("hello");
  json_object_set(msg, "msg", json_str);
  // decref json string
  json_decref(json_str);

  pc_notify_t *notify = pc_notify_new();
  pc_notify(client, notify, route, msg, on_notified);
}
```

#### 发起一个 requst 请求
```
// request callback
void on_request_cb(pc_request_t *req, int status, json_t *resp) {
  if(status == -1) {
    printf("Fail to send request to server.\n");
  } else if(status == 0) {
    char *json_str = json_dumps(resp, 0);
    if(json_str != NULL) {
      printf("server response: %s\n", json_str);
      free(json_str);
    }
  }

  // release relative resource with pc_request_t
  json_t *msg = req->msg;
  pc_client_t *client = req->client;
  json_decref(msg);
  pc_request_destroy(req);

  // stop client
  pc_client_stop(client);
}

// send a request
void do_request(pc_client_t *client) {
  // compose request
  const char *route = "connector.helloHandler.hi";
  json_t *msg = json_object();
  json_t *str = json_string("hi~");
  json_object_set(msg, "msg", str);
  // decref for json object
  json_decref(str);

  pc_request_t *request = pc_request_new();
  pc_request(client, request, route, msg, on_request_cb);
}
```

### API 接口  
* 创建一个新的pomelo client实例  
```
pc_client_t *pc_client_new();
```

* 停止客户端的连接  
该接口适合于在libuv子线程中调用，然后在主线程中，通过 pc_client_join来wait子线程退出  
```
void pc_client_stop(pc_client_t *client);
```

* 销毁客户端的连接  
```
void pc_client_destroy(pc_client_t *client);
```

* 主线程中调用等待子线程的退出  
```
int pc_client_join(pc_client_t *client);
```

* 创建一个request请求实例  
```
pc_request_t *pc_request_new();
```

* 销毁一个request请求实例  
```
void pc_request_destroy(pc_request_t *req);
```

* 连接到服务器，在连接过程中会创建子线程用于处理网络I/O  
```
int pc_client_connect(pc_client_t *client, struct sockaddr_in *addr);
```

* 销毁pc_connect_t类型的实例  
```
void pc_connect_req_destroy(pc_connect_t *conn_req);
```

* 发起一个request请求  
```
int pc_request(pc_client_t *client, pc_request_t *req, const char *route,
               json_t *msg, pc_request_cb cb);
```

* 创建一个notify请求实例  
```
pc_notify_t *pc_notify_new();
```

* 销毁一个notify请求实例  
```
void pc_notify_destroy(pc_notify_t *req);
```

* 发起一个notify请求  
```
int pc_notify(pc_client_t *client, pc_notify_t *req, const char *route,
              json_t *msg, pc_notify_cb cb);
```

* 添加一个事件监听  
```
int pc_add_listener(pc_client_t *client, const char *event,
                    pc_event_cb event_cb);
```

* 删除一个事件监听  
```
void pc_remove_listener(pc_client_t *client, const char *event,
                    pc_event_cb event_cb);
```

* 触发一个事件监听  
```
void pc_emit_event(pc_client_t *client, const char *event, void *data);
```

### 编译
#### 前提条件
下载 [gyp](http://code.google.com/p/gyp/source/checkout)  
gyp 其实是一个python写的脚本，并不需要安装，只需要下载下来，可以执行gyp里面的脚本就行  

#### Mac 环境
```
./pomelo_gyp
xcodebuild -project pomelo.xcodeproj
```

#### IOS 环境
```
./pomelo_gyp -DTO=ios
./build_ios
```

#### IOS 模拟器
```
./pomelo_gyp -DTO=ios
./build_iossim
```

#### Linux 环境
```
./pomelo_gyp
make
```

#### Windows 环境
在libpomelo项目跟目录下  
打开[git bash](https://help.github.com/articles/set-up-git#platform-windows)，敲入  
```
mkdir -p build
git clone https://github.com/martine/gyp.git build/gyp
```
之后，打开windows cmd命令行窗口，并且cd切换目录到libpomelo跟目录下面，敲入    
```
build\gyp\gyp.bat --depth=. pomelo.gyp -Dlibrary=static_library -DTO=pc 
```
之后就会生成pomelo.sln，使用visual studio打开即可进行编译  


#### Android 环境
开发前提条件：   
windows:   
* 安装 [Cygwin](http://www.cygwin.com/) with make (select make package from the list during the install).    
* android adt eclipse 这个只要下载最新的 android sdk 里面就有一个配置好环境的 eclipse    

环境搭建：    
1: 新建一个 android 工程，比如新建一个 test 的 工程，建完之后如图：  
![test工程](http://ww3.sinaimg.cn/large/6a98ae6cgw1e3ym2kkdofj207x0f0q3t.jpg)


2: 然后在项目根目录下面，新建一个 jni 文件夹  
然后里面添加一个 Android.mk 文件  
在 Android.mk 里面敲入    

 

    LOCAL_PATH := $(call my-dir)
    
    include $(CLEAR_VARS)
    
    LOCAL_MODULE := game_shared
    
    LOCAL_MODULE_FILENAME := libgame               
    
    LOCAL_WHOLE_STATIC_LIBRARIES := pomelo_static
                
    include $(BUILD_SHARED_LIBRARY)
    
    LOCAL_CFLAGS    := -D__ANDROID__ 
    
    $(call import-module,libpomelo) 


这样子就表示将在 android 中使用 libpomelo 编译而来的 .so 库  

3: 然后在项目目录下面新建一个 pomelo 的文件夹，然后从 github 上把最新的 libpomelo 下载到 刚刚建的 pomelo 文件夹下面  
![enter image description here](http://ww2.sinaimg.cn/large/6a98ae6cgw1e3ymh7vavqj208h0gtq3v.jpg)

4: 然后打开终端（windows 则打开 cygwin）
在项目目录下敲入  
ndk-build NDK_MODULE_PATH=/android项目绝对路径/pomelo/  
即可完成编译  

![enter image description here](http://ww3.sinaimg.cn/large/6a98ae6cgw1e3ymfi9wk8j20lt0e9787.jpg)


5: 如果是要结合cocos2d-x进行开发，那么只需要把 libpomelo 放在 /cocos2dx绝对路径/cocos2dx/platform/third_party/android/prebuilt 文件夹里面，然后执行 ./build_native.sh 即可  
具体可参考 [cocos2d-x android](https://github.com/cocos2d/cocos2d-x/tree/master/samples/Cpp/TestCpp/proj.android)

使用pomelo做服务端开发时，无论什么客户端，只要能遵循与服务端的线上协议，就能够与服务端建立通信。pomelo内建提供的sioconnector和hybridconnector都定义了自己的协议格式，其中sioconnector用于socket.io的通信，hybridconnector则用来处理websocket和tcp的连接通信。为了方便客户端的开发，pomelo提供了部分平台的客户端SDK，这里主要会介绍一下用于Web端的JavaScript的SDK以及基于C语言的libpomelo的使用。

Web端JavaScript开发库
=======================

对于浏览器来说，HTML5中已经支持了websocket，因此使用支持websocket的浏览器可以直接与服务端的hybridconnector建立通信。而对于比较旧的浏览器来说，还没有支持websocket的，可以使用基于socket.io的方式进行与服务端建立连接。因此，对于Web端，pomelo提供了两套开发库，分别适用于支持websocket的浏览器和不支持websocket的浏览器，这两套开发库的链接如下，适用于socket.io的[pomelo-jsclient-socket.io](https://github.com/pomelonode/pomelo-jsclient-socket.io)以及适用于websocket的[pomelo-jsclient-websocket](https://github.com/pomelonode/pomelo-jsclient-websocket)。

#### socket.io的客户端开发库

  对于使用socket.io的客户端SDK来说，其依赖[socket.io-client](https://github.com/learnboost/socket.io-client/), 由于这个库在使用[component](https://github.com/component/component/)进行管理时有bug，因此在使用的时候，是直接引用其提供的js文件，具体引用的js文件为[socket.io-client.js](https://github.com/LearnBoost/socket.io-client/blob/master/socket.io-client.js)。对于pomelo-jsclient-socket.io来说，同样也是直接使用引用其js文件，也即是[pomelo-client.js](https://github.com/pomelonode/pomelo-jsclient-socket.io/blob/master/lib/pomelo-client.js)。在直接引用这两个文件后即可使用pomelo的调用了。

#### websocket的客户端开发库

对于使用websocket的客户端SDK来说，使用了[component](https://github.com/component/component/)进行管理，因此只需要配置一个component.json文件，里面配置相应的依赖，然后运行

    $ component install
    $ component build

component会自动寻找依赖，完成客户端js的打包。用户只需要引用编译后的build.js即可，然后就可以使用pomelo的调用了。关于component的使用，请参考component的wiki。我们的例子[chatofpomelo-websocket](https://github.com/NetEase/chatofpomelo-websocket/tree/master/web-server/public/js/lib)，这里就是使用了component来管理前端js的，可以作为用户使用的一个参考。

<a name="clientAPI"/>
#### web端API简介

无论是socket.io的还是websocket的，都提供了统一的API，下面对这些API进行简单的介绍。

* pomelo.init(params, cb)

这是往往是客户端的第一次调用，params中应该指出要连接的服务器的ip和端口号，cb会在连接成功后进行回调;

* pomelo.request(route, msg, cb)

请求服务，route为服务端的路由，格式为"<ServerType>.<HandlerName>.<MethodName>", msg为请求的内容，cb会响应回来后的回调;

* pomelo.notify(route, msg)

发送notify，不需要服务器回响应的，因此没有对响应的回调，其他参数含义同request;

* pomelo.on(route, cb)

这个是从EventEmmiter继承过来的方法，用来对服务端的推送作出响应的。route会用户自定义的，格式一般为"onXXX";

* pomelo.disconnect()

这个是pomelo主动断开连接的方法。

libpomelo
===============

libpomelo 是 [pomelo](https://github.com/NetEase/pomelo) 的 c 客户端，支持pomelo 0.3版本以后的协议  

### 依赖
* [libuv](https://github.com/joyent/libuv) 跨平台开发库，主要使用了网络I/O和线程  
* [jansson](https://github.com/akheron/jansson) c 的 json 解析库  

### 使用
#### 创建客户端实例
```
// create a client instance.
pc_client_t *client = pc_client_new();
```

#### 添加事件监听
```
// add some event callback.
pc_add_listener(client, "onHey", on_hey);
pc_add_listener(client, PC_EVENT_DISCONNECT, on_close);
```

#### 监听器的定义
```
// disconnect event callback.
void on_close(pc_client_t *client, const char *event, void *data) {
  printf("client closed: %d.\n", client->state);
}
```

#### 连接到服务器
```
struct sockaddr_in address;

memset(&address, 0, sizeof(struct sockaddr_in));
address.sin_family = AF_INET;
address.sin_port = htons(port);
address.sin_addr.s_addr = inet_addr(ip);

// try to connect to server.
if(pc_client_connect(client, &address)) {
  printf("fail to connect server.\n");
  pc_client_destroy(client);
  return 1;
}
```

#### 发起一个 notify 请求
```
// notified callback
void on_notified(pc_notify_t *req, int status) {
  if(status == -1) {
    printf("Fail to send notify to server.\n");
  } else {
    printf("Notify finished.\n");
  }

  // release resources
  json_t *msg = req->msg;
  json_decref(msg);
  pc_notify_destroy(req);
}

// send a notify
void do_notify(pc_client_t *client) {
  // compose notify.
  const char *route = "connector.helloHandler.hello";
  json_t *msg = json_object();
  json_t *json_str = json_string("hello");
  json_object_set(msg, "msg", json_str);
  // decref json string
  json_decref(json_str);

  pc_notify_t *notify = pc_notify_new();
  pc_notify(client, notify, route, msg, on_notified);
}
```

#### 发起一个 requst 请求
```
// request callback
void on_request_cb(pc_request_t *req, int status, json_t *resp) {
  if(status == -1) {
    printf("Fail to send request to server.\n");
  } else if(status == 0) {
    char *json_str = json_dumps(resp, 0);
    if(json_str != NULL) {
      printf("server response: %s\n", json_str);
      free(json_str);
    }
  }

  // release relative resource with pc_request_t
  json_t *msg = req->msg;
  pc_client_t *client = req->client;
  json_decref(msg);
  pc_request_destroy(req);

  // stop client
  pc_client_stop(client);
}

// send a request
void do_request(pc_client_t *client) {
  // compose request
  const char *route = "connector.helloHandler.hi";
  json_t *msg = json_object();
  json_t *str = json_string("hi~");
  json_object_set(msg, "msg", str);
  // decref for json object
  json_decref(str);

  pc_request_t *request = pc_request_new();
  pc_request(client, request, route, msg, on_request_cb);
}
```

### API 接口  
* 创建一个新的pomelo client实例  
```
pc_client_t *pc_client_new();
```

* 停止客户端的连接  
该接口适合于在libuv子线程中调用，然后在主线程中，通过 pc_client_join来wait子线程退出  
```
void pc_client_stop(pc_client_t *client);
```

* 销毁客户端的连接  
```
void pc_client_destroy(pc_client_t *client);
```

* 主线程中调用等待子线程的退出  
```
int pc_client_join(pc_client_t *client);
```

* 创建一个request请求实例  
```
pc_request_t *pc_request_new();
```

* 销毁一个request请求实例  
```
void pc_request_destroy(pc_request_t *req);
```

* 连接到服务器，在连接过程中会创建子线程用于处理网络I/O  
```
int pc_client_connect(pc_client_t *client, struct sockaddr_in *addr);
```

* 销毁pc_connect_t类型的实例  
```
void pc_connect_req_destroy(pc_connect_t *conn_req);
```

* 发起一个request请求  
```
int pc_request(pc_client_t *client, pc_request_t *req, const char *route,
               json_t *msg, pc_request_cb cb);
```

* 创建一个notify请求实例  
```
pc_notify_t *pc_notify_new();
```

* 销毁一个notify请求实例  
```
void pc_notify_destroy(pc_notify_t *req);
```

* 发起一个notify请求  
```
int pc_notify(pc_client_t *client, pc_notify_t *req, const char *route,
              json_t *msg, pc_notify_cb cb);
```

* 添加一个事件监听  
```
int pc_add_listener(pc_client_t *client, const char *event,
                    pc_event_cb event_cb);
```

* 删除一个事件监听  
```
void pc_remove_listener(pc_client_t *client, const char *event,
                    pc_event_cb event_cb);
```

* 触发一个事件监听  
```
void pc_emit_event(pc_client_t *client, const char *event, void *data);
```

### 编译
#### 前提条件
下载 [gyp](http://code.google.com/p/gyp/source/checkout)  
gyp 其实是一个python写的脚本，并不需要安装，只需要下载下来，可以执行gyp里面的脚本就行  

#### Mac 环境
```
./pomelo_gyp
xcodebuild -project pomelo.xcodeproj
```

#### IOS 环境
```
./pomelo_gyp -DTO=ios
./build_ios
```

#### IOS 模拟器
```
./pomelo_gyp -DTO=ios
./build_iossim
```

#### Linux 环境
```
./pomelo_gyp
make
```

#### Windows 环境
在libpomelo项目跟目录下  
打开[git bash](https://help.github.com/articles/set-up-git#platform-windows)，敲入  
```
mkdir -p build
git clone https://github.com/martine/gyp.git build/gyp
```
之后，打开windows cmd命令行窗口，并且cd切换目录到libpomelo跟目录下面，敲入    
```
build\gyp\gyp.bat --depth=. pomelo.gyp -Dlibrary=static_library -DTO=pc 
```
之后就会生成pomelo.sln，使用visual studio打开即可进行编译  


#### Android 环境
开发前提条件：   
windows:   
* 安装 [Cygwin](http://www.cygwin.com/) with make (select make package from the list during the install).    
* android adt eclipse 这个只要下载最新的 android sdk 里面就有一个配置好环境的 eclipse    

环境搭建：    
1: 新建一个 android 工程，比如新建一个 test 的 工程，建完之后如图：  
![test工程](http://ww3.sinaimg.cn/large/6a98ae6cgw1e3ym2kkdofj207x0f0q3t.jpg)


2: 然后在项目根目录下面，新建一个 jni 文件夹  
然后里面添加一个 Android.mk 文件  
在 Android.mk 里面敲入    

 

    LOCAL_PATH := $(call my-dir)
    
    include $(CLEAR_VARS)
    
    LOCAL_MODULE := game_shared
    
    LOCAL_MODULE_FILENAME := libgame               
    
    LOCAL_WHOLE_STATIC_LIBRARIES := pomelo_static
                
    include $(BUILD_SHARED_LIBRARY)
    
    LOCAL_CFLAGS    := -D__ANDROID__ 
    
    $(call import-module,libpomelo) 


这样子就表示将在 android 中使用 libpomelo 编译而来的 .so 库  

3: 然后在项目目录下面新建一个 pomelo 的文件夹，然后从 github 上把最新的 libpomelo 下载到 刚刚建的 pomelo 文件夹下面  
![enter image description here](http://ww2.sinaimg.cn/large/6a98ae6cgw1e3ymh7vavqj208h0gtq3v.jpg)

4: 然后打开终端（windows 则打开 cygwin）
在项目目录下敲入  
ndk-build NDK_MODULE_PATH=/android项目绝对路径/pomelo/  
即可完成编译  

![enter image description here](http://ww3.sinaimg.cn/large/6a98ae6cgw1e3ymfi9wk8j20lt0e9787.jpg)


5: 如果是要结合cocos2d-x进行开发，那么只需要把 libpomelo 放在 /cocos2dx绝对路径/cocos2dx/platform/third_party/android/prebuilt 文件夹里面，然后执行 ./build_native.sh 即可  
具体可参考 [cocos2d-x android](https://github.com/cocos2d/cocos2d-x/tree/master/samples/Cpp/TestCpp/proj.android)

# Pomelo-性能测试(以LordOfPomelo为测试对象)


### 目 录
##### 测试环境
1. 服务端测试环境
2. 客户端测试环境


##### 测试结果
1. 多进程多角色同时战斗场景(最多486个角色)
2. 多进程多角色同时行走场景(最多800个角色)
3. 多进程多角色同时战斗/行走场景(最多558个角色)


### 测试环境
##### 1.1 服务端测试环境
<table class="table table-bordered table-striped table-condensed">
  <th width="15%">服务</th>
  <th width="30%">机器</th>
  <th width="55%">硬件配置</th>
  <tr>
    <td>GameServer<br>
      &<br>
      WebServer
    </td>
    <td>pomelo3.server.163.org</td>
    <td>
      云主机<br>
      1CPU 8核心<br>
      CPU型号 GenuineIntel QEMU Virtual CPU version 1.1.2@2.0GHz<br>
      16G 内存<br>
      1网卡<br>
      linux/64位 OS<br>
    </td>
  </tr>
</table>

###### 说明:
* 服务端采用Node.js开发, 磁盘IO主要为log写入, 所有game-server服务器均配置toobusy(MAXLAG为默认的70ms), 出现瓶颈的部分在CPU.

##### 1.2 客户端测试环境

<table class="table table-bordered table-striped table-condensed">
  <th width="15%">服务</th>
  <th width="30%">机器</th>
  <th width="55%">硬件配置</th>
  <tr>
    <td>Clients</td>
    <td>pomelo16~25.server.163.org</td>
    <td>
      云主机<br>
      1CPU 1核心<br>
      CPU型号 GenuineIntel Westmere E56xx/L56xx/X56xx (Nehalem-C)@2.6GHz<br>
      1G 内存<br>
      1网卡<br>
      linux/64位 OS<br>
    </td>
  </tr>
</table>
###### 说明:
* 客户端是全部走内网的。


### 测试结果

##### 1. 多进程多角色同时战斗场景(最多486个角色同时处于area3场景)
* 9台云主机上各启动1个客户端进程, 每个客户端进程上运行1个代理, 每个代理负责55个角色, 这样会有495个角色登录游戏. 9个客户端代理并发, 每2秒发起一次角色登录操作, 最终会有486个角色同时处于area3场景, 登录成功的角色每隔2~5秒发起一次攻击(攻击对象为附近的其他角色或者怪物)或者捡道具操作. 攻击的成功率为98.29%. 如下图:

![attack-1](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/attackJpg/1.jpg)
![attack-2](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/attackJpg/2.jpg)


* 每个角色的出生点随机分布于15个点上, 如下图:

![attack-3](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/attackJpg/3.jpg)
![attack-4](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/attackJpg/4.jpg)

* 486个角色都登录成功并开始发起攻击时, 服务器和pomelo16客户端的top:

![attack-5](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/attackJpg/5.jpg)

* 测试完毕时服务器和pomelo16客户端的top:


![attack-6](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/attackJpg/6.jpg)

* 测试过程中服务器状态:

![attack-7](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/attackJpg/7.jpg)
![attack-8](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/attackJpg/8.jpg)
![attack-9](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/attackJpg/9.jpg)
![attack-10](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/attackJpg/10.jpg)

* 9台云主机上各启动1个客户端进程, 每个客户端进程上运行1个代理, 每个代理负责90个角色, 这样会有810个角色登录游戏. 9个客户端代理并发, 每2秒发起一次角色登录操作, 最终会有800个角色同时处于area3场景, 登录成功的角色每隔2~5秒发起一次移动操作. 移动的成功率为99.95%. 如下图:

![move-1](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/moveJpg/1.jpg)
![move-2](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/moveJpg/2.jpg)

* 这800个角色随机出生于地图上的15个点. 每一个角色的移动操作都是有规律的, 8次移动为一轮动作循环, 每次的步长为随机值(1~walkSpeed), 8次移动后该角色大致可以回到起点. 这么做的目的是尽量将角色限定在其出生点附近, 以使得所有角色尽量均匀分布于整张地图. 如下图:

![move-3](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/moveJpg/3.jpg)
![move-4](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/moveJpg/4.jpg)

* 800个角色都登录成功并开始移动时, 服务器和pomelo16客户端的top:

![move-5](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/moveJpg/5.jpg)

* 测试完毕时服务器和pomelo16客户端的top:

![move-6](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/moveJpg/6.jpg)

* 测试过程中服务器状态:

![move-7](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/moveJpg/7.jpg)
![move-8](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/moveJpg/8.jpg)
![move-9](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/moveJpg/9.jpg)
![move-10](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/moveJpg/10.jpg)

##### 3. 多进程多角色同时战斗/行走场景(最多558个角色)
* 9台云主机上各启动1个客户端进程, 每个客户端进程上运行1个代理, 每个代理负责63个角色, 这样会有567个角色登录游戏. 9个客户端代理并发, 每2秒发起一次角色登录操作, 最终会有558个角色同时处于area3场景, 登录成功的角色每隔2~5秒发起一次攻击(50%)或者移动(50%)操作. 攻击的成功率为99.50%. 移动的成功率为99.57%.  如下图:

![both-1](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/bothJpg/1.jpg)
![both-2](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/bothJpg/2.jpg)
![both-3](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/bothJpg/3.jpg)

* 这558个角色随机出生于地图上的15个点. 角色攻击时的对象为附近的其他角色或者怪物. 角色的移动操作都是有规律的, 8次移动为一轮动作循环, 每次的步长为随机值(1~walkSpeed), 8次移动后该角色大致可以回到起点. 这么做的目的是尽量将角色限定在其出生点附近, 以使得所有角色尽量均匀分布于整张地图. 如下图:

![both-4](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/bothJpg/4.jpg)
![both-3](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/bothJpg/5.jpg)

* 558个角色都登录成功并开始攻击/移动时, 服务器和pomelo16客户端的top:

![both-5](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/bothJpg/6.jpg)

* 测试完毕时服务器和pomelo16客户端的top:

![both-7](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/bothJpg/7.jpg)

* 测试过程中服务器状态:

![both-8](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/bothJpg/8.jpg)
![both-9](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/bothJpg/9.jpg)
![both-10](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/bothJpg/10.jpg)
![both-11](http://pomelo.netease.com/resource/documentImage/lordofpomelo/performanceTest/bothJpg/11.jpg)


日志管理
===========

pomelo 日志是通过 [pomelo-logger](https://github.com/NetEase/pomelo-logger) 模块来管理的，[pomelo-logger](https://github.com/NetEase/pomelo-logger) 是对 [log4js](https://github.com/nomiddlename/log4js-node) 的简单封装，并提供了一些非常有用的 feature。

日志是通过 category 来进行管理与维护的，可以在log4js.json文件中进行配置  
```json
{
  "appenders": [
    {
      "type": "console"
    },
    {
      "type": "file",
      "filename": "./logs/con-log-${opts:serverId}.log",
      "pattern": "connector",
      "maxLogSize": 1048576,
      "layout": {
        "type": "basic"
      },
      "backups": 5,
      "category": "con-log"
    },
    {
      "type": "file",
      "filename": "./logs/rpc-log-${opts:serverId}.log",
      "maxLogSize": 1048576,
      "layout": {
        "type": "basic"
      },
      "backups": 5,
      "category": "rpc-log"
    },
    {
      "type": "file",
      "filename": "./logs/forward-log-${opts:serverId}.log",
      "maxLogSize": 1048576,
      "layout": {
        "type": "basic"
      },
      "backups": 5,
      "category": "forward-log"
    },
    {
     "type": "file",
     "filename": "./logs/rpc-debug-${opts:serverId}.log",
     "maxLogSize": 1048576,
     "layout": {
      "type": "basic"
     },
     "backups": 5,
     "category": "rpc-debug"
    },
    {
      "type": "file",
      "filename": "./logs/crash.log",
      "maxLogSize": 1048576,
      "layout": {
        "type": "basic"
      },
      "backups": 5,
      "category":"crash-log"
    },
    {
      "type": "file",
      "filename": "./logs/admin.log",
      "maxLogSize": 1048576,
      "layout": {
          "type": "basic"
        }
      ,"backups": 5,
      "category":"admin-log"
    },
    {
      "type": "file",
      "filename": "./logs/pomelo.log",
      "maxLogSize": 1048576,
      "layout": {
          "type": "basic"
        }
      ,"backups": 5,
      "category":"pomelo"
    }
  ],

  "levels": {
    "rpc-log" : "ERROR",
    "forward-log": "ERROR"
  },

  "replaceConsole": true,
  "lineDebug": false
}

```

从配置文件中可以看出，每一项（除了console项）都配了category，pomelo-logger 通过 getLogger 的第一个参数指定 category 来把该logger输出的日志定向到该category配置的文件或者其它输出方案。  
你可以添加自己的category，并在getLogger指定该category，你就可以把日志定向到该category所配的输出方案  
**注意**：不建议使用不指定category的方式来进行配置，这样子所有的logger都会定向到该全局的输出方案  

### 日志category  
在pomelo中有些指定的category用于输出日志：  
* pomelo： 输出 pomelo 框架里的日志  
* admin-log： 输出 pomelo-admin 用于监控client登陆master时输出的日志  
* crash-log： 输出服务器crash异常时的日志信息  
* rpc-debug： 输出 rpc-debug 的日志，需要开启 [rpc-debug 模式](https://github.com/NetEase/pomelo/wiki/pomelo-0.6%E7%89%88%E6%96%B0%E7%89%B9%E6%80%A7#rpc-debug%E6%97%A5%E5%BF%97)  
* forward-log : 输出从前端服务器转发到后端服务器的请求日志  
* rpc-log: 输出 rpc filter 上的日志  
* con-log: 输出 handler filter 上的日志  

### 日志levels
可以通过指定日志的levels来控制输出的日志  
```javascript
"levels": {
    "rpc-log" : "ERROR",
    "forward-log": "ERROR"
}
```

日志等级从左到右依次提升：  
```
TRACE, DEBUG, INFO, WARN, ERROR, FATAL
```

在levels上等级配的越低，输出的日志范围则越大  
相反，则输出的日志范围越小  
比如：
```javascript
var rpc_logger = require('pomelo-logger').getLogger('rpc-log', __filename);
rpc_logger.info("msg");
```

这里rpc_logger的输出日志等级是 INFO，而 levels 上配的是 ERROR  
那么该日志就不会被输出到对应的appenders上面  
你需要levels改成低于 INFO 的级别，比如 DEBUG 才会把 rpc_logger 的日志输出  

### 日志配置项说明
* type： 指定appenders的类型，可以是console， dataFile， file 等，具体详见 [log4js](https://github.com/nomiddlename/log4js-node/wiki/Appenders)
* filename： 指定输出文件的路径
* pattern：指定输出日志的pattern
* maxLogSize：指定输出日志的最大大小
* layout：指定输出的layout样式
* backups：指定最大输出的文件数目
* category：指定该appender对应的category，如果没有该项，说明该appender是一个全局的appender
* replaceConsole：指定是否替换默认的console
* lineDebug：指定是否开启debug显示日志行数

概述
==========

命令行工具pomelo是Pomelo框架提供的一个小工具，该工具能够帮助开发者更便捷、更有效率地进行应用开发。该工具包括的命令支持绝大多数的应用开发操作，包括创建初始项目、启动应用、停止应用、关闭应用等。用户可以通过pomelo --help命令查询相关命令及其使用说明。

命令行安装
===========

当使用如下命令安装Pomelo的时候，pomelo会自动安装在相应的bin目录下:

    $ npm install pomelo -g


命令介绍
=========

目前pomelo支持如下命令及选项:

* init: 创建一个新项目，该项目中包含创建pomelo应用的基本文件及pomelo应用的简单示例。
* start: 启动应用及服务器。
* list: 列出当前应用开启的所有服务器的信息，包括服务器Id、服务器类型、pid、堆使用情况、启动时长。
* stop: 关闭应用及服务器或者停止指定的服务器。
* kill: 强制关闭应用及服务器。
* add: 运行时动态添加服务器。
* masterha: 当启用masterha高可用的时候，用来启动master服务器的slave节点。
* --version：列出当前使用pomelo的版本信息。
* --help：列出所有pomelo支持的命令及使用说明。


## 命令使用说明

* init 

根据给出的路径或文件名创建新项目，支持相对路径和绝对路径。默认情况下为当前路径，项目名称为当前文件夹名称,命令如下：

    pomelo init [dirname]

在创建新项目时，需要选择新项目使用的与客户端通信时使用的connector,1 代表 Websocket(native socket), 2 代表socket.io。当当前目录下有同名文件夹存在时，会提示是否覆盖，还是取消创建。

* start

该命令用来启动Pomelo应用，命令格式如下:

    pomelo start [-e,--env <env>] [-d,--directory <code directory>]
                 [-D,--daemon]

其中，-e 用来选择启动时使用的env，如production，development，stress-test等; -d 用来指定项目目录； -D 用来开启daemon模式启动，如果开启了daemon，那么进程将转入后台运行, 所有的日志将不再打印到console上，只能通过对应的日志文件查看日志。在0.7及以前的版本中，对于env的使用，没有使用-e选项，而是直接作为一个参数来使用的，这里需要注意一下。

用户可以在<project_dir>/game-server/config/servers.json中为不同的服务器中添加不同参数，这些参数是node和v8支持的参数，是用来指定和影响node及v8的行为的。例如，当我们想对某一个服务器开启调试的时候，就可以在服务器配置中，增加args配置项，并在args中配置开启调试的端口等，示例如下:

```json
{"connector":[{"id":"connector-server-1", "host":"127.0.0.1", "port":4050, 
"clientPort":3050, "args":"--debug=[port]"}]}
```

* list

当应用启动后，该命令列出所有服务器信息。由于当执行此操作时，pomelo是作为监控管理框架的一个客户端的，在连接注册到master上的时候，需要进行身份验证。默认生成的项目中，有一个默认的用户名admin，口令也为admin，因此在不指定用户名和口令的时候，默认使用的用户名和口令均为admin，下面的stop命令和kill命令均需要使用用户名和口令验证，默认值与此处相同。应用的管理用户可以通过修改config/adminUser.json文件进行配置,具体的配置格式可以参考pomelo init生成的项目中的相关配置。

执行本命令时，还需要指定master服务器的ip和port, 这样可以是的pomelo list可以在任意地方执行。pomelo stop/kill/add等也同样需要指定master服务器的ip和port，默认使用127.0.0.1:3005作为master服务器的地址。

命令格式如下: 

     pomelo list [-u,--username <username>] [-p,--password <password>]
                 [-h,--host <master-host>] [-P,--port <master-port>]

* stop 

stop用来停止当前应用，优雅地关闭应用。和kill命令不同，这种关闭首先会切断客户端与服务器的连接，然后逐一关闭所有服务器。如果指定了服务器serverId的话，则会关闭特定的服务器，而不是关闭所有的服务器。与list命令一样，需要权限验证，默认的用户名和密码均为admin,也需要指定master服务器的位置, 跟pomelo list一样，默认使用127.0.0.1:3005。

命令格式如下:
    
     pomelo stop [-u,--username <username>] [-p,--password <password>]
                 [-h,--host <master-host>] [-P,--port <master-port>]
                 [<serverIds>...]

* kill 

该命令强制关闭应用。在本地进行应用开发过程中，如果遇到kill之后还有服务器进程没有关闭的情况，可以增加--force选项，强制关闭所有服务器进程。该操作相当地暴力，可能产生数据丢失等不好的影响，可以在开发调试时使用，不推荐在线上使用该命令。该命令同样也需要进行身份验证以及指定master服务器的位置，具体方式同list和stop。

该命令需在项目的根目录或game-server下使用，命令格式如下:

     pomelo kill [-u,--username <username>] [-p,--password <password>]
                 [-h,--host <master-host>] [-P,--port <master-port>]
                 [-f,--force]

* add

该命令用来运行时动态增加服务器，与pomelo list等命令类似，pomelo add也需要身份验证以及指定master服务器的地址。具体命令格式如下:

     pomelo add [-u,--username <username>] [-p,--password <password>]
                [-h,--host <master-host>] [-P,--port <master-port>]
                [<server-args>...]

args参数是用来指定新增服务器的参数的，包括服务器类型，服务器id等， 支持一次增加一台或多台同类型的服务器，例子如下：

     pomelo add host=127.0.0.1 port=8000++ clientPort=9000++ frontend=true clusterCount=3 serverType=connector 
     pomelo add host=127.0.0.1 port=8000 clientPort=9000 frontend=true serverType=connector id=added-connector-server

* masterha

当启用了master服务器的高可用后，该命令用来启动master服务器的slave节点，需要在game-server/config目录下配置masterha.json。其他的命令行参数类似于pomelo start，格式如下：

    pomelo masterha [-d,--direcotry <code directory>]

* 其他

查看当前Pomelo的版本时，可以使用如下命令:
    
    pomelo --version

查看pomelo命令行工具的帮助时，可以使用如下命令:

    pomelo --help
    pomelo add --help
    pomelo start --help

* 注:

一般来说在开发环境中，master服务器的地址会一直是127.0.0.1:3005,使用的管理用户的username和password直接使用默认的admin即可，这样的话，开发调试时，在执行具体的pomelo命令的时候，maser服务器的地址信息以及管理用户信息都可以省略。

#pomelo-robot
pomelo-robot 是一个用来对pomelo游戏服务器框架进行性能测试的工具, 也可以测试其他基于socket.io服务的性能. 
该模块可以采用单机或者分布式测试两种模式. 

#功能
对游戏项目进行自动化的性能测试和分析, 为游戏服务器提供机器人及其运行脚本, 最终输出性能测试分析报告. 
pomelo-robot 模块通过沙箱的方式执行用户自定义的JS脚本. 运行过程中各客户端会自动把数据汇报给主节点, 主节点把所有节点的测试数据进行提炼汇总, 计算出平均响应时间等统计数据, 然后定时发给内置的HTTP服务器进行界面展示. 

#模块结构
模块内部运行结构如下：

![](https://raw.github.com/palmtoy/ImageBucket/master/Pomelo/Robot/1.jpg)

"Master"负责收集所有"Client"的运行数据并展示统计结果. <br/>
"Client"负责在多个沙箱("User")中运行自定义脚本, 同时向"Master"汇报运行数据. 

##使用示例
创建Node.js测试工程, 工程目录结构如下图所示:<br/>

![](https://raw.github.com/palmtoy/ImageBucket/master/Pomelo/Robot/2.jpg)

安装依赖库:<br/>
``` javascript
npm install pomelo-robot
```

###config.json配置
"config.json"分为两种运行环境: 开发(dev)或生产(prod)环境, "prod"环境的文件内容如下：
``` javascript
{
  "master": {"host": "127.0.0.1", "port":8888, "webport":8889, "interval":500}
}
```
"master"：主服务器的IP, 与客户端的通讯端口, WEB界面端口, 间隔多少毫秒运行一个自定义JS脚本(如:lord.js). <br/>

###实现自定义脚本配置
#####在"env.json"中配置自定义脚本路径:<br/>
``` javascript
{
  "env": "prod",
  "script": "/app/script/lord.js"
}
```

#####实现自定义脚本"lord.js": 
``` javascript
// ...
var queryHero = require(cwd + '/app/data/mysql').queryHero;
// ...
function entry(host, port, token, callback) {
  // ...
  // 初始化socketClient
  pomelo.init({host: host, port: port, log: true}, function() {
    pomelo.request('connector.entryHandler.entry', {token: token}, function(data) {
	  // ...
      afterLogin(pomelo,data);
    });
  });
}
// ...
```

"/app/data/mysql.js"中查找登录角色的代码如下：
``` javascript
// ...
queryHero = function(client,limit,offset,cb){
    var users = [];
    var sql = "SELECT User.* FROM User,Player where User.id = Player.userId and User.name like 'pomelo%' limit ? offset ? ";
	// ...
};
// ...
``` 

上面的代码运行在沙箱中: 首先登录游戏服务器, 登录成功后回调"afterLogin"函数, 用户可以进行后续的相关操作. <br/>

###启动入口文件app.js
"app.js"会根据启动参数判断是启动"master"服务还是"client"服务. <br/>
``` javascript
var envConfig = require('./app/config/env.json');
var config = require('./app/config/' + envConfig.env + '/config');
//...
if (mode === 'master') {
    robot.runMaster(__filename);
} else {
    var script = (process.cwd() + envConfig.script);
    robot.runAgent(script);
}
// ...
``` 
具体代码可参考[工程](https://github.com/NetEase/pomelo-robot-demo). <br/>

###运行测试
运行如下命令, 启动"master"服务: <br/>
"node app.js master" <br/>
打开浏览器访问地址"http://masterIp:8889" <br/>

运行如下命令, 启动"client"服务: <br/>
"node app.js client" <br/>
注: 可以在多台机器上启动"client"服务进行性能和压力测试.

WEB界面会显示连接到"master"的"client"数量, 可以在"Per Agent Users"一栏中配置每个"client"将要运行的沙箱数量, 点击"Go"按钮通知所有的"client"开始运行. WEB界面会定时获取后台数据进行展示. <br/>
运行界面如下图所示：<br/>

![](https://raw.github.com/palmtoy/ImageBucket/master/Pomelo/Robot/3.jpg) 

![](https://raw.github.com/palmtoy/ImageBucket/master/Pomelo/Robot/4.jpg) 

###其他
源代码请参考[工程](https://github.com/NetEase/pomelo-robot) 
## 概述
pomelo-sync模块用于解决游戏进程中需要持久化的数据在内存和存储系统之间的同步问题. 该模块为上述的数据同步需求提供了一种异步的实现方式, 并可以根据用户配置, 定时的将数据同步到持久层(如MySQL, Redis, 磁盘文件等). 

## 应用场景
在游戏进程中, 需要进行大量的数据更新与同步(如角色的位置坐标, 血量, 装备属性等). 如果频繁的操作数据持久层, IO操作的开销就会很大. 采用定时批量的方式同步变动的数据是避免IO开销太大的一种方法, pomelo-sync就是按照这个思路设计和实现的. pomelo-sync的配置与iBATIS类似, 不同的一点是ORM完全由用户配置控制, 具有很大的灵活性, 因此, pomelo-sync可以应用于各种不同的数据库中(如MongoDB等). 

## 模块结构
pomelo-sync模块内部结构如下：

![](http://pomelo.netease.com/resource/documentImage/pomelo-sync.png) 

Logic Interface：提供侵入式的数据更新调用接口, 包括常规的add、update、delete和立即执行持久化的接口flush <br/>

Invoke Interface：提供持久化的实际调用执行接口 <br/>
Queue：保存本周期内需要持久化的对象, 可支持多节点转发数据<br/>
Timer：可支持静态配置和动态修改同步时间间隔<br/>
Mapping：支持在持久化时自定义同步方法映射<br/>

Store Interface：封装了各种存储引擎的持久化接口 <br/>
Log：提供对数据变动时的AOF日志记录 <br/>
Mysql, Redis, File：根据用户传入的对象执行用户自定义的同步方法 <br/>

## 安装
npm install pomelo-sync-plugin <br/>
注: 目前pomelo-sync模块被封装在了[pomelo-sync-plugin](https://github.com/NetEase/pomelo-sync-plugin)插件中.

## 使用示例
### 使用pomelo-sync-plugin
``` javascript
// app.js
var sync = require('pomelo-sync-plugin');
// ...
// Configure database
app.configure('production|development', 'area|auth|connector|master', function() {
  var dbclient = require('./app/dao/mysql/mysql').init(app);
  app.set('dbclient', dbclient);
  app.use(sync, {sync: {path:__dirname + '/app/dao/mapping', dbclient: dbclient}});
});
// ...
```
注: "/app/dao/mapping"路径下的所有js文件都会被加载进入pomelo-sync中, 这些模块中定义了定时同步时所执行的所有面向持久层的操作. 加载模块的代码如下所示:
``` javascript
// pomelo-sync-plugin/node_modules/pomelo-sync/lib/dbsync.js
var DataSync = module.exports = function(options) {
  // ...
  this.mapping = this.loadMapping(options.mappingPath);
  // ...
};
```

### 配置同步对象映射关系
该模块支持用户自定义同步方法, 如：
``` javascript
// game-server/app/dao/mapping/taskSync.js
module.exports = {
  updateTask: function(dbclient, val, cb) {
    var sql = 'update Task set taskState = ?, startTime = ?, taskData = ? where id = ?';
    // ...
    var args = [val.taskState, val.startTime, taskData, val.id];
    dbclient.query(sql, args, function(err, res) {
    // ...
    });
  }
};
```

### 创建sync对象
``` javascript
// pomelo-sync-plugin/lib/components/sync.js
var DataSync = require('pomelo-sync');
// ...
var createSync = function(opts){
  var opt = opts || {};
  opt.mappingPath = opts.path;
  opt.client = opts.dbclient;
  opt.interval = opts.interval || 60 * 1000;
  return new DataSync(opt);
};
```

## API
### sync.exec(key,id,val,cb)
添加异步定时执行的操作
#### Arguments
+ key -  方法映射的关键词, 使用时需要唯一. 
+ id  -  实体对象主键. 
+ val -  需要同步对象, 添加后会克隆此对象. 
+ cb  -  同步完成后的异步回调, 可以为空. 

具体使用示例:
``` javascript
// app/dao/taskDao.js
// ...
task.on('save', function() {
  app.get('sync').exec('taskSync.updateTask', task.id, task);
});
// ...
```

### sync.flush(key,id,val,cb)
立即同步某个对象到持久层
#### Arguments
+ key -  方法映射的关键词, 使用时需要唯一. 
+ id  -  实体对象主键. 
+ val -  需要同步对象. 
+ cb  -  同步完成后的异步回调, 可以为空. 

### sync.isDone()
检查内存中是否还有需要同步到持久层的数据对象, 一般配合"sync()"方法使用.

### sync.sync()
无视定时器, 立即执行同步过程. 一般用在服务器关闭时调用. 代码如下：
``` javascript
// pomelo-sync-plugin/lib/components/sync.js
Component.prototype.stop = function(force, cb) {
  // ...
  this.state = STATE_STOPED;
  this.sync.sync();
  var self = this;
  var interval = setInterval(function(){
    if (self.sync.isDone()) {
      clearInterval(interval);
      cb();
    }
  }, 200);
};
``` 

## 其他参数选项
该模块默认的同步时间间隔为"1000 * 60"(即1分钟), 如需修改, 使用"opt.interval"传入即可. <br/>
该模块默认关闭"AOF"日志记录, 如需打开, 使用"opts.aof=ture"打开. 

## 注意
如需支持事务操作则应依赖于持久层内置事务模型来保证.

## 其他
更详细的示例, 请参考该模块[源代码](https://github.com/NetEase/pomelo-sync)与[游戏Demo](https://github.com/NetEase/lordofpomelo). 

#Treasures介绍
##描述
[Treasures](https://github.com/NetEase/treasures) 游戏是从 [LordOfPomelo](https://github.com/NetEase/lordofpomelo) 中抽取出来的, 去掉了大量的游戏逻辑, 用以更好的展示 [Pomelo](https://github.com/NetEase/pomelo) 框架的用法以及运作机制. 

Treasures 很简单, 输入一个用户名后, 会随机得到一个游戏角色并进入游戏场景. 在游戏场景中地上会散落一些宝物, 每个宝物都有分数, 玩家操作游戏角色去捡起地上的宝物, 然后得到相应的分数. 

##安装和运行
安装 `pomelo`

```bash
npm install -g pomelo
```
获取源码
```bash
git clone https://github.com/NetEase/treasures.git
```
安装 `npm` 依赖包（先进入项目目录）
```bash
sh npm-install.sh
```
启动 `web-server`  (先进入`web-server`目录)
```bash
node app.js
```
启动 `game-server` (先进入`game-server`目录)
```bash
pomelo start
```
在浏览器中访问 [http://localhost:3001](http://localhost:3001) 进入游戏.

如有问题, 可以参照 [pomelo快速使用指南](https://github.com/NetEase/pomelo/wiki/pomelo%E5%BF%AB%E9%80%9F%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8D%97)

也可以参照 [tutorial1 分布式聊天](https://github.com/NetEase/pomelo/wiki/tutorial1--%E5%88%86%E5%B8%83%E5%BC%8F%E8%81%8A%E5%A4%A9)

##架构
Treasures 分为 web-Server 和 game-Server 两部分. 

* `web-server` 是用 Express 建立的最一个基础的 http 服务器, 用来为浏览器页面的访问提供服务. 

* `game-server` 是 WebSocket 服务器, 用来运行整个游戏的逻辑. 

首先, 通过配置文件来看 `game-server` 的具体架构 `game-server/config/servers.json`
```javascript
{
  "development": {
    "connector": [
      {"id": "connector-server-1", "host": "127.0.0.1", "port": 3150, "clientPort": 3010, "frontend": true},
      {"id": "connector-server-2", "host": "127.0.0.1", "port": 3151, "clientPort": 3011, "frontend": true}
    ],
    "area": [
      {"id": "area-server-1", "host": "127.0.0.1", "port": 3250, "areaId": 1}
    ],
    "gate": [
      {"id": "gate-server-1", "host": "127.0.0.1", "clientPort": 3014, "frontend": true}
    ]
  }
}
```
可以看到, 服务端是由以下几个部分构成：

* 1 个 `gate` 服务器, 主要用于负载均衡, 把来自客户端的连接分散到两个 `connector` 服务器上. 
* 2 个 `connector` 服务器, 主要用于接收和发送消息. 
* 1 个 `area` 服务器, 主要用于驱动游戏场景和游戏逻辑

服务器之间的关系, 如下图所示：

![treasure-arch](http://pomelo.netease.com/resource/documentImage/treasure-arch.png)

##源码分析
#####通过游戏流程来分析代码:

###1. 连接服务器
客户端 `web-server/public/js/main.js` 的 `entry` 方法中:

```javascript
pomelo.request('gate.gateHandler.queryEntry', {uid: name}, function(data) {
  //...
});
```

服务端 `game-server/app/servers/gate/handler/gateHandler.js` 的 `queryEntry`方法中:

```javascript
Handler.prototype.queryEntry = function(msg, session, next) {
  // ...
  // 通过crc算法将玩家输入的用户名字符串转换为整数, 然后对connector服务器个数取余hash到某个connector服务器上.
  // 最后将要连接的 connector 服务器的 host 和 port 返回给客户端.
  next(null, {code: Code.OK, host: res.host, port: res.wsPort});
};
```

这样客户端就能连接到所分配的 `connector` 服务器上了. 

###2. 进入游戏
在与 `connector` 服务器建立连接之后, 就可以进入游戏了:

```javascript
pomelo.request('connector.entryHandler.entry', {name: name}, function(data) {
  // ...
});
```

在客户端第一次向 `connector` 服务器发出请求时, 服务器会将 `session` 信息进行初始化和绑定:

```javascript
session.bind(playerId); // session 与 playerId 绑定
session.set('areaId', 1); // 设置玩家 areaId
```
并将该 `connector` 服务器的序号与一个自增的变量 `id` 组合生成该角色的 `playerId`, 最后将生成的这个 `playerId` 发送给客户端.

客户端向服务端发起进入场景的请求：

```javascript
pomelo.request("area.playerHandler.enterScene", {name: name, playerId: data.playerId}, function(data) {
  // ...
});
```

客户端向服务端发送请求后, 请求先到达 `connector` 服务器, 然后 `connector` 服务器根据pomelo框架的默认转发规则(`pomelo/lib/components/proxy.js`中的`defaultRoute`函数), 将请求路由到相应的 `area` 服务器(本例子中只有一个`area`服务器), `area` 服务器中的 `playerHandler` 再处理相应的请求. 这样玩家就加入到游戏场景中了. 

在一个玩家加入到游戏场景之后, 其他玩家必须能即时的看到这个玩家的加入, 所以服务端必须将消息广播到在此游戏场景中的所有玩家. 
建立 `channel`, 所有加入此游戏场景的玩家都会加入到这个 `channel` 中

```javascript
// game-server/app/models/area.js 的 addEntity 函数中
// 获取 channel, 如果没有就创建一个, 然后将玩家加入 channel
getChannel().add(e.id, e.serverId);
```

当 `area` 中有玩家加入, 或其他事件发生改变时, 这些信息都会被推送到在这个 `channel` 中的每个玩家. 例如有玩家加入时：

```javascript
// game-server/app/models/area.js 的 entityUpdate 函数中
getChannel().pushMessage({route: 'addEntities', entities: added});
// 注: entityUpdate 是由 game-server/app/models/timer.js 中的 tick 函数调用的(详见下面介绍).
```

这些消息都是通过 `connector` 服务器发送到客户端的. `area` 中的消息是通过`session.frontendId` 来决定是由哪个 `connector` 服务器发出去. 

客户端接受消息:
```javascript
// web-server/public/js/msgHandler.js 中的 init 函数:
// 当有新玩家加入时, 服务端会广播消息给所有玩家. 客户端通过这个路由绑定, 来获取消息.
pomelo.on('addEntities', function(data) {
  // ...
});
```

###3. Area 服务器
`area` 服务器是一个由 `tick` 来驱动的游戏场景. 每个tick(100ms)都会对场景中 `entity` 的状态进行更新. 如果 `entities` 的状态发生了改变, 那么新的状态会被推送到所有相关客户端.
```javascript
function tick() {
  //run all the action
  area.actionManager().update();
  // update entities
  area.entityUpdate();
  // update rank
  area.rankUpdate();
}
```

例如玩家发起一个 `move` 动作:

客户端
```javascript
// 向服务端发送 move 请求request:
pomelo.request('area.playerHandler.move', {targetPos: targetPos}, function(result) {...});
```
服务端 `playerHandler` 接受请求：
```javascript
handler.move = function(msg, session, next) {
  // ...
  // 产生一个 move action
  var action = new Move({
    entity: player,
    endPos: endPos
  });
  // ...
  // 并将该 action 加入到 actionManager 中:
  if (area.timer().addAction(action)) { ... });
  // ...
});
```
然后这个 `action` 会在下个 `tick` 中更新. 

###4. 客户端发送和接受消息
客户端和服务端的通讯有以下几种方式：

* Request - Response 方式

```javascript
// 向 connector 发送请求, 参数 {name: name}
pomelo.request('connector.entryHandler.entry', {name: name}, function(data) {
  // 回调函数得到请求的返回结果
  // do something
});
```

* Notify (向服务端发送通知)

```javascript
// 向服务端发送notify通知
pomelo.notify("***.***.***", params);
```

* Push （服务端主动发送消息到客户端）

```javascript
// 当有新玩家加入时, 服务端会广播消息给所有玩家. 客户端通过这个路由绑定, 来获取消息:
pomelo.on('addEntities', function(data) {
  // ...
});
```

###5. 离开游戏

当玩家离开游戏时, `connector` 服务器会先收到断开的消息. 然后需要在 `area` 服务器中将用户剔除, 并广播消息给其他在线玩家.
 
因为服务器之间的进程都是独立的, 所以这就涉及到一个 `RPC` 调用. 好在 Pomelo 框架对 `RPC` 做了很好的封装, 例如:
`area` 服务器想要提供一系列的 `remote` 接口供其他服务器进程调用, 只需要在 `servers/area` 目录下创建一个 `remote` 目录, 在 `remote` 目录下的文件暴露出来的接口, 都可以作为 `RPC` 调用接口. 

例如, 玩家离开:

```javascript
// connector 中对 session 绑定事件, 当 session 关闭时, 触发事件
session.on('closed', onUserLeave.bind(null, self.app));
var onUserLeave = function (app, session, reason) {
  if (session && session.uid) {
    // rpc 调用
    app.rpc.area.playerRemote.playerLeave(session, {playerId: session.get('playerId'), areaId: session.get('areaId')}, null);
  }
};
```

对应的 `area/remote/playerRemote.js` 中 `playerLeave` 方法

```javascript
exp.playerLeave = function(args, cb) {
  // ...
  // 发出通知
  area.getChannel().pushMessage({route: 'onUserLeave', code: consts.MESSAGE.RES, playerId: playerId});
  // ...
};
```
这样就轻松的完成了一个跨进程的调用.


###6. 总结
通过上述对游戏流程相关源代码的分析, 我们对Treasures的代码结构已经有了比较深入的认识. 上述流程也已基本涵盖使用Pomelo框架进行游戏客户端/服务器端开发的相关方法, 如需继续深入了解此方面的内容请参考[LordOfPomelo-介绍](https://github.com/NetEase/pomelo/wiki/LordOfPomelo-%E4%BB%8B%E7%BB%8D).


#LordOfPomelo介绍
[LordOfPomelo](https://github.com/NetEase/lordofpomelo)是一个基于Pomelo框架开发的分布式MMORPG游戏[Demo](http://pomelo.netease.com/lordofpomelo/).

##LordOfPomelo的主要内容
涵盖了主流MMORPG的核心内容: 多个不同游戏场景, 两种职业, 多种类型的任务, 丰富多彩的道具和武器, 组队, 副本, 以及与各种怪物和Boss的战斗. 玩家可以在多个虚拟场景中穿梭, 完成各种任务, 提升等级, 并和其他玩家互动.

LordOfPomelo采用了基于分区的场景管理, 一张地图表示一个游戏场景, 与一个独立的场景服务器对应, 由该服务器提供对应的服务. 这种设计在避免了复杂的跨服事务的同时提供了对服务器扩展的支持, 开发者可以通过加入新的游戏场景来提高整个服务端的负载能力. 为了考察Pomelo服务器的响应能力, 我们在场景中采用了实时游戏模式: 玩家的攻击, 技能释放, 道具的检取、使用等行为都是实时进行的. 

整个游戏采用了Pomelo框架的标准开发模式, 实现了集群化服务器管理, 并且可以使用LordOfPomelo中对线性扩展的支持, 加入新的服务器来提高总体的负载能力. 在经过多轮性能测试与优化后, 达到了单场景800人的负载能力, 同时可以保证良好的响应时间(100ms左右). 

##LordOfPomelo整体架构

<img src="http://pomelo.netease.com/resource/documentImage/lordofpomelo/lordofpomelo-all-arch.png" alt="lordofpomelo overall architecture" width="600px"></img>

如上图所示, LordOfPomelo包括两种类型的服务器: game-server和web-server. web-server是基于HTTP的web服务器, 玩家通过web-server实现注册和登录逻辑. 在玩家完成验证之后就会通过websocket连接到game-server集群, 进入实际的游戏场景之中. game-server是LordOfPomelo的核心服务器集群, 包括一组前端的websocket服务器, 以及后端的游戏逻辑服务器集群, game-server的架构如下图: 

<img src="http://pomelo.netease.com/resource/documentImage/lordofpomelo/game-server.png" alt="game server" width="600px"></img>

上图中的Client可以是任何支持websocket的客户端, LordOfPomelo中自带的客户端是通过HTML5实现的, 不但可以运行在PC的浏览器上, 而且可以运行在其它支持HTML5的终端中（如iPhone, iPad和配置较高的android设备）. 不同平台之间的玩家可以进行对等、实时的互动. 

如图所示, game-server中的服务器也分为两类: frontend server和backend server, frontend server是一组websocket服务器集群, 用来处理与websoket客户端之间消息通讯, 负责消息的转发, 过滤, 以及消息广播等功能. backend server则主要用来处理游戏逻辑, 包括各种不同类型的游戏逻辑服务器. 其中, 场景服务器是最重要的游戏服务器, 主要负责游戏场景管理, 游戏数据的更新和保存, 客户端请求的处理, 以及怪物和NPC行为的驱动等. 这些功能是通过与其他服务器的协同工作来实现的. 同时, 场景服务器也采取了可扩展的形式, 每个场景对应一个独立的场景服务器. 可以通过增加游戏场景来分散单个服务器的压力, 提高整体负载. 

##LordOfPomelo分析
* [LordOfPomelo服务器介绍](LordOfPomelo-服务器介绍)
* [LordOfPomelo中的数据压缩](https://github.com/NetEase/pomelo/wiki/Pomelo-%E6%95%B0%E6%8D%AE%E5%8E%8B%E7%BC%A9%E5%8D%8F%E8%AE%AE)
* [LordOfPomelo代码组织](LordOfPomelo-代码组织)
* [LordOfPomelo启动流程](LordOfPomelo-启动流程)


在与客户端通信的时候，pomelo目前提供了hybridconnector和sioconnector，其中hybridconnector支持tcp，websocket;sioconnector支持socket.io。但是实际编程中，只有这些connector可能还无法满足我们的需求，我们可能需要自己定制自己的connector，pomelo提供了定制connector的接口，在这部分就是要说明这个问题。

内建的connector分析
====================

pomelo内建的connector包括sioconnector和hybridconnector，这里以sioconnector为例来分析，说明如何实现一个connector。
首先sioconnector的构造函数里需要三个参数host、port、opts，(host,port)是要监听socket绑定的，在sioconnector的start调用中，会开启对应的监听，并使得当有连接事件发生时，能够将连接事件抛出。抛出连接事件的时候，对应的通信socket是SioSocket。SioSocket的事件中，当客户端主动断开连接时，需要触发disconnect事件，当通信出现错误时，触发error事件，当有消息获得的时候触发message事件。当收到客户端的请求message或者需要给客户端发送回应或者推送消息的时候，pomelo会使用connector的decode函数对数据进行解码。对于客户端请求的消息，其上报到应用层的格式应为：

```javascript

{ 
  id : <requestId>,
  route: <handlerRoute>,
  body:  <requestBody>
}

```

* 这里id是客户端请求的requestId，这个数值由客户端产生的，因此不同session的请求id是互相不干涉的。如果不是请求，只是一个notify的话，id值为空。route是对应应用服务器的请求位置，格式为"<ServerType>.<HandlerName>.<MethodName>"。body为具体请求时携带的参数信息,当我们发起filter-handler链对请求进行处理的时候，参数msg就是这里的body值，是在这里产生的。

* 对于服务器端给客户端的响应或者服务器端的推送消息，会使用connector的encode进行编码，编码函数的签名为:

    encode(reqId, route, msg);

其中，如果是响应的话，reqId是对应的请求id，route为请求携带的route,实际上可以省略，msg会具体的相应内容;

* 如果是推送消息的话，reqId为空值，route为客户端的route，也就是"on<XXX>"这种格式。其返回值应该是能被socket发送的缓冲区。

* decode/endcode函数还可以通过配置选项opts来进行配置，如果在opts里指定了encode/decode，那么将会优先使用opts中指定的encode/decode。

* connector还应实现stop方法，对于sioconnector来说，其stop方法里面关闭了监听socket连接。

经过对sioconnector的分析，我们完成了pomelo中connector的抽象。

connector抽象
==============

在涉及到客户端与服务器端进行通信的时候，往往都会使用类似与tcp服务器客户端通信的模式，我们的connector抽象也不例外。在这里，我们假定要实现一个FooConnector，看看需要实现些什么。

* 首先需要一个FooConnector，FooConnector的构造函数需要一些自己的参数，这些参数要包括创建一个连接监听所需要的所有信息，当然比较经典的参数信息是(host,port)对，但是对于一些比较特殊的connector来说，其连接监听所需要的信息可能就不是(host,port)对了，比如用于本地通信的share memory以及命名管道等。

* FooConnector需要实现一个start函数，在这个start函数中，会启动对连接的监听，最经典的操作应该是listen调用。当然在具体实现一些比较特殊的connector的时候，可能不会是listen调用。start中还应该对实现当有连接到来的时候，触发connector的connection事件，对应经典实现的accept返回，当然是异步的触发。在触发connection事件的时候，应该传出参数FooSocket。

* FooSocket是FooConnector触发connection事件时传出的参数，可以类比经典tcp通信中，accept返回的用于通信的socket。当FooSocket出现通信错误时，触发error事件;当遇到客户端主动断开连接时，应该触发事件disconnect;当收到客户端传来的消息时，应该能够触发message事件，message事件携带的参数为FooBuffer类型。

* FooBuffer类型可以类比经典tcp通信中的byte数组，在javascript中，FooBuffer一般为string或者Buffer类型，当然用户也可以定制自己的类型。需要注意的每一次message事件的触发，携带的都应该是一个完整的包，不能出现半包以及粘包，用户的connector实现要保证这一点。当然，只有类似与tcp这样的流协议的时候才可能出现半包粘包的问题，一些基于数据报的协议是不会出现这种问题的。

* Connector还需要提供一个decode函数，这个decode函数的参数为上面FooSocket的message事件携带的FooBuffer，这个decode函数应该能够把这个FooBuffer解码成具体的应用层能够直接使用的请求对象，也就是说decode函数的返回值应该为如下格式的对象:

```javascript
{
   id: <requestId>,
   route: <handlerRoute>,
   body: <requestBody>
}
```

* 当服务端向用户发起消息推送或者响应的时候，Connector应该提供encode函数，完成具体的打包操作，Connector提供的encode函数签名应该为:
    
    encode(reqId, route, body);

encode函数的返回值类型为FooBuffer，也就是FooSocket可以处理的类型，encode完成用户的请求数据的打包。如果是服务端推送数据的话，reqId的值应该为空。

* 由于我们自己定义了encode/decode函数，因此我们可以设计实现我们自己的线上协议，只要在应用层抛数据的时候保持一致即可。

* 当具体发送打包后的数据时，需要FooSocket提供一个发送方法send，send的参数就是encode打包后的FooBuffer，其签名为：
   
   send(FooBuffer);

* 在具体实现数据往客户端发送的时候，有时候并不是一旦数据产生就往外发出，而是会先缓存，定时发送数据，这样对于大量小包产生的场景，将会带来很大的性能提升。因为产生的很多小包，可以批量发出，因此FooSocket还要支持批量发消息，对应的函数签名为:

   sendBatch(FooBufferArray);

一般来说，对于底层协议是二进制协议的话，在打包的时候由于已经定义了包边界，因此当有多个包的FooBuffer要发出的时候，只需要将所有的Buffer打包成一个大的Buffer就可以了，hybridconnector中就是这样实现的。而在sioconnector中，因为其底层协议使用的json，因此其将这些消息组成了一个json数组，具体可以参考它们对应的实现。我们在实现FooSocket的sendBatch方法时，可以根据具体的实际情况进行实现，其语义就是一次批量发送多个包。

* FooSocket还应该有主动断开连接的方法disconnect，用于当服务器想把某个用户kick掉的时候调用。

* 当最后应用程序关闭的时候，FooConnector需要提供stop方法，用来关闭相应的连接监听，可以类比tcp服务器中最后关闭用来监听的socket。

* 综上所述，我们得出与定制Connector相关的类图，如下:

![pomelo](images/fooconnector.png)

* 在app.js中，如果我们的FooConnector的构造函数使用的绑定地址信息是(host,port)对的话，我们通过如下的调用，启用我们自己定制的connector:
```javascript

app.set('connectorConfig', {
    connector: FooConnector,
    encode : <encode func>, //optional
    decode : <decode func>, //optional
    others: <others>
    });
```

这里需要指出，通过opts配置的encode/decode会优先使用，如果没有通过opts配置encode/decode的话，将会使用connector配置的encode/decode，如果既没有配置encode/decode，又没有对connector实现decode/encode，将会出现错误。这里的connector配置项使用的是FooConnector的构造函数，当pomelo构造connector时，如果发现配置的是一个构造函数的话，会按如下的方式进行构造:

```javascript

  new FooConnector(host, clientPort, opts);

```

如果定制的FooConnector的构造的时候使用的地址信息不是(host,port),那么你就不能使用这种方式进行配置，你可以使用如下方式进行配置:

```javascript

var conn = new FooConnector(<addr_args>, opts);

app.set('connectorConfig', {
  connector: conn,
  
  // ....
});
```
小结
=========

在本部分，阐述了如何实现自定义connector，给出了connector的抽象，介绍了当实现一个全新的connector的时候应该需要实现的内容。pomelo对于connector的实现是完全开放的，用户可以根据自己的需求定制connector，定制自己的通信协议，只要自己的客户端与服务端线上协议保持一致就行了。

pomelo-admin-web 是 pomelo 框架中基于[pomelo-admin](https://github.com/NetEase/pomelo-admin)开发的web端监控的模块，可以通过 web 端的方式来对游戏服务器集群的运行状态，性能，日志等进行实时的监控，它采用‘类插件’的开发模式，开发者可以很方便的扩展具体的监控模块逻辑，目前在 adminConsole 中，集成的监控模块有如下几个： 

![Image](images/adminConsole1.png)

* systemInfo  
用于监控各个服务器上的系统信息，包括 loadavg,men,CPU(I/0),DISK(I/0)  

* nodeInfo  
用于监控各个服务器上的进程信息，包括 pid,cpu%,mem%，vsz，rss  

* conRequest  
用于监控由 connector 请求所产生的日志，包括玩家的登入，移动，切换场景等所花费的时间，并给出具体的路由(route)

* rpcRequest  
用于监控游戏服务器中 rpc 的调用情况，所花费的时间  

* forRequest  
用于监控由 forward 请求所产生的日志

* onlineUser  
用于实时监控在线玩家的信息，包括user login name，login ip，login time  

* sceneInfo  
用于实时监控玩家的场景信息，包括玩家所在的服务器，玩家所在的坐标等  

* scripts  
该模块提供了可以在 adminConsole 端在具体的服务器上执行脚本(script)  

* profiler  
该模块集成了chrome控制台下面的 Profiles 性能分析工具，可以用来对Pomelo服务器端的代码进行性能分析  

##adminConsole安装与使用  
运行环境：linux or mac os x   

    $ git clone https://github.com/NetEase/pomelo-admin-web.git
    $ cd pomelo-admin-web
    $ node app

浏览器中访问： http://localhost:7001， 就可以打开管理控制台界面。  
如果在此之前已经启动了 pomelo 项目，就可以在 adminConsole 上面进行监控了   
如果端口有冲突，请在config/admin.json修改端口，访问的浏览器必须支持websocket，推荐使用chrome.  

##scripts模块脚本编写注意事项  
scripts模块使用了 node.js 中的 [vm](http://nodejs.org/api/vm.html) module 来执行脚本  
内置提供了  
app --- pomelo application 实例    
os --- os 模块  
fs --- fs 模块  
process --- process 模块    
util --- util 模块    
来做为 vm 的 sandbox 上下文环境，即我们可以直接在脚本中调用这些  
为了便于输出结果，在 adminConsole 中，把执行的结果统一赋值给了全局 result 变量  
因此，在编写脚本的时候，要输出的结果要赋值给 result 变量（不要用 var 进行声明，它是全局的）  
比如，可以编写一个脚本来获取服务器的cpu数量信息  
```js
var cpus = os.cpus();
result = util.inspect(cpus,true,null);
```  

#LordOfPomelo代码组织

LordOfPomelo的代码主要包括两部分: 后端服务器代码game-server和前端客户端代码web-server. game-server是游戏服务端, 包括所有的游戏逻辑代码和游戏服务器代码. web-server是游戏客户端, 包括用户注册和登录界面代码, 以及一个用HTML5编写的游戏客户端. 除了这两部分之外, 还有一个公用的shared目录, 用来存放前后端共用的代码和配置. 

作为一个分布式的游戏服务器, LordOfPomelo可以同时运行在多台服务器上, 却统一使用同一套代码, 不同的服务器会根据配置加载各自的目录代码. 下图是LordOfPomelo的代码结构: 

![lordofpomelo_arch](http://pomelo.netease.com/resource/documentImage/lordofpomelo/code/LOP_arch.png)

## game-server服务端代码分析

![game-server](http://pomelo.netease.com/resource/documentImage/lordofpomelo/code/game-server.png)

game-server根目录下的app.js是服务器代码的入口, 其他目录的功能如下: 
* /app    : 服务端js代码, 包括服务器代码和游戏逻辑代码. 
* /config : LordOfPomelo中的配置文件. 
* /logs   : 服务器端运行时产生的日志文件. 
* /scripts: 统计模块对应的本地脚本. 
* /test   : LordOfPomelo中的测试用例

### 逻辑代码

逻辑代码主要用来完成具体的业务逻辑, 如用来驱动怪物的AI代码, 用来计算地图中路径的寻路代码等, 逻辑代码在/app/domain目录下: 

![logic](http://pomelo.netease.com/resource/documentImage/lordofpomelo/code/logic.png)

* /action : 负责处理客户端的请求. 由于场景是由tick驱动的, 而tick的间隔一般较短(默认100ms), 当请求需要在多个tick中执行的时候就会被封装为一个action来执行. 
* /aoi    : aoi相关逻辑, 包括aoi消息的封装, 以及对aoi消息的处理. 
* /area   : 场景相关逻辑, 提供场景中的主要接口. 包括: 场景中实体的加入、更新和删除, 广播消息的推送, 场景中服务的访问(AOI, AI等), 场景信息的获取等. 同时还包括一个Timer, 用来驱动场景中的逻辑. 
* /entity : 场景中的所有实体, 包括玩家, 怪物, npc, 宝物, 装备, 队伍等. 
* /event  : 用来集中处理场景逻辑中产生的各种事件, 包括玩家消息, 怪物消息等. 
* /map    : 用来完成地图的加载和解析, 以及地图中区域的抽象. 
* /task   : 任务相关的代码, 控制任务的执行和取消, 以及任务奖励的获得. 

### 服务器代码. 

![servers](http://pomelo.netease.com/resource/documentImage/lordofpomelo/code/servers.png)

服务器代码在/servers目录下, 通过规约的形式组织, 对外提供rpc接口, 处理客户端和服务端的请求并返回结果. LordOfPomelo中使用的服务器包括: 
* /area     : 场景服务器, 用来储存场景信息, 处理客户端的请求, 如用户添加, 删除, 攻击等操作. 
* /chat     : 聊天服务器, 处理聊天信息
* /connector: 连接服务器, 负责维护用户session, 接受用户数据, 并将服务端的广播数据推送给玩家
* /login    : 登录服务器, 用来验证用户登录信息
* /path     : 寻路服务器, 用来完成路径计算功能. 
* /manager  : 副本/组队服务器, 用来管理全局的副本和组队功能. 

## web-server代码架构

![web server](http://pomelo.netease.com/resource/documentImage/lordofpomelo/code/web_server.png)

LordOfPomelo的页面端代码主要分为两个部分: 基于HTML5开发的ui代码和使用colorbox开发的游戏逻辑代码. ui代码包括注册/登录页面, 游戏场景中的各种选项和菜单. 这些代码基于HTML5开发, 使用css3进行渲染. 游戏场景的绘制和游戏逻辑的驱动则是基于colorbox开发, 并使用到了HTML5中的很多特性. 

除此之外, web-server中还包括用户注册代码和oauth验证的逻辑, 这些代码在lib目录下. 

下图是页面端的内容: 

![client & html](http://pomelo.netease.com/resource/documentImage/lordofpomelo/code/client_html.png)

* /animation_json : 动画相关的json描述.
* /css            : 代码中所用到的css文件. 
* /image          : 客户端中用到的图片资源.
* /js             : 所有客户端的js文件.
* /index.html     : 是LordOfPomelo的入口文件.

下图是游戏js代码组织: 

![client & html](http://pomelo.netease.com/resource/documentImage/lordofpomelo/code/game_client.png)

* /config   : 客户端的配置信息.
* /handler  : 客户端的handler, 用来处理服务端response请求.
* /lib      : colorbox和pomelo的客户端通讯库代码.
* /model    : 客户端的游戏逻辑代码.
* /ui       : ui代码.
* /utils    : 客户端用到的工具类.
* /app.js   : 客户端的初始化入口, 负责初始化客户端的逻辑代码. 


LordOfPomelo的启动流程采用了Pomelo中的启动模式. 在阅读下面内容前, 请先阅读[pomelo启动流程](https://github.com/NetEase/pomelo/wiki/pomelo%E5%90%AF%E5%8A%A8%E6%B5%81%E7%A8%8B).

app.js是LordOfPomelo的入口, 主要负责所有服务器的配置, 以及组件的加载和启动. LordOfPomelo的启动主要分为两步：启动master服务器, 再由master服务器分别启动其他服务器. 

### 组件的配置和加载
LordOfPomelo中使用了多个外部组件, 这些组件在服务器启动时加载, 提供各种服务：如数据统计, 路由功能的替换, 游戏场景的初始化等. 

LordOfPomelo中使用了基于脚本的统计, 这些组件通过运行自定义的脚本, 收集服务器运行数据并生成报告, 更加具体的功能, 请见：

``` javascript
	var sceneInfo = require('./app/modules/sceneInfo');
	var onlineUser = require('./app/modules/onlineUser');
	if(typeof app.registerAdmin === 'function'){
    app.registerAdmin('sceneInfo', new sceneInfo());
    app.registerAdmin('onlineUser',new onlineUser(app));
	}
```

LordOfPomelo启动时还会加载areas的配置文件, 用来建立场景和服务器之间的映射:

``` javascript
  //Set areasIdMap, a map from area id to serverId.
	if (app.serverType !== 'master') {
	  var areas = app.get('servers').area;
	  var areaIdMap = {};
	  for(var id in areas){
	  	areaIdMap[areas[id].area] = areas[id].id;
	  }
	  app.set('areaIdMap', areaIdMap);
	}
```

为了能在多个场景服务器中正确的路由, LordOfPomelo中加载了自定义的路由组件, 通过使用场景与服务器之间的映射信息, 可以确保玩家的请求被分发到对应的场景服务器上:

``` javascript
  // route configures
	app.route('area', routeUtil.area);
	app.route('connector', routeUtil.connector);
```

除了服务器的通用配置以外, app.js中还负责不同服务的初始化工作: 如全局服务器的初始化, 场景的初始化, 以及寻路服务器的初始化, 这些初始化会根据服务器的类型进行不同的初始化过程: 

``` javascript
app.configure('production|development', 'area', function(){
  app.filter(pomelo.filters.serial());
  app.before(playerFilter());
  //Load scene server and instance server
  var server = app.curServer;
  if(server.instance){
    instancePool.init(require('./config/instance.json'));
    app.areaManager = instancePool;
  }else{
    scene.init(dataApi.area.findById(server.area));
    app.areaManager = scene;
  }
  //Init areaService
  areaService.init();
});
```

数据同步插件和MySql的初始化:

``` javascript
// Configure database
app.configure('production|development', 'area|auth|connector|master', function() {
  var dbclient = require('./app/dao/mysql/mysql').init(app);
  app.set('dbclient', dbclient);
  app.use(sync, {sync: {path:__dirname + '/app/dao/mapping', dbclient: dbclient}});
}); 
```

### 服务器的启动

LordOfPomelo的启动也采用了Pomelo框架中的启动方式, 即将master作为一个默认组件, 在app.js调用app.start()方法后加载, 启动master服务. 

master组件会负责启动其他所有服务. 这个启动过程分为两个阶段：第一阶段, master服务启动其他所有服务器, 在服务器启动完毕后, 其中的monitor组件会连到master对应的监听端口上, 表明该服务器启动完毕. 第二阶段, 在所有服务器都启动完毕之后, mater会调用所有服务器上的afterStart接口, 来进行启动后的处理工作. 


# LordOfPomelo介绍

LordOfPomelo是一个基于Pomelo游戏框架开发的MMORPG(大型多人在线角色扮演游戏)的游戏Demo, 具有角色、怪物、装备、战斗、聊天、技能、升级系统、任务系统、组队、副本等较为完整的游戏功能. 

LordOfPomelo服务端采用了Pomelo框架, 客户端采用了基于HTML5的colorbox框架, 在大约3个月的时间内实现快速开发. 服务端约8000行代码, 客户端约6000行代码. 支持单场景800人以上的并发访问, 响应时间控制在100ms左右. 

# 运行环境
* [nodejs](http://nodejs.org/)
* Windows、Linux 或 MacOS 操作系统
* MySql 数据库

# 安装LordOfPomelo

## 下载源码

`git clone https://github.com/NetEase/lordofpomelo.git`

## 安装依赖包 

进入目录：
`cd lordofpomelo`

安装依赖包：
`sh npm-install.sh`(Windows: `npm-install.bat`)

# 创建MySql数据库

## 创建数据库
sql文件路径：./game-server/config/schema/Pomelo.sql

* 安装MySql数据库(略)
* 登录MySql:
`mysql –u用户名 –p密码`
(登录成功提示符：mysql>)
* 创建数据库:
`mysql> create database Pomelo;`
* 选择数据库:
`mysql> use Pomelo;`
* 导入sql文件:
`mysql> source ./game-server/config/schema/Pomelo.sql`

## 修改数据库配置
数据库配置文件为./shared/config/mysql.json
```json
{
  "development": {
   "host" : "127.0.0.1",
    "port" : "3306",
    "database" : "Pomelo",
    "user" : "xy",
    "password" : "dev"
  },
  "production": {
   "host" : "127.0.0.1",
    "port" : "3306",
    "database" : "Pomelo",
    "user" : "xy",
    "password" : "dev"
  }
}
```

将"development"环境下的的数据库配置修改为实际的配置. 

# 运行游戏
需要分别启动game-server和web-server. 
game-server的启动方式：

* `pomelo start` (pomelo的安装方法参考[pomelo快速使用指南](https://github.com/NetEase/pomelo/wiki/pomelo快速使用指南)) 注: 如果上次启动的进程没有完全退出, 可以使用`pomelo kill --force`来结束所有node进程. 

web-server的启动方式：

* `cd web-server && node app`

# 访问游戏
本地运行, 直接在浏览器中访问 http://localhost:3001 或者 http://127.0.0.1:3001

浏览器需支持websocket, 推荐使用chrome. 

# 相关问题解决办法
1. 端口冲突

修改服务器配置文件./game-server/config/servers.json,内容如下：
```json
{
  "development": {
    "connector": [
      {"id": "connector-server-1", "host": "127.0.0.1", "port": 3150, "clientPort": 3010, "frontend": true},
      {"id": "connector-server-2", "host": "127.0.0.1", "port": 3151, "clientPort":3011, "frontend": true}
    ],
    "area": [
      {"id": "area-server-1", "host": "127.0.0.1", "port": 3250, "area": 1}, 
      {"id": "area-server-2", "host": "127.0.0.1", "port": 3251, "area": 2}, 
      {"id": "area-server-3", "host": "127.0.0.1", "port": 3252, "area": 3}, 
      {"id": "instance-server-1", "host": "127.0.0.1", "port": 3260, "instance": true},
      {"id": "instance-server-2", "host": "127.0.0.1", "port": 3261, "instance": true},
      {"id": "instance-server-3", "host": "127.0.0.1", "port": 3262, "instance": true}
    ],
    "chat": [
      {"id":"chat-server-1","host":"127.0.0.1","port":3450}
    ],
    "path": [
      {"id": "path-server-1", "host": "127.0.0.1", "port": 3550}
    ],
    "auth": [
      {"id": "auth-server-1", "host": "127.0.0.1", "port": 3650}
    ],
    "gate": [
      {"id": "gate-server-1", "host": "127.0.0.1", "clientPort": 3014, "frontend": true}
    ],
    "manager": [
      {"id":"manager-server-1","host":"127.0.0.1","port":3750}
    ]
  },
  "production": {
    // ...
  }
}
```

该配置文件分别定义了development和production环境下的各个服务器的配置信息, 包括服务器类型, 地址, 端口号等, production环境下的参数和development环境的结构类似. frontend参数为true时表示前端服务器. 端口冲突时可以修改相应的端口号. 

或者修改文件./web-server/public/js/config/config.js, 内容如下：
```json
__resources__["/config.js"] = {meta: {mimetype: "application/javascript"}, data: function(exports, require, module, __filename, __dirname) {
  module.exports = { 
    IMAGE_URL:'http://pomelo.netease.com/art/',
    GATE_HOST: window.location.hostname,
    GATE_PORT:3014
  };
}};
```
该文件是web服务器的常用配置信息: IMAGE_URL是图片等静态资源的地址; GATE_HOST是gate服务器接受websocket的入口, 所有的websocket请求须先经过gate服务器获取connector服务器的id, 然后再和connector建立连接; GATE_PORT是前端gate的端口号. manager服务器主要负责是副本和组队功能.

# 配置文件汇总说明
* ./game-server/config/master.json

master服务器的配置信息, 包括development和production环境下的服务器地址、端口号等. 

master服务器负责启动、关闭各服务器, 并监控所有服务器的状态信息. 
* ./game-server/config/servers.json

area、connector等服务器的配置信息, 包括development和production环境下的服务器地址、端口号等. 由于connector是前端服务器, 用于接收并转发玩家的请求, 所以会有clientPort. 

* ./shared/config/mysql.json

数据库配置信息, 在安装LordOfPomelo之后需要根据数据库安装的实际情况修改development和production环境的参数. 

* ./web-server/public/js/config/config.js

客户端图片等静态资源及HTTP访问地址的配置. 

# 登录问题说明
LordOfPomelo提供了注册新用户以及使用github, google, facebook, twitter和新浪微博授权的方式进行登录. 在使用github等授权方式进行登录时, 需要自己通过OAuth授权认证, 然后修改配置文件中的对应信息(./web-server/config/oauth.json). 


#各类服务器介绍

LordOfPomelo采用分布式的设计, 服务端是由一个服务器集群组成的, 包括：多台场景服务器, 一台或多台寻路服务器, 聊天服务器, 副本/组队服务器, 全局服务器, 长连接服务器等. 

![backend server](http://pomelo.netease.com/resource/documentImage/lordofpomelo/servers.png)

###connecter服务器

与web的短连接模式不同, 在网络游戏中客户端与服务端建立的都是长连接. 而长连接本身是需要一定的资源来维持的, 在LordOfPomelo中, 我们使用websocket协议在客户端和服务器之间建立连接. 而connector服务器就是用来维护这些连接, 并中转客户端和服务端之间的消息. 在LordOfPomelo中, 客户端和服务端的连接状态是通过一个抽象的session来维护的, session是一个客户端在服务端的标识, 用来维护用户的登录状态, 用户的基本信息, 以及用户的websocket连接信息. 

###gate服务器

gate服务器的主要作用是为用户提供一个统一的websocket入口, 并负责用户验证和connector服务器的分配. 与connector服务器不同, LordOfPomelo中只有一台gate服务器. gate服务器会向所有客户端暴露一个固定的websocket接口, 当用户登录时, 会首先连接gate服务器, 完成验证, 并获得由gate服务器分配的对应connetor服务器的信息. 之后, 客户端会断开与gate服务器的连接, 通过获取的信息连接对应的connector服务器, 获取对应的服务. 

###验证服务器

验证服务器负责用户注册和验证. 作为用户验证的统一入口, 提供远程调用接口供其他服务器调用, 来进行用户的验证. 验证服务器的主要作用是屏蔽认证验证的细节, 为其他服务器提供统一的验证接口. 

###场景服务器

在网络游戏中, 出于性能和负载的考量, 大的游戏世界总是会被分成多个区域, 这些不同区域就是场景. 在LordOfPomelo中, 一张游戏地图就是一个游戏场景, 与一台独立的场景服务器对应. 场景是构成LordOfPomelo游戏世界的基本单位, 不能进行分割和简单的并行扩展. 场景服务器负责维护场景中所有实体, 并驱动实体AI运行游戏逻辑. 

场景服务器负责处理游戏中的几乎所有逻辑, 同时为其他服务器提供操纵场景数据的接口. 在LordOfPomelo中, 虽然场景本身不能分割, 但可以通过加入新的游戏场景的方法来分散用户, 从而提高游戏服务器总的负载量. 而一些与场景相关的服务也可以通过独立运行的方式进行水平扩展. 

###寻路服务器

寻路服务是游戏服务器的基本服务之一, 玩家跑动, 怪物移动都需要寻路服务提供支持. 其功能是根据地图中的起点和终点, 得到一条这两点之间的最优路径. 由于寻路是典型的无状态、计算密集型服务, 在LordOfPomelo中, 我们将寻路逻辑与场景逻辑分离, 放在单独的寻路服务器中, 从而减轻了场景服务器的压力. 而寻路服务器也可以根据需要进行简单的并行扩展. LordOfPomelo中的寻路算法使用A*实现, 提供了通用的计算接口, 并封装为一个模块, 具体信息见[pomelo-pathfinding](https://github.com/NetEase/pomelo-pathfinding). 

###聊天服务器

聊天服务是网游的基本服务之一. 在LordOfPomelo中, 聊天服务是与场景服务分离的, 通过一个独立的服务器来实现. 聊天服务器会维护一份所有在线用户的数据, 通过这些数据与connector服务器通讯, 来实现玩家之间的即时通讯. 

###副本/组队服务器

副本/组队服务器是后端服务器集群中负责全局管理副本全生命周期和组队相关操作的功能服务器.具体可参考[lordofpomelo 0.3新特性](https://github.com/NetEase/pomelo/wiki/lordofpomelo-0.3%E6%96%B0%E7%89%B9%E6%80%A7) 

##场景管理与介绍

LordOfPomelo中的场景服务负责管理游戏中所有实体和整个游戏世界. 而出于安全性和一致性等方面的考虑, 所有的游戏逻辑验证都是在后端进行的, 因此场景服务还包括了游戏中所有的逻辑判断和处理. LordOfPomelo的场景服务是游戏服务的核心, 也是逻辑最为复杂的部分, 下面就对LordOfPomelo中的场景服务进行分析：

###LordOfPomelo中的场景管理

LordOfPomelo中每个场景对应一个独立的场景服务器, 所有的业务逻辑都在场景服务器内部进行. 对于跨场景的操作, 则是通过一个全局服务器来进行处理. 下图就是一台单独的场景服务器的功能：

![area](http://pomelo.netease.com/resource/documentImage/lordofpomelo/area.png)
 
####实体管理

游戏场景中的所有实体都会在进入场景时加载到内存中, 之后所有的修改都会直接在内存中进行, 并通过数据同步模块来定时同步到数据库中. 这一设计将场景中所有的数据操作都变成了直接的内存操作, 提高了整体性能, 规避了频繁的缓慢IO操作. 

LordOfPomelo中实体的定义都在domain目录下的entity文件夹中, 采用了面向对象的设计思想, 所有实体都继承自entity类. 实体的加入和删除都通过area中的接口(addEntity/removeEntity)来处理, 从而减轻了对象的管理负担. 

####消息服务

LordOfPomelo中的消息服务可以分为两种：一对一的RPC请求<-->响应, 以及一对多的广播消息. 
由于LordOfPomelo中的逻辑验证是在服务端进行的, 对于客户端的大部分请求, 服务端都会有一个直接的回复来进行处理, 这种回复是使用了类似于web中的request/response模式来实现的. 

对于广播服务, LordOfPomelo中使用了基于AOI的区域通知服务. 即在收到广播消息后, 根据消息类型, 通过AOI服务获得需要通知的玩家列表, 然后对该列表中的玩家进行广播, 从而大幅减少了消息的数量. 

####AOI服务

玩家的视野一般远小于场景的大小, 因此对于场景中的绝大部分消息, 进行简单的全场景广播是没有必要而且无法承受的. 当有消息需要发送时, 如何确定该消息需要通知的玩家列表就是AOI模块的功能了. 

LordOfPomelo中实现的是基于灯塔的AOI服务. 其基本的实现方法是将整个地图划分为若干个等大的tower, 每个tower负责维护一个对象列表, 指向所有在这个tower范围内的对象. 然后在这个数据结构的基础上来触发各种AOI事件. 


在这部分，我们将讨论关于rpc调用相关的问题。在pomelo中rpc的调用主要是通过proxy组件和remote组件实现，其中proxy组件主要负责创建rpc客户端代理，让开发者在pomelo中更方便地进行rpc调用；remote组件主要负责加载rpc服务，包括系统的rpc服务和用户的rpc服务。Pomelo的rpc框架主要解决了两个问题，第一个就是进程间的路由策略，第二个则是rpc底层的通信协议的选择。对于第一个问题，pomelo提供了一套灵活的路由机制，并允许开发者根据需要自由地控制路由信息；对于第二个问题，pomelo现在支持基于socket.io的通信机制和基于原生socket的通信机制。下面我们就分别介绍rpc客户端和服务端的具体实现：

## RPC客户端
rpc客户端主要负责产生代理对象，加载路由策略和进行消息的转发。
### proxy组件
在进行pomelo开发的过程中，进行rpc调用的代码如下：

```
app.rpc.chat.chatRemote.add(session, uid, serverId, param, cb);
```

在pomelo中之所以能够如此简洁地进行rpc调用是因为javascript的语言特性和pomelo底层对rpc客户端进行的封装。proxy组件在启动时首先会生成一个rpc client，同时监听系统中服务器增加、服务器移除、服务器替换事件；当这些事件被触发时，proxy组件会根据相应的事件信息对服务器代理对象进行相应的动态变化。例如，当有新的服务器增加时，proxy组件会增加该服务器的代理对象；当有服务器被移除后，proxy组件会移除该服务器的代理对象。在proxy组件启动完成时会将rpc client生成的代理对象挂载到app.rpc下，这样开发者在进行rpc调用时就可以匹配到对应的代理对象，从而通过rpc client进行相应的rpc调用。

### RPC client
对于rpc client，其整体架构图如下所示：

<center>
![rpc client](http://pomelo.netease.com/resource/documentImage/rpc-client.png)
</center>

在最底层，使用mail box的抽象隐藏了底层通讯协议的细节。一个mail box对应一个远程服务器的连接。Mail box对上提供了统一的接口，如：连接，发送，关闭等。Mail box内部则可以提供不同的实现，包括底层的传输协议，消息缓冲队列，传输数据的包装等。开发者可以根据实际需要，实现不同的mail box，来满足不同的底层协议的需求。现在pomelo提供基于socket.io的mail box和基于原生socket的mail box，默认使用socket.io。

在mail box上面，是mail station层，负责管理底层所有mail box实例的创建和销毁，以及对上层提供统一的消息分发接口。上层代码只要传递一个目标mail box的id，mail station则可以知道如何通过底层相应的mail box实例将这个消息发送出去。开发者可以给mail station传递一个mail box的工厂方法，即可以定制底层的mail box实例的创建过程了，比如：连接到某个服务器，使用某一类型的mail box，而其他的服务器，则使用另外一个类型的mail box。

再往上的是路由层。路由层的主要工作就是提供消息路由的算法。路由函数是可以从外面定制的，开发者通过注入自定义的路由函数来实现自己的路由策略。每个rpc消息分发前，都会调用路由函数进行路由计算。容器会提供与该rpc相关的玩家会话对象（当中包含了该玩家当前的状态）和rpc的描述消息（包含了rpc的具体信息），通过这两个对象，即可做出路由的决策。路由的结果是目标mail box的id，然后传递给底下的mail station层即可。

最上面的是代理层，其主要作用是隐藏底层rpc调用的细节。Pomelo会根据远程接口生成代理对象，上层代码调用远程对象就像调用本地对象一样。但这里对远程代理对象有两个约定的规则，即第一个参数必须是相关玩家的session对象，如果没有这么一个对象可以填充null，在路由函数中需做特殊处理。还有就是最后一个参数是rpc调用结果的回调函数，调用的错误或是结果全部通过该回调函数返回，且这个参数不能省略。而在远程服务的提供端，方法的声明与代理端的声明相比，除了不需要第一个session参数，其余的参数是一样的。

### rpc请求流程
对于发送rpc请求，rpc客户端采用了一种懒加载的机制，其主要实现思路是客户端与服务端的连接并不是在服务器启动后就创建，而是当客户端第一次向服务端发起rpc请求时才真正建立连接。当客户端与相应的服务端建立连接后，以后有从该客户端到对应服务端的请求就无需再建立连接，消息可以直接发送。消息的发送过程类似前面介绍的handler-filter链处理模式，同样在rpc请求过程开发者可以添加before和after filter对消息进行相应的处理，现在pomelo内建的rpc filter包括rcpLog和toobusy。

## RPC服务端
rpc服务端主要负责接收客户端的rpc请求后将相应的消息转给客户端请求的rpc服务中，同时将rpc服务处理完成的消息返回给rpc客户端。
### remote组件
remote组件在启动时会创建一个rpc server，同时加载系统中所有的rpc服务；remote组件在关闭时会停止rpc server的所有服务。
### RPC server
对于rpc server，其整体架构图如下所示：

<center>
![rpc server](http://pomelo.netease.com/resource/documentImage/rpc-server.png)
</center>
 
最底下的是acceptor层，主要负责网络监听，消息的接收和解析。Acceptor层与mail box层相对应，可以看成是网络协议栈上同一层上的两端，即从mail box层传入的消息与acceptor层上传出的消息应该是同样的内容。所以这两端的实例必须一致，使用同样的底层传输协议，对传输的数据使用同样格式进行封装。在客户端替换了mail box的实现，则在服务提供端也必须替换成对应的acceptor实现。同mail box一样，pomelo提供基于socket.io的acceptor和基于原生socket的acceptor。

往上是dispatch层。该层主要完成的工作是根据rpc描述消息将请求分发给上层的远程服务。

最上层的是远程服务层，即提供远程服务业务逻辑的地方，由pomelo框架自动加载remote代码来完成。

## 总结
在本部分，详细介绍了rpc客户端和服务端的通信机制，包括对mail box、mail station、acceptor、gateway的功能进行了阐述，同时分析了pomelo中proxy组件和remote组件的相关功能。

##pomelo-cli 交互式命令行
pomelo-cli 提供了一个交互式命令行，开发者可以使用这个工具对使用[pomelo](https://github.com/NetEase/pomelo)框架开发的应用和服务进行运维  

### 安装
```
npm install -g pomelo-cli
```

### 登录
使用命令  
```
pomelo-cli -h host -P port -u username -p password  
```

默认的pomelo-cli登录参数  
```
pomelo-cli -h 127.0.0.1 -P 3005 -u monitor -p monitor
```

登录用户的用户名密码权限等级是在config/adminUser.json里面进行配置的  
具体可以参考[admin user](https://github.com/NetEase/pomelo-admin#user-level-control)  

对于kill, stop, add ,enable, disable 等命令是受权限限制的，非admin用户将无权进行操作  

### 命令
#### use  
使用某个context来进行操作，context可以是serverId或者是all  
use {serverId|all}  
之后你的命令就会被应用到该context  
```
example: use area-server-1  
example: use all  
```

#### quit
敲入 **quit** 你就会退出 pomelo-cli  

#### kill
关闭所有服务器  
```
example: kill
```
**注意**：小心使用该命令  

#### exec
执行脚本文件  
exec {filepath}  
filepath 可以是相对于pomelo-cli命令执行的路径  
```
example : exec xxx.js 
```
等价于 exec pwd/xxx.js  

filepath 也可以是以 / 开头的绝对路径  
```
example : exec /home/user/xxx.js
```

脚本文件的执行是通过 [vm](http://nodejs.org/api/vm.html) 模块  
vm context 是  
```
var context = {
  app: this.app,
  require: require,
  os: require("os"),
  fs: require("fs"),
  process: process,
  util: util
};
```
执行结果是通过 **result** 参数  
因此，你在脚本文件里，你需要使用**result**来得到返回结果  
getCPUs.js
```
var cpus = os.cpus();
result = util.inspect(cpus,true,null);
```

#### get
等价于 app.get(key)  
get {key}  

#### set
等价于 app.set(key, value)  
set {key} {value}  
**注意**：value 必须是 string 或者简单的value  

#### add
动态添加服务器到pomelo集群中  
add 参数是来自于servers.json配置文件中的 key = value 对
```
example: add host=127.0.0.1 port=3451 serverType=chat id=chat-server-2  
example: add host=127.0.0.1 port=3152 serverType=connector id=connector-server-3 clientPort=3012 frontend=true  
```

**注意**：添加服务器必须使用正确完整的参数，否则添加的服务器会处于bad模式  

#### stop
停止服务器，以serverId作为参数  
stop {serverId}  
```
example: stop area-server-1 
```

#### show
查看信息比如：servers, connections  
可以查看如下信息：  
servers, connections, logins, modules, status, proxy, handler, components, settings  
```
example: show servers  
example: show connections  
example: show proxy  
example: show handler  
example: show logins  
```
**注意**: 只有查看servers的时候是可以在任何一个context下面的，其他的所有的信息查看必须在某一个server的context下进行。

#### enable
enable admin module 设置 或者 enable app 设置  
enable module {moduleId}  
enable app {settings}  
```
example: enable module systemInfo  
example: enable app systemMonitor
```

#### disable
disable admin module 设置 或者 disable app 设置  
disable module {moduleId}  
disable app {settings}
```
example: disable module systemInfo  
example: disable app systemMonitor
```

#### dump
dump v8 heap 和 cpu 以供之后的分析  
dump cpu|memory {filepath} [times] [--force]  
times 是 cpu dump 所需要的时间，以秒为单位  
```
example: dump cpu /home/xxx/test 5  
example: dump memory /home/xxx/test 
```
**注意**：你可以使用 --force 来覆盖写入已经存在的文件  
```
example: dump cpu /home/xxx/test 5 --force  
example: dump memory /home/xxx/test --force
```

##### 分析dump结果  
打开[google chrome](https://www.google.com/intl/en/chrome/browser/)浏览器，按下F12来打开浏览器控制台  
找到**profile**标签，右键选择**Load profile...**  
选择dump文件，点击**open**。dump 文件就会被载入，你就可以进行分析  
关于dump的更多信息，你可以访问[ndump](https://github.com/piaohai/ndump)  

在这一部分，我们来实现一个简易的分布式聊天应用，为了简单化，我们将直接从github上获取对应的源码，当然你也可以首先`pomelo init`,获得一个初始的项目目录，然后参照github上的源码，建立相应的目录，在默认的位置填充相应的源码。


源码结构
===========

源码在github上面，通过如下命令，获得：

    $ git clone https://github.com/NetEase/chatofpomelo-websocket.git
    $ git checkout tutorial-starter

这个是很简单的应用，其代码结构如下图：

![源码结构图](images/source.png)

#### game-server

game-server目录放的是所有游戏服务器的逻辑，以文件app.js作为入口，运行游戏的所有逻辑和功能。从图上可以看出其servers里面有三个目录，分别是gate，connector，chat。在pomelo中，使用路径来区分服务器类型，因此三个目录代表了三种不同类型的服务器，每一个目录下面可以定义handler,remote,定义了handler和remote就决定了这个服务器的行为。

* 对于gate服务器，其逻辑实现代码在其gateHandler.js中，它接受客户端查询connector的请求，返回给客户端一个可以连接的connector的(ip,port);

* connector服务器，其逻辑代码在entryHandler.js中，它主要完成接受客户端的请求，维护与客户端的连接，路由客户端的请求到chat服务器;

* chat服务器，其既有handler代码，也有remote代码， handler中处理用户的send请求，而remote是当有用户加入或者退出的时候，由connector来发起远程调用时调用的。在remote里由于涉及到用户的加入和退出，所以会有对channel的操作。

game-server 的子目录config下面是游戏服务器所用到的配置文件存放的地方，配置信息使用JSON格式，包含有日志，master服务器和其他服务器的配置信息。除了这个pomleo所需的配置信息外，一般情况下，也将游戏逻辑所需要的配置信息放到这个目录下，例如数据库的配置信息，地图信息等。

logs子目录下存放游戏服务器产生的所有的日志信息。 

#### web-server

由于我们这个聊天应用的客户端是web，所以需要一个web服务器。在这个目录下，主要是客户端的js，css和静态资源等等。在本例子中，里面有用户登录，聊天的逻辑的js文件等等。我们在这个例子教程中，更多地关注的是服务器端的逻辑以及功能，对于客户端，我们几乎不需要怎么修改其代码，直接使用默认就好。

安装及运行
===============

首先，确保你已经成功安装了pomelo。执行命令安装依赖:

    $ sh npm-install.sh

启动游戏服务器:

    $ cd game-server
    $ pomelo start

启动web服务器:

    $ cd web-server
    $ node app.js

如果启动过程中没有问题的话，下面我们就可以使用我们的聊天服务了，打开浏览器，输入`http://127.0.0.1:3001/index.html`, 输入一个用户名和一个房间名，就可以加入到聊天中了。可以多开几个客户端实例，测试chat是否能正常地运行，可以在一个房间里广播，也可以单个给某一个人发消息，效果图如下： 

![chat](images/chatofpomelo.png)

chat分析
================

我们要搭建的pomelo聊天室具有如下的运行架构：

 ![multi chat](images/multi-chat.png)

 在这个架构里，前端服务器也就是connector专门负责承载连接， 后端的聊天服务器则是处理具体逻辑的地方。
 这样扩展的运行架构具有如下优势：
 * 负载分离：这种架构将承载连接的逻辑与后端的业务处理逻辑完全分离，这样做是非常必要的， 尤其是广播密集型应用（例如游戏和聊天）。密集的广播与网络通讯会占掉大量的资源，经过分离后业务逻辑的处理能力就不再受广播的影响。

 * 切换简便：因为有了前、后端两层的架构，用户可以任意切换频道或房间都不需要重连前端的websocket。

 * 扩展性好：用户数的扩展可以通过增加connector进程的数量来支撑。频道的扩展可以通过哈希分区等算法负载均衡到多台聊天服务器上。理论上这个架构可以实现频道和用户的无限扩展。

#### 客户端
聊天室的逻辑包括以下几个部分：
*   用户进入聊天室：这部分逻辑负责把用户信息注册到session，并让用户加入聊天室的channel。
*   用户发起聊天： 这部分包括了用户从客户端发起请求，服务端接收请求等功能。
*   广播用户的聊天： 所有在同一个聊天室的客户端收到请求并显示聊天内容。
*   用户退出： 这部分需要做一些清理工作，包括session和channel的清理。

客户端首先要给gate服务器查询一个connector服务器，gate给其回复一个connector的地址及端口号，这里没有列出完整的代码，具体的代码在路径web-server/public/js/client.js中,详细代码略去，见client.js:

```javascript
fuction queryEntry(uid, callback) {
  var route = 'gate.gateHandler.queryEntry';
  // ...
}

$("#login").click(function() {
  username = $("#loginUser").attr("value");
  rid = $('#channelList').val();

  // ...

 //query entry of connection
  queryEntry(username, function(host, port) {
    pomelo.init({
      host: host,
      port: port,
      log: true
    }, function() {
              // ...
    });
  });
});

```

客户端在查询到connector后，需要发请求给connector服务器， 第一次请求要给connector进程，因为首次进入时需要绑定对应的uid信息，这里略去详细代码:

```javascript
pomelo.request('connector.entryHandler.enter', {username: username, rid: rid}, function(){
  // ...
}); 
```
当用户发起聊天的时候，会请求服务chat.chatHandler.send，大致代码如下:

```javascript
pomelo.request('chat.chatHandler.send', {content:msg, from: username, target: msg.target}, function(data) {
  // ...
});
```
当有用户加入、离开以及发起聊天时，同房间的人将会收到服务端推送来的相应消息,这些在客户端是以回调的方式进行添加的，大致代码如下：

```javascript

pomelo.on('onAdd', function(data) {
  // ...
});

pomelo.on('onLeave', function(data) {
  // ...
});

pomelo.on('onChat', function(data) {
  // ...
});

```

客户端的详细代码都在目录web-server/public/js/client.js文件中，这里，客户端的js是使用[component](https://github.com/component/component)进行管理的,详细请参阅component的参考文档。

### 服务端

我们知道，在pomelo中，只要定义了一个服务器的handler和remote，那么就定义了这个服务器的行为，就决定了这个服务器的类型。在本例子中，有三种服务器，gate，connector，chat,它们完成的具体逻辑如下:

* gate完成客户端对connector的查询，在其handler了里有其实现的代码，由于在这里，本例中仅仅配置了一台connector服务器，因此直接返回其信息给客户端即可，然后客户端就可以连接到connector了。

```javascript
handler.queryEntry = function(msg, session, next) {
	var uid = msg.uid;
	// ...
};
```

* connector接受用户的连接，完成用户的注册及绑定，维护客户端session信息，处理客户端的断开连接，其逻辑代码在connector/handler/entryHandler.js中。大致如下：

```javascript
handler.enter = function(msg, session, next) {
	var self = this;
	var rid = msg.rid;
	var uid = msg.username + '*' + rid
	var sessionService = self.app.get('sessionService');
  // .....
};
```

* chat服务器是执行聊天逻辑的地方，它维护channel信息，一个房间就是一个channel，一个channel里有多个用户，当有用户发起聊天的时候，就会将其内容广播到整个channel。chat服务器还会接受connector的远程调用，完成channel维护中的用户的加入以及离开，因此chat服务器不仅定义了handler，还定义了remote。当有客户端连接到connector上后，connector会向chat发起远程过程调用，chat会将登录的用户，加到对应的channel中，其大致代码为：

```javascript
// chatHandler.js
handler.send = function(msg, session, next) {
	var rid = session.get('rid');
	var username = session.uid.split('*')[0];
	// .....
};

// chatRemote.js
ChatRemote.prototype.add = function(uid, sid, name, flag, cb) {
	var channel = this.channelService.getChannel(name, flag);
};

ChatRemote.prototype.kick = function(uid, sid, name) {
	var channel = this.channelService.getChannel(name, false);
  // ...
};
```
* **注意** 在实现具体的Handler的时候，最后需要调用next，其中next的签名为 next(err, resp).如果没有出现错误，那么err为空即可；如果不是request请求，而是notify的话，则一样需要调用next，此时resp参数是不需要的，一般情况下，如果没有错误的话，就直接使用``next(null)``即可。

服务器配置信息在config目录下，现在我们只关注servers.json, master.json。master.json配置是master服务器的配置信息，包括地址端口号，servers.json配置具体的应用服务器信息。在配置文件中，分为development和production两种环境，表示开发环境和产品环境，我们在`pomelo start`后面可以通过-e可以指定使用哪个环境，更多帮助参见`pomelo start --help`。

小结
========

在这部分，我们下载了一个简单的聊天应用，并安装运行起来，并对其源码进行了分析。在本例子中，为了简单起见，我们对每一种类型仅仅配置一台服务器，其中对于前端服务器来说需要指定frontend为true。[下一步](扩充服务器 "多台服务器")，我们将对每一种服务器类型配置多台服务器，以此来展示pomelo强大的可伸缩性。


##pomelo-daemon
pomelo-daemon 提供了一个 daemon 服务，可以用这个服务来进行分布式部署以及日志收集

### 安装
```
npm install -g pomelo-daemon
```

### 使用
#### 启动pomelo集群  
* 在服务器上面部署代码  
* 把servers.json上面的host配置称为正确的host，而不是 '127.0.0.1'  
* 在config文件夹下面添加daemon.json文件  
daemon.json 例子
```json
{
    "id": "dh37fgj492je",
    "key": "agarxhqb98rpajloaxn34ga8xrunpagkjwlaw3ruxnpaagl29w4rxn",
    "algorithm": "sha256",
    "user": "pomelo"
}
```
**注意**：pomelo-daemon 使用 [hawk](https://github.com/hueniverse/hawk) 来提供服务间的请求认证  
* cd 到 /game-server 路径下面  
* 在master服务器上，敲入命令  
```
pomelo-daemon
```
* 在其它服务器上，敲入命令  
```
pomelo-daemon --mode=server
```
**注意**：你可以使用nohup来部署daemon  
```
nohup pomelo-daemon --mode=server
```
* 在master服务器上，pomelo-daemon client，敲入命令  
```
start all
```
* pomelo 集群启动起来了  

#### daemon rpc 日志收集  
pomelo-daemon 提供了 pomelo rpc 日志收集同步到 mongodb，然后可以通过 [pomelo-admin-web](https://github.com/NetEase/pomelo-admin-web) 来进行分析查看  
* 添加 mongo.json 文件到 config 文件夹下面  
mongo.json 例子  
```json
{
    "host": "localhost",
    "port": 27017,
    "username": "pomelo",
    "password": "pomelo",
    "database": "test",
    "collection": "cpomelo"
}
```
* 启动 pomelo-daemon rpc logger 收集，使用 --pattern 参数来设置 rpc-log 文件的patterns  
```
pomelo-daemon --mode=server --log --pattern=rpc-log
```
**注意**：rpc-logs 日志收集仅仅用于调试，在生产环境下面不建议使用rpc-logs模式