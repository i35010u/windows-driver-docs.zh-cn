---
title: 面向连接的环境
description: 面向连接的环境
keywords:
- 面向连接的 NDIS WDK，环境
- CoNDIS WDK 网络，环境
- 面向连接的 NDIS WDK，微型端口驱动程序
- CoNDIS WDK 网络，微型端口驱动程序
- 微型端口驱动程序 WDK 网络，CoNDIS
- 面向连接的 NDIS WDK，呼叫管理器
- CoNDIS WDK 网络，呼叫管理器
- 呼叫经理 WDK 网络，面向连接的操作
- 面向连接的 NDIS WDK，MCM 驱动程序
- CoNDIS WDK 网络，MCM 驱动程序
- MCM 驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a70222ba286612081c7c9cad9cce8ef0e031ac15
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838759"
---
# <a name="connection-oriented-environment"></a>面向连接的环境





NDIS 支持以下面向连接的驱动程序：

-   面向连接的客户端

-   呼叫管理器

-   集成微型端口呼叫管理器 (MCM) 驱动程序

-   面向连接的微型端口驱动程序

下图显示了面向连接的客户端、呼叫管理器和微型端口驱动程序的配置。

![说明面向连接的客户端、呼叫管理器和微型端口驱动程序的配置的示意图](images/conormed.png)

下图显示了面向连接的客户端和集成 MCM 驱动程序的配置。

![具有集成 mcm 驱动程序的面向连接的环境](images/conorcli.png)

*面向连接的微型端口驱动程序* 控制 (nic 的一个或多个网络接口卡) 并在面向连接的协议驱动程序 (面向连接的客户端和调用管理器) 和 NIC 硬件之间提供接口。

有关面向连接的微型端口驱动程序执行的面向连接的操作的摘要，请参阅 [小型端口驱动程序执行的面向连接的操作](connection-oriented-operations-performed-by-miniport-drivers.md)。

*调用管理器* 是一个 NDIS 协议驱动程序，它为面向连接的客户端提供调用设置和清理服务。 呼叫管理器：

-   使用面向连接的微型端口驱动程序的发送和接收功能，与网络实体（例如网络交换机或远程对等）交换信号消息。

-   支持一个或多个信号协议驱动程序。 有关呼叫管理器执行的面向连接的操作的摘要，请参阅 [呼叫管理器执行的面向连接的操作](connection-oriented-operations-performed-by-call-managers.md)。

*集成的 MCM 驱动程序* 是面向连接的微型端口驱动程序，它还向面向连接的客户端提供呼叫管理器服务。 MCM 驱动程序具有以下特征：

-   MCM 驱动程序向客户端提供与面向连接的微型端口驱动程序成对使用的面向连接的服务但是，调用管理器到小型端口驱动程序接口是驱动程序内部的，因此不透明到 NDIS。

-   多个呼叫管理器和 MCM 驱动程序可以共存于同一个环境中。

-   每个呼叫管理器或 MCM 驱动程序均可支持多个信号协议驱动程序。

有关 MCM 驱动程序和调用管理器的详细比较，请参阅 [MCM 驱动程序与呼叫管理器有何不同](mcm-drivers-vs--call-managers.md)。

*面向连接的客户端*：

-   使用呼叫管理器或 MCM 驱动程序的调用设置和关闭服务。

-   使用面向连接的微型端口驱动程序的发送和接收功能，或使用 MCM 驱动程序来发送和接收数据。

-   可以在其上边缘向更高层的应用程序提供其自己的网络和传输层服务。

-   使用呼叫管理器的服务和面向连接的微型端口驱动程序，或在其上边缘使用 MCM 驱动程序的服务。

-   可以是一个适配层，位于旧协议与面向连接的 NDIS 之间。

    此类适配层使用调用管理服务建立基础连接，但通过它上面的无连接协议隐藏此接口的面向连接的特性。

**注意**  面向连接的客户端的上边缘接口的定义超出了 NDIS 文档的范围。 如果客户端充当适配层，则其上边缘接口由它适应面向连接的 NDIS 的协议定义。

 

有关面向连接的客户端执行的面向连接的操作的摘要，请参阅 [客户端执行的面向连接的操作](connection-oriented-operations-performed-by-clients.md)。

## <a name="related-topics"></a>相关主题


[NDIS 微型端口驱动程序](ndis-miniport-drivers2.md)

 

 






