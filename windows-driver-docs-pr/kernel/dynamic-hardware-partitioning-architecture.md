---
title: 动态硬件分区体系结构
description: 动态硬件分区体系结构
ms.assetid: 1b6a1dc5-ec32-4bb9-acaf-14db284b4a0e
keywords:
- 动态硬件分区 WDK，体系结构
- 硬件分区 WDK 动态，体系结构
- 将 WDK 动态硬件分区分区
- 体系结构 WDK 动态硬件分区
- 动态分区服务器 WDK
- 服务器 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7154d74696036e0ba4411f0135ca2601337cd79
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403274"
---
# <a name="dynamic-hardware-partitioning-architecture"></a>动态硬件分区体系结构


硬件分区服务器可以配置为一个或多个独立的硬件分区。 硬件分区由一个或多个分区单位组成。 分区单位可以是处理器、内存模块或 i/o 主机桥。

下图显示了硬件分区服务器的示例。

![阐释硬件分区服务器的示意图](images/dhparch.gif)

在上图中，服务器总共有12个分区单元：四个内存模块、四个处理器模块和四个 i/o 主机桥接模块。 其中每个分区单位都分配给三个硬件分区之一。 每个硬件分区都与其他硬件分区完全隔离。 服务处理器负责配置硬件分区。 它控制分区单元到硬件分区的映射，并在硬件分区之间创建隔离。

从 Windows Server 2008 开始，每个分区单元被视为即插即用 (PnP) 设备。 由于这些设备是 PnP 设备，因此可以在操作系统启动后添加它们。

有关设备驱动程序如何向操作系统注册自身以接收通知的详细信息，请参阅 [驱动程序通知](introduction-to-driver-notification.md)。

有关在将分区单元动态添加到硬件分区时，应用程序如何向操作系统注册其自身以接收通知的详细信息，请参阅 [应用程序通知](introduction-to-application-notification.md)。

 

 




