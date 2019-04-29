---
title: 面向连接的环境
description: 面向连接的环境
ms.assetid: 596d7d74-ad9d-40da-b483-3afc0e333f98
keywords:
- 面向连接的 NDIS WDK 环境
- CoNDIS WDK 网络、 环境
- 面向连接的 NDIS WDK，微型端口驱动程序
- CoNDIS WDK 网络、 微型端口驱动程序
- 微型端口驱动程序 WDK 网络的 CoNDIS
- 面向连接的 NDIS WDK，调用管理器
- CoNDIS WDK 网络、 调用管理器
- 调用管理器 WDK 网络、 面向连接的操作
- 面向连接的 NDIS WDK，MCM 驱动程序
- CoNDIS WDK 网络、 MCM 驱动程序
- MCM 驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38c3fbdb7ed895138cb0c005984f23aae82cbe59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357450"
---
# <a name="connection-oriented-environment"></a>面向连接的环境





NDIS 支持以下面向连接的驱动程序：

-   面向连接的客户端

-   呼叫管理器

-   集成的微型端口调用管理器 (MCM) 驱动程序

-   面向连接的微型端口驱动程序

下图显示了面向连接的客户端、 调用 manager 和微型端口驱动程序的配置。

![说明的面向连接的客户端、 调用 manager 和微型端口驱动程序配置的关系图](images/conormed.png)

下图显示了面向连接的客户端和集成的 MCM 驱动程序的配置。

![使用集成的 mcm 驱动程序的面向连接的环境](images/conorcli.png)

一个*面向连接的微型端口驱动程序*控制一个或多个网络接口卡 (Nic)，并提供面向连接的协议驱动程序 （面向连接的客户端和调用管理器） 和 NIC 之间的接口硬件。

通过面向连接的微型端口驱动程序执行的面向连接的操作的摘要，请参阅[Connection-Oriented 微型端口驱动程序执行的操作](connection-oriented-operations-performed-by-miniport-drivers.md)。

一个*呼叫管理器*NDIS 协议驱动程序，它提供调用安装程序和面向连接的客户端的关闭的服务。 呼叫管理器中：

-   使用发送和接收的面向连接的微型端口驱动程序功能，以与网络实体，例如网络交换机或远程对等节点的信号消息交换。

-   支持一个或多个信号协议驱动程序。 由呼叫管理器执行的面向连接的操作的摘要，请参阅[Connection-Oriented 调用管理器执行的操作](connection-oriented-operations-performed-by-call-managers.md)。

*MCM 的集成驱动程序*是面向连接的微型端口驱动程序，还向面向连接的客户端提供调用管理器服务。 MCM 驱动程序具有以下特征：

-   MCM 驱动程序与面向连接的微型端口驱动程序; 配对呼叫管理器作为向客户端提供相同的面向连接的服务但是，调用管理器微型端口驱动程序接口是驱动程序的内部，因此不透明的 NDIS。

-   多个调用管理器和 MCM 驱动程序可以在同一环境中共存。

-   每个呼叫管理器或 MCM 驱动程序可以支持多个信号协议驱动程序。

MCM 驱动程序和调用管理器的详细比较，请参阅[MCM 驱动程序与的区别的 Call Manager](mcm-drivers-vs--call-managers.md)。

一个*面向连接的客户端*:

-   使用调用安装程序和呼叫管理器或 MCM 驱动程序的关闭服务。

-   使用发送和接收的面向连接的微型端口驱动程序或可发送和接收数据的 MCM 驱动程序的功能。

-   可以提供其自己网络和传输层服务添加到在其上边缘的更高层的应用程序。

-   使用呼叫管理器和面向连接的微型端口驱动程序，或它的服务在其上边缘使用 MCM 驱动程序的服务。

-   可以进行适配层，位于旧协议与面向连接的 NDIS 之间。

    此类适配层使用从上面的无连接协议调用管理服务以建立但隐藏基础连接此接口的面向连接的性质。

**请注意**  面向连接的客户端的上边缘接口的定义不在 NDIS 文档的讨论范围。 如果客户端充当适配层，其上边缘接口定义适应面向连接的 NDIS 的协议。

 

有关执行的面向连接的客户端的面向连接的操作的摘要，请参阅[Connection-Oriented 的客户端执行的操作](connection-oriented-operations-performed-by-clients.md)。

## <a name="related-topics"></a>相关主题


[NDIS 微型端口驱动程序](ndis-miniport-drivers2.md)

 

 






