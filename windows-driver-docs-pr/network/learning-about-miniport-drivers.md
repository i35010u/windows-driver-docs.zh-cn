---
title: 了解微型端口驱动程序
description: 了解微型端口驱动程序
ms.assetid: faaeee13-7d21-4e06-a33c-da249716d925
keywords:
- 无连接驱动程序 WDK 网络
- 面向连接的驱动程序 WDK 网络
- WAN 微型端口驱动程序 WDK 网络
- 微型端口驱动程序 WDK 网络，WAN 微型端口驱动程序
- NDIS 微型端口驱动程序 WDK，WAN 微型端口驱动程序
- 微型端口驱动程序 WDK 网络，具有 WDM 下边缘的微型端口驱动程序
- NDIS 微型端口驱动程序 WDK，具有 WDM 下边缘的微型端口驱动程序
- WDM 低边缘 WDK 网络
- 微型端口驱动程序 WDK 网络，IrDA 微型端口驱动程序
- NDIS 微型端口驱动程序 WDK，IrDA 微型端口驱动程序
- IrDA 驱动程序 WDK 网络
- 微型端口驱动程序 WDK 网络，可缩放的网络支持
- NDIS 微型端口驱动程序 WDK，可缩放的网络支持
- 网络驱动程序 WDK，类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1972946352fc71de78863dcbdbde0a3b29099ce
ms.sourcegitcommit: 29c2e6dd8a3de3c11822d990adf1edd774f8a136
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "91230009"
---
# <a name="learning-about-miniport-drivers"></a>了解微型端口驱动程序





有多种类型的微型端口驱动程序。 以下列表说明了应阅读哪些 WDK 文档部分，具体取决于要编写的微型端口驱动程序的类型：

<a href="" id="connectionless-miniport-drivers"></a>**无连接微型端口驱动程序**  
如果你正在编写一个小型端口驱动程序用于控制网络接口卡 (NIC) 用于无连接网络媒体 (如以太网) ，请阅读：

-   [NDIS 微型端口驱动程序简介](deserialized-ndis-miniport-drivers.md)

-   [NDIS 微型端口驱动程序](./initializing-a-miniport-driver.md)

<a href="" id="connection-oriented-miniport-drivers"></a>**面向连接的微型端口驱动程序**  
如果要为面向连接的网络媒体 (（例如 ISDN) ）编写小型端口驱动程序，请阅读：

-   本主题中前面列出的 "无连接微型端口驱动程序" 的所有部分

-   [面向连接的 NDIS](connection-oriented-ndis.md)

<a href="" id="wan-miniport-drivers"></a>**WAN 微型端口驱动程序**  
如果你正在编写用于控制广域网) NIC (WAN 的微型端口驱动程序，请阅读：

-   本主题中前面列出的 "无连接微型端口驱动程序" 的所有部分

-   [WAN 微型端口驱动程序](wan-miniport-drivers.md)

<a href="" id="miniports-with-a-wdm-lower-interface"></a>**使用 WDM 下接口的微型端口**  
如果你正在编写一个微型端口驱动程序，该驱动程序将接口提供给其他内核驱动程序，并且具有 Microsoft Windows 驱动模型 (WDM) 较低接口，请阅读：

-   本主题中前面列出的 "无连接微型端口驱动程序" 的所有部分

-   [包含 WDM 下接口的微型端口驱动程序](miniport-drivers-with-a-wdm-lower-interface.md)

<a href="" id="irda-miniport-drivers"></a>**IrDA 微型端口驱动程序**  
如果要编写控制 IrDA 适配器的微型端口驱动程序，请阅读：

-   本主题中前面列出的 "无连接微型端口驱动程序" 的所有部分

<a href="" id="miniport-drivers-that-support-scalable-networking"></a>**支持可缩放网络的微型端口驱动程序**  
若要了解支持可缩放网络的微型端口驱动程序，请阅读：

-   [可缩放网络](/windows-hardware/drivers/ddi/_netvista/)

<a href="" id="miniport-drivers-that-support-offloading-tcp-ip--------to-hardware-------"></a>**支持将 TCP/IP 卸载到硬件的微型端口驱动程序**   
若要了解将 TCP/IP 卸载到硬件的微型端口驱动程序，请阅读：

-   [TCP/IP 卸载](tcp-ip-offload.md)

 

