---
title: 了解协议驱动程序
description: 了解协议驱动程序
ms.assetid: a908f91e-7529-42b5-9a3d-82d2a519d969
keywords:
- 协议驱动程序 WDK 网络连接、 无连接下边缘
- NDIS 协议驱动程序 WDK，无连接的下边缘
- 协议驱动程序 WDK 网络、 面向连接的客户端和提供程序
- NDIS 协议驱动程序 WDK、 面向连接的客户端和提供程序
- 协议驱动程序 WDK 网络 Winsock 支持
- NDIS 协议驱动程序 WDK、 Winsock 支持
- 网络、 Winsock 内核 WDK Winsock 协议驱动程序支持
- 网络驱动程序 WDK，类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddb35995bb4b84f133aae42b8c8e0b9a58be812f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356221"
---
# <a name="learning-about-protocol-drivers"></a>了解协议驱动程序





您可以编写无连接或面向连接的下边缘的协议驱动程序。 此外，协议驱动程序可以提供 Winsock 支持。 以下列表描述了 WDK 文档中的哪些部分，应，具体取决于你正在编写的协议驱动程序的类型：

<a href="" id="protocol-drivers-that-have-a-connectionless-lower-edge"></a>**有无连接的下边缘的协议驱动程序**  
如果你正在编写的下边缘提供无连接的微型端口驱动程序的接口协议驱动程序，请阅读：

-   [协议的 NDIS 驱动程序](ndis-protocol-drivers.md)

<a href="" id="protocol-drivers-that-are-connection-oriented-clients-or-that-are-connection-oriented-providers-of--------call-manager-services"></a>**协议驱动程序是面向连接的客户端或调用管理器服务的面向连接的提供商**  
如果你正在编写的面向连接的客户端提供面向连接的微型端口驱动程序的接口，或者如果你正在编写面向连接的调用管理器中，读取：

-   [协议的 NDIS 驱动程序](ndis-protocol-drivers.md)

-   [面向连接的 NDIS](connection-oriented-ndis.md)

<a href="" id="protocol-drivers-that-have-winsock-support"></a>**Winsock 支持的协议驱动程序**  
如果你正在编写一种协议，提供了 Winsock 支持，请阅读：

-   [协议的 NDIS 驱动程序](ndis-protocol-drivers.md)

-   [Windows 套接字传输帮助程序 Dll](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565691(v=vs.85))

 

 





