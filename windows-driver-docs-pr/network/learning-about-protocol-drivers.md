---
title: 了解协议驱动程序
description: 了解协议驱动程序
keywords:
- 协议驱动程序 WDK 网络，无连接的下边缘
- NDIS 协议驱动程序 WDK，无连接的下边缘
- 协议驱动程序 WDK 网络、面向连接的客户端和提供程序
- NDIS 协议驱动程序 WDK、面向连接的客户端和提供程序
- 协议驱动程序 WDK 网络，Winsock 支持
- NDIS 协议驱动程序 WDK，Winsock 支持
- Winsock 内核 WDK 网络，对 Winsock 的协议驱动程序支持
- 网络驱动程序 WDK，类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 302a3018c9767938943cf6d37dbc339b60fb3346
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789703"
---
# <a name="learning-about-protocol-drivers"></a>了解协议驱动程序





您可以编写一个协议驱动程序，该驱动程序具有无连接或面向连接的下边缘。 此外，你的协议驱动程序还可以提供 Winsock 支持。 以下列表说明了应阅读哪些 WDK 文档部分，具体取决于要编写的协议驱动程序的类型：

<a href="" id="protocol-drivers-that-have-a-connectionless-lower-edge"></a>**具有无连接下边缘的协议驱动程序**  
如果你正在编写一个协议驱动程序，其下边缘提供连接到无连接微型端口驱动程序的接口，请阅读：

-   [NDIS 协议驱动程序](./roadmap-for-developing-ndis-protocol-drivers.md)

<a href="" id="protocol-drivers-that-are-connection-oriented-clients-or-that-are-connection-oriented-providers-of--------call-manager-services"></a>**协议驱动程序是面向连接的客户端，或者是呼叫管理器服务的面向连接的提供商**  
如果你正在编写面向连接的小型端口驱动程序接口的面向连接的客户端，或者如果你要编写面向连接的调用管理器，请阅读：

-   [NDIS 协议驱动程序](./roadmap-for-developing-ndis-protocol-drivers.md)

-   [面向连接的 NDIS](connection-oriented-ndis.md)

<a href="" id="protocol-drivers-that-have-winsock-support"></a>**支持 Winsock 的协议驱动程序**  
如果你正在编写提供 Winsock 支持的协议，请阅读：

-   [NDIS 协议驱动程序](./roadmap-for-developing-ndis-protocol-drivers.md)

-   [Windows 套接字的传输帮助程序 Dll](/previous-versions/windows/hardware/network/ff565691(v=vs.85))

 

