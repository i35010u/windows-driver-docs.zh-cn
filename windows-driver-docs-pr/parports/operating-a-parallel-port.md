---
title: 打开并行端口
description: 打开并行端口
ms.assetid: c9015a01-a7cb-41f4-9710-a868ef19f6d7
keywords:
- 供应商提供的并行驱动程序 WDK，并行端口操作
- 系统提供的函数驱动程序 WDK 并行端口
- 函数驱动程序 WDK 并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 994070744393cc3ed89e463336f947277367415d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842737"
---
# <a name="operating-a-parallel-port"></a>打开并行端口





本部分介绍客户端（尤其是供应商提供的并行设备函数驱动程序）如何操作并行端口。

系统提供的并行端口函数驱动程序为系统中枚举的每个并行端口创建一个功能设备对象（FDO）。 以下主题介绍客户端如何使用端口的 FDO 所提供的接口运行并行端口：

[创建和启动并行端口](creating-and-starting-a-parallel-port.md)

[打开并关闭并行端口](opening-and-closing-a-parallel-port.md)

[获取有关并行端口的信息](obtaining-information-about-a-parallel-port.md)

[同步使用并行端口](synchronizing-the-use-of-a-parallel-port.md)

[选择并取消选择附加到并行端口的 IEEE 1284 设备](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)

[设置和清除并行端口上的通信模式](setting-and-clearing-the-communication-mode-on-a-parallel-port.md)

[连接到 IEEE 1284.3 数据链路设备](connecting-to-an-ieee-1284-3-data-link-device.md)

[将中断服务例程连接到并行端口](connecting-an-interrupt-service-routine-to-a-parallel-port.md)

有关并行端口系统支持的详细信息，请参阅：

[ParallelPorts 和设备简介](introduction-to-parallel-ports-and-devices.md)

[系统提供的并行驱动程序](system-supplied-parallel-drivers.md)

[系统提供的并行驱动程序的客户端接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

 

 




