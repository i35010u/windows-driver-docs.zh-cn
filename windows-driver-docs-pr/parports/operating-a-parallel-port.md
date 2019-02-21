---
title: 运行并行端口
description: 运行并行端口
ms.assetid: c9015a01-a7cb-41f4-9710-a868ef19f6d7
keywords:
- 供应商提供并行驱动程序 WDK、 并行端口操作
- 系统提供的函数的驱动程序 WDK 的并行端口
- 功能的驱动程序 WDK 的并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 826f1999e1edfea550c8b96e1dec1a262b3870e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545410"
---
# <a name="operating-a-parallel-port"></a>运行并行端口





本部分介绍的客户端，具体而言，并行设备的供应商提供的函数驱动程序运行的并行端口的方式。

并行端口的系统提供的函数驱动程序创建用于枚举在系统中的每个并行端口的功能的设备对象 (FDO)。 以下主题介绍了客户端通过使用提供的端口的 FDO 界面运行并行端口的方式：

[创建和启动并行端口](creating-and-starting-a-parallel-port.md)

[打开和关闭并行端口](opening-and-closing-a-parallel-port.md)

[获取有关并行端口的信息](obtaining-information-about-a-parallel-port.md)

[同步使用并行端口](synchronizing-the-use-of-a-parallel-port.md)

[选择和取消选择附加到并行端口的 IEEE 1284 设备](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)

[设置和清除并行端口上的通信模式](setting-and-clearing-the-communication-mode-on-a-parallel-port.md)

[连接到 IEEE 1284.3 数据链接设备](connecting-to-an-ieee-1284-3-data-link-device.md)

[连接到并行端口中断服务例程](connecting-an-interrupt-service-routine-to-a-parallel-port.md)

有关系统支持并行端口的详细信息，请参阅：

[ParallelPorts 和设备简介](introduction-to-parallel-ports-and-devices.md)

[系统提供并行的驱动程序](system-supplied-parallel-drivers.md)

[系统提供并行的驱动程序的客户端接口](https://msdn.microsoft.com/library/windows/hardware/ff543926)

 

 




