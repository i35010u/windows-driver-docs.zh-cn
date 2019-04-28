---
title: 动态硬件分区体系结构
description: 动态硬件分区体系结构
ms.assetid: 1b6a1dc5-ec32-4bb9-acaf-14db284b4a0e
keywords:
- 动态硬件分区 WDK，体系结构
- 硬件分区 WDK 动态的体系结构
- 分区 WDK 动态硬件，体系结构
- 体系结构 WDK 动态硬件分区
- 动态可分区服务器 WDK
- 服务器 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57366470ad89d8305ad0958c1530c7ea671e4da7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341479"
---
# <a name="dynamic-hardware-partitioning-architecture"></a>动态硬件分区体系结构


硬件可分区服务器可以配置到一个或多个独立的硬件分区。 硬件分区包含一个或多个分区单元。 分区单位可以是一个处理器、 内存模块或 I/O 主桥。

下图显示了硬件可分区服务器的一个示例。

![说明硬件可分区服务器的关系图](images/dhparch.gif)

在上图中，服务器具有 12 个分区单元总数： 四个内存模块、 四个处理器模块和四个 I/O 主机桥模块。 每个分区单位被分配给一个三个硬件分区。 每个硬件分区是完全独立于其他硬件分区。 服务处理器负责硬件分区的配置。 它控制的映射到硬件分区的分区单元，并创建硬件分区之间的隔离。

从 Windows Server 2008 开始，每个分区单元被视为插 (PnP) 设备。 由于这些设备是即插即用，因此您可以在操作系统启动后添加它们。

有关如何将设备驱动程序可以向注册其自身操作系统到硬件分区以动态方式添加的分区单元时接收通知的详细信息，请参阅[驱动程序通知](driver-notification.md)。

有关应用程序如何可以注册其自身与操作系统的分区单元以动态方式添加到硬件分区时接收通知的详细信息，请参阅[应用程序通知](application-notification.md)。

 

 




