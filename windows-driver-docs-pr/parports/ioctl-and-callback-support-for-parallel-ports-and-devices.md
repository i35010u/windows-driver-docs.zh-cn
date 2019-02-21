---
title: IOCTL 和并行端口和设备的回调支持
description: IOCTL 和并行端口和设备的回调支持
ms.assetid: 72a31f50-2f59-4a4d-aac7-571f83a94259
keywords:
- 系统提供并行的驱动程序 WDK Ioctl
- Ioctl WDK 并行驱动程序
- 回调 WDK 并行驱动程序
- 系统提供并行驱动程序 WDK，回调
- 并行设备 WDK，回调
- 并行设备 WDK，Ioctl
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8d707bbd2b70b5af8ce580c5ba9ab489eceff6d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524510"
---
# <a name="ioctl-and-callback-support-for-parallel-ports-and-devices"></a>IOCTL 和并行端口和设备的回调支持





本部分提供指向介绍系统提供的并行驱动程序如何支持操作系统的并行端口和设备连接到并行端口的主题。

供应商的并行连接到并行端口的设备功能的驱动程序是可选的。 系统提供的并行驱动程序提供广泛支持用于直接控制为原始的设备，并行设备和操作系统的设备的父并行端口。

有关信息系统提供的函数驱动程序提供了 Ioctl 和回调执行并行端口，请参阅以下主题：

[获取有关并行端口的信息](obtaining-information-about-a-parallel-port.md)

[同步使用并行端口](synchronizing-the-use-of-a-parallel-port.md)

[选择和取消选择附加到并行端口的 IEEE 1284 设备](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)

[设置和清除并行端口上的通信模式](setting-and-clearing-the-communication-mode-on-a-parallel-port.md)

[连接到 IEEE 1284.3 数据链接设备](connecting-to-an-ieee-1284-3-data-link-device.md)

有关 Ioctl 和回调系统提供总线驱动程序提供的用于运行并行设备附加到并行端口的信息，请参阅：

[打开并使用并行设备](opening-and-using-a-parallel-device.md)

[连接到并行的设备](connecting-to-a-parallel-device.md)

[获取有关并行的设备的信息](obtaining-information-about-a-parallel-device.md)

[锁定和解锁并行端口以供并行设备](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

[设置和清除并行设备的通信模式](setting-and-clearing-a-communication-mode-for-a-parallel-device.md)

[并行的设备上设置属性](setting-attributes-on-a-parallel-device.md)

[读取和写入并行设备](reading-and-writing-a-parallel-device.md)

有关如何运行的并行端口和设备连接到并行端口的详细信息，请参阅：

[运行并行端口](operating-a-parallel-port.md)

[运行并行设备附加到并行端口](operating-a-parallel-device-attached-to-a-parallel-port.md)

[系统提供并行的驱动程序的客户端接口](https://msdn.microsoft.com/library/windows/hardware/ff543926)

 

 




