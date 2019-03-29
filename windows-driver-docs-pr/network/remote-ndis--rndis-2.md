---
title: 远程 NDIS (RNDIS)
description: 远程 NDIS (RNDIS)
ms.assetid: 857cec9c-6098-4fd3-9528-fa592da997f4
keywords:
- 远程 NDIS WDK 网络
- 远程 NDIS 网络驱动程序 WDK，
- RNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc549cad806a7863478d06a1c728d0c580912bbb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565818"
---
# <a name="remote-ndis-rndis"></a>远程 NDIS (RNDIS)





远程 NDIS (RNDIS) 是 USB，如动态插 (PnP) 总线上的以太网 (802.3) 网络设备的总线无关的类规范 1394、 蓝牙和 InfiniBand。 远程 NDIS 定义抽象的控制和数据通道通过主计算机和远程 NDIS 设备之间独立于总线的消息协议。 远程 NDIS 是不够精确，以允许对远程 NDIS 设备的供应商无关的类驱动程序支持在主计算机上。

从 Windows XP 的 Microsoft Windows 版本包括 USB 设备的远程 NDIS 驱动程序。 若要使用 USB 设备使用此驱动程序，IHV 必须提供遵循中的模板的 INF 文件[远程 NDIS INF 模板](remote-ndis-inf-template.md)。

从主机中，远程 NDIS 消息发送到远程 NDIS 设备和远程 NDIS 设备会使用相应的完成消息进行响应。 消息还会在未经请求的方式从远程 NDIS 设备到主机。

本部分包括：

[远程 NDIS (RNDIS) 的概述](overview-of-remote-ndis--rndis-.md)

[远程 NDIS 通信](remote-ndis-communication.md)

[远程 NDIS 到 USB 的映射](remote-ndis-to-usb-mapping.md)


 

 





