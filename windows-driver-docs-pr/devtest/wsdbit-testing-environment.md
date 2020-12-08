---
title: WSDBIT 测试环境
description: WSDBIT 测试环境
keywords:
- WSDBIT 工具 WDK，测试环境
- WSDAPI 基本互操作性工具 WDK，测试环境
- WSDBIT 工具 WDK，网络拓扑
- WSDAPI 基本互操作性工具 WDK，网络拓扑
- 测试环境 WDK WSDBIT
- WSDBIT 工具 WDK，服务
- WSDAPI 基本互操作性工具 WDK，服务
- SimpleService 服务 WDK WSDBIT
- AttachmentService 服务 WDK WSDBIT
- EventingService 服务 WDK WSDBIT
- WSDBIT 工具 WDK，用于测试的设备
- WSDAPI 基本互操作性工具 WDK、用于测试的设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a66f5f4ea5e590e2c69d4b72dd647d8edc687d69
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810631"
---
# <a name="wsdbit-testing-environment"></a>WSDBIT 测试环境

本主题介绍物理环境和设备及其托管服务功能。

## <a name="network-model"></a>网络模型

要测试的设备和客户端连接到以太网网段，并构成单个 IP 子网。 网络寻址方案 (例如 IPv4、IPv6 或主机名) 并不相关，只要客户端和设备至少支持一个公共方案，子网中必须只有一个设备和一个客户端。

为了便于调试和故障排除，你应该使用网络监视器来监视设备与客户端之间的流量交换。 若要监视所有流量，必须将设备和客户端通过以太网集线器连接到网段。 如果某个集线器不可用，则可以通过在运行 WSDBIT 的计算机上安装网络监视器来监视流量。

下图显示了由设备、客户端和网络监视器组成的网络拓扑，它们都是通过集线器连接的。

![说明用于 wsdapi 基本互操作性工具的网络拓扑的示意图 (wsdbit) 测试](images/wsdbit1.png)

## <a name="test-device"></a>测试设备

若要参与设备端测试，应按照以下一般准则所述来实现设备。 有关设备实现的详细信息，请参阅 Web 服务的 [WSDBIT 参考](wsdbit-reference.md) 和 [设备配置文件 (DPWS) ](http://schemas.xmlsoap.org/ws/2006/02/devprof/) 规范。

下表描述了服务和互操作性测试用例依赖关系。

|方案|SimpleService|AttachmentService|EventingService|
|----|----|----|----|
|设备和服务检查|一个或多个 SimpleService、|AttachmentService,|或 EventingService|
|设备控制|X| | |
|Attachments| |X| |
|事件处理| | |X|

测试设备应托管三种类型的服务：

- `https://schemas.example.org/SimpleService`

- `https://schemas.example.org/AttachmentService`

- `https://schemas.example.org/EventingService`

### <a name="simpleservice"></a>SimpleService

**SimpleService** 服务有四种方法：

- **单向** 方法是将整数作为参数的单向方法。

- **双向** 是请求-响应方法，其中两个整数在请求中，并在响应中包含这些整数的总和。

- **TypeCheck** 是请求-响应方法，其中有许多不同类型的请求和响应中的完全相同的类型，包括 boolean、decimal、Float 和 url 列表。

- **AnyCheck** 是请求-响应方法，其中包含请求中的 XML 片段，并在响应中返回同一个片段。

### <a name="attachmentservice"></a>AttachmentService

**AttachmentService** 服务发送和接收附件。 要发送和接收的附件数据在 \\ 互操作目录中包含为两个单独的文件： `Image1.jpg` 和 `Image2.jpg` 。 此服务有两种方法：

- **OneWayAttachment** 是一种单向方法，其中附件作为参数。

- **TwoWayAttachment** 是一个请求-响应方法，其中包含请求和响应中的附件。

### <a name="eventingservice"></a>EventingService

**EventingService** 服务有两种可订阅的事件：

- **SimpleEvent** 是没有参数的事件。

- **IntegerEvent** 是返回整数的事件。

## <a name="implementing-test-services"></a>实现测试服务

若要执行所有互操作性测试事例，必须实现所有这些服务。 在这种情况下，在初始启动后，设备会承载其中每个服务的一个实例。

但是，如果你只想实现其中部分服务，请参阅本主题开头处的表，获取有关服务和互操作测试用例依赖项的信息。

>[!NOTE]
>若要尝试任何高级互操作性方案 (例如 [设备控制](device-control-scenarios.md)、 [附件](attachments-scenarios.md)和 [事件](eventing-scenarios.md)) ，测试设备至少必须支持 [设备和服务检查测试事例](device-and-service-inspection-scenarios.md)。 如果设备未通过该测试用例，则你可能无法继续高级测试用例。

测试设备和 WSDBIT 设备 (WSDBIT \_ server) 必须能够执行以下操作：

- 显示 **SimpleService** 单向方法的整数输入参数。

- 显示在双向类型检查请求中提交的类型的值。

- 验证收到的附件是否与预期的已知附件有关，并且必须显示此验证的结果。

- 启动 **EventingService** 到手动输入或计时器中描述的两种事件。

- 显示在可扩展 (**xs： any**) 部分中接收的数据。

- 使用 **xs： anyURI testdevice** 作为用于发现的 **wsd： scope** 元素。
