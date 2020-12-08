---
title: 打开并行端口
description: 打开并行端口
keywords:
- 供应商提供的并行驱动程序 WDK，并行端口操作
- 系统提供的函数驱动程序 WDK 并行端口
- 函数驱动程序 WDK 并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68727729e1d092a6e1d252d9a37e12217cecb418
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806097"
---
# <a name="operating-a-parallel-port"></a>打开并行端口





本部分介绍客户端（尤其是供应商提供的并行设备函数驱动程序）如何操作并行端口。

系统提供的并行端口函数驱动程序为系统中枚举的每个并行端口 (FDO) 创建一个功能设备对象。 以下主题介绍客户端如何使用端口的 FDO 所提供的接口运行并行端口：

[创建和启动并行端口](creating-and-starting-a-parallel-port.md)

[打开和关闭并行端口](opening-and-closing-a-parallel-port.md)

[获取有关并行端口的信息](obtaining-information-about-a-parallel-port.md)

[同步并行端口的使用](synchronizing-the-use-of-a-parallel-port.md)

[选择和取消选择连接到并行端口的 IEEE 1284 设备](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)

[设置和清除并行端口上的通信模式](setting-and-clearing-the-communication-mode-on-a-parallel-port.md)

[连接到 IEEE 1284.3 数据链路设备](connecting-to-an-ieee-1284-3-data-link-device.md)

[将中断服务例程连接到并行端口](connecting-an-interrupt-service-routine-to-a-parallel-port.md)

有关并行端口系统支持的详细信息，请参阅：

[ParallelPorts 和设备简介](introduction-to-parallel-ports-and-devices.md)

[系统提供的并行驱动程序](system-supplied-parallel-drivers.md)

[System-Supplied 并行驱动程序的客户端接口](/windows-hardware/drivers/ddi/index)

 

