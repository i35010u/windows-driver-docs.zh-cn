---
title: 文件系统筛选器驱动程序与设备驱动程序的类似程度如何
description: 文件系统筛选器驱动程序与设备驱动程序的类似程度如何
ms.assetid: 7797239e-e0cc-4422-bcc6-31cfe6efd8e4
keywords:
- 筛选器驱动程序 WDK 文件系统和设备驱动程序
- 文件系统筛选器驱动程序（WDK）和设备驱动程序
- 设备驱动程序 WDK 文件系统
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8350bd322e894b589127aa4a732da7cc4e2f191f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063332"
---
# <a name="how-file-system-filter-drivers-are-similar-to-device-drivers"></a>文件系统筛选器驱动程序与设备驱动程序的类似程度如何

Microsoft Windows 操作系统中的文件系统筛选器驱动程序和设备驱动程序类似于以下方式：

- **类似结构**

  与设备驱动程序一样，文件系统筛选器驱动程序具有 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)、 [调度](../kernel/writing-dispatch-routines.md)和 [i/o 完成](../kernel/using-iocompletion-routines.md) 例程。 它们调用设备驱动程序调用的许多相同内核模式例程，并筛选设备的 i/o 请求 (即与它们关联的文件系统卷) 。

- **类似的功能**

  - 由于文件系统筛选器驱动程序和设备驱动程序是 i/o 系统的一部分，因此它们都 (Irp) 接收 [i/o 请求数据包](../kernel/packet-driven-i-o-with-reusable-irps.md) ，并对它们进行操作。

  - 与设备驱动程序一样，文件系统筛选器驱动程序还可以创建自己的 Irp，并将其发送到较低级别的驱动程序。

  - 两种类型的驱动程序都可以通过使用回调函数) 各种系统事件来注册通知 (。

- **其他相似性**

  - 与设备驱动程序一样，文件系统筛选器驱动程序可以接收 [I/o 控制代码简介](../kernel/introduction-to-i-o-control-codes.md) (IOCTLs) 。 请注意，文件系统筛选器驱动程序还可以接收并定义 [文件系统控制代码](/windows-hardware/drivers/ddi/index) (FSCTLs) 。

  - 与设备驱动程序一样，文件系统筛选器驱动程序可以配置为在系统启动时加载，或在系统启动过程完成后再加载。