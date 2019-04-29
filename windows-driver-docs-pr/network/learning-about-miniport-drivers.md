---
title: 了解微型端口驱动程序
description: 了解微型端口驱动程序
ms.assetid: faaeee13-7d21-4e06-a33c-da249716d925
keywords:
- 无连接驱动程序 WDK 网络
- 面向连接的驱动程序 WDK 网络
- WAN 微型端口驱动程序 WDK 网络
- 微型端口驱动程序 WDK 网络连接、 WAN 微型端口驱动程序
- NDIS 微型端口驱动程序 WDK、 WAN 微型端口驱动程序
- 微型端口驱动程序 WDK 网络具有 WDM 下边缘的微型端口驱动程序
- NDIS 微型端口驱动程序 WDK，微型端口驱动程序使用 WDM 降低边缘
- WDM 较低的边缘 WDK 网络
- 微型端口驱动程序 WDK 网络 IrDA 微型端口驱动程序
- NDIS 微型端口驱动程序 WDK，IrDA 微型端口驱动程序
- IrDA 驱动程序 WDK 网络
- 微型端口驱动程序 WDK 网络连接、 可缩放网络支持
- NDIS 微型端口驱动程序 WDK、 可缩放的网络支持
- 网络驱动程序 WDK，类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1384d03543b91995b46f11e04e7dac9032366573
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365368"
---
# <a name="learning-about-miniport-drivers"></a>了解微型端口驱动程序





有几种类型的微型端口驱动程序。 以下列表描述了 WDK 文档中的哪些部分，应，具体取决于你正在编写的微型端口驱动程序的类型：

<a href="" id="connectionless-miniport-drivers"></a>**无连接的微型端口驱动程序**  
如果你正在编写控制无连接网络媒体 （如以太网） 网络接口卡 (NIC) 的微型端口驱动程序，请阅读：

-   [NDIS 微型端口驱动程序简介](introduction-to-ndis-miniport-drivers.md)

-   [NDIS 微型端口驱动程序](writing-ndis-miniport-drivers.md)

<a href="" id="connection-oriented-miniport-drivers"></a>**面向连接的微型端口驱动程序**  
如果你正在编写面向连接的网络媒体 （例如 ISDN) 的微型端口驱动程序，请阅读：

-   所有在"无连接的微型端口驱动程序"下，本主题前面列出的部分

-   [面向连接的 NDIS](connection-oriented-ndis.md)

<a href="" id="wan-miniport-drivers"></a>**WAN 微型端口驱动程序**  
如果你正在编写控制广域网 (WAN) NIC 的微型端口驱动程序，请阅读：

-   所有在"无连接的微型端口驱动程序"下，本主题前面列出的部分

-   [WAN 微型端口驱动程序](wan-miniport-drivers.md)

<a href="" id="miniports-with-a-wdm-lower-interface"></a>**使用 WDM 低界面的微型端口**  
如果你正在编写的其他内核驱动程序将接口和 Microsoft Windows 驱动程序模型 (WDM) 较低界面的微型端口驱动程序，请阅读：

-   所有在"无连接的微型端口驱动程序"下，本主题前面列出的部分

-   [微型端口驱动程序使用 WDM 降低接口](miniport-drivers-with-a-wdm-lower-interface.md)

<a href="" id="irda-miniport-drivers"></a>**IrDA 微型端口驱动程序**  
如果你正在编写控制 IrDA 适配器的微型端口驱动程序，请阅读：

-   所有在"无连接的微型端口驱动程序"下，本主题前面列出的部分

<a href="" id="miniport-drivers-that-support-scalable-networking"></a>**支持可缩放的网络的微型端口驱动程序**  
若要了解有关支持可缩放的网络的微型端口驱动程序的信息，请阅读：

-   [可缩放网络](https://msdn.microsoft.com/library/windows/hardware/ff570735)

<a href="" id="miniport-drivers-that-support-offloading-tcp-ip--------to-hardware-------"></a>**支持卸载到硬件的 TCP/IP 的微型端口驱动程序**   
若要了解有关将 TCP/IP 卸载到硬件的微型端口驱动程序的信息，请阅读：

-   [TCP/IP 卸载](tcp-ip-offload.md)

 

 





