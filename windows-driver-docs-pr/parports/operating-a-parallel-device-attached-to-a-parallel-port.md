---
title: 打开连接到并行端口的并行设备
description: 打开连接到并行端口的并行设备
ms.assetid: 5ad36162-efbe-4be8-954c-964ef12c539a
keywords:
- 并行端口 WDK，并行设备操作
- 并行设备 WDK
- 供应商提供的并行驱动程序 WDK，并行设备操作
- 并行设备 WDK，客户端操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a36e1566045bbb7b3712520c02cf7e839429bcb
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382703"
---
# <a name="operating-a-parallel-device-attached-to-a-parallel-port"></a>打开连接到并行端口的并行设备





本部分描述了客户端（尤其是供应商为并行设备提供的函数驱动程序）如何操作连接到并行端口的并行设备。

系统提供的并行端口总线驱动程序为在并行端口上枚举的每个并行设备创建 (PDO) 的物理设备对象。 以下主题介绍客户端如何使用设备 PDO 提供的接口操作并行设备：

[打开和使用并行设备](opening-and-using-a-parallel-device.md)

[连接到并行设备](connecting-to-a-parallel-device.md)

[获取有关并行设备的信息](obtaining-information-about-a-parallel-device.md)

[锁定和解锁供并行设备使用的并行端口](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

[设置和清除并行设备的通信模式](setting-and-clearing-a-communication-mode-for-a-parallel-device.md)

[在并行设备上设置属性](setting-attributes-on-a-parallel-device.md)

[向并行设备进行读取和写入](reading-and-writing-a-parallel-device.md)

有关连接到并行端口的并行设备支持的详细信息，请参阅：

[ParallelPorts 和设备简介](introduction-to-parallel-ports-and-devices.md)

[系统提供的并行驱动程序](system-supplied-parallel-drivers.md)

[系统提供的并行驱动程序的客户端接口](/windows-hardware/drivers/ddi/index)

 

