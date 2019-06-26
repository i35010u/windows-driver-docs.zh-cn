---
title: 打开连接到并行端口的并行设备
description: 打开连接到并行端口的并行设备
ms.assetid: 5ad36162-efbe-4be8-954c-964ef12c539a
keywords:
- 并行端口 WDK，并行设备操作
- 并行设备 WDK
- 供应商提供并行驱动程序 WDK，并行设备操作
- 并行设备 WDK，客户端操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34873e3d44f3ad5ea96fa952b28be414a9aef6b8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358504"
---
# <a name="operating-a-parallel-device-attached-to-a-parallel-port"></a>打开连接到并行端口的并行设备





本部分介绍的客户端，具体而言，并行设备的供应商提供的函数驱动程序的运行方式连接到并行端口的并行设备。

并行端口的系统提供的总线驱动程序创建并行端口上枚举每个并行设备的物理设备对象 (PDO)。 以下主题介绍了客户端通过使用提供的设备的 PDO 界面运行并行设备的方式：

[打开并使用并行设备](opening-and-using-a-parallel-device.md)

[连接到并行的设备](connecting-to-a-parallel-device.md)

[获取有关并行的设备的信息](obtaining-information-about-a-parallel-device.md)

[锁定和解锁并行端口以供并行设备](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

[设置和清除并行设备的通信模式](setting-and-clearing-a-communication-mode-for-a-parallel-device.md)

[并行的设备上设置属性](setting-attributes-on-a-parallel-device.md)

[读取和写入并行设备](reading-and-writing-a-parallel-device.md)

有关支持并行设备附加到并行端口的详细信息，请参阅：

[ParallelPorts 和设备简介](introduction-to-parallel-ports-and-devices.md)

[系统提供的并行驱动程序](system-supplied-parallel-drivers.md)

[系统提供并行的驱动程序的客户端接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

 

 




