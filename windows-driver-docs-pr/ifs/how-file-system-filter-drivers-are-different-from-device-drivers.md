---
title: 文件系统筛选器驱动程序与设备驱动程序的差异在哪里
description: 文件系统筛选器驱动程序与设备驱动程序的差异在哪里
ms.assetid: 64a59564-a4d7-4174-82d3-60bd1a30b2d8
keywords:
- 筛选器驱动程序 WDK 文件系统和设备驱动程序
- 文件系统筛选器驱动程序（WDK）和设备驱动程序
- 设备驱动程序 WDK 文件系统
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: a187ba6b9cf1305a5e6a59daeed67abba189704c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063334"
---
# <a name="how-file-system-filter-drivers-are-different-from-device-drivers"></a>文件系统筛选器驱动程序与设备驱动程序的差异在哪里

Microsoft Windows 操作系统中的文件系统筛选器驱动程序和设备驱动程序在以下方面有所不同：

- **无电源管理**

  由于文件系统筛选器驱动程序不是设备驱动程序，因此不会直接控制硬件设备，它们不会接收 [**IRP \_ MJ \_ 电源**](../kernel/irp-mj-power.md) 请求。 相反，电源 Irp 会直接发送到存储设备堆栈。 但在极少数情况下，文件系统筛选器驱动程序可能会干扰电源管理。 出于此原因，文件系统筛选器驱动程序不应 \_ \_ 在 **DriverEntry** 例程中为 IRP MJ 功能注册调度例程，并且它们不应调用 [PoXxx](/windows-hardware/drivers/ddi/index) 例程。

- **无 WDM**

  文件系统筛选器驱动程序不能 (WDM) 驱动程序上 Windows 驱动模型。 Microsoft [Windows 驱动模型](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model) 仅适用于设备驱动程序。

- **无 AddDevice 或 StartIo**

  由于文件系统筛选器驱动程序不是设备驱动程序，因此不会直接控制硬件设备，它们不应具有 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 或 [**StartIo**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程。

- **已创建不同的设备对象**

  尽管文件系统筛选器驱动程序和设备驱动程序都创建设备对象，但它们在创建的设备对象的数量和种类上有所不同。

  设备驱动程序创建物理和功能设备对象来表示设备。 即插即用 (PnP) Manager 构建并维护一个全局设备树，其中包含设备驱动程序创建的所有设备对象。 文件系统筛选器驱动程序创建的设备对象不包含在此设备树中。

  文件系统筛选器驱动程序不创建物理或功能设备对象。 而是创建控制设备对象并筛选设备对象。 *控制设备对象*表示系统和用户模式应用程序的筛选器驱动程序。 *筛选器设备对象*执行筛选特定文件系统或卷的实际工作。 文件系统筛选器驱动程序通常会创建一个控制设备对象和一个或多个筛选器设备对象。

- **其他差异**

  - 因为文件系统筛选器驱动程序不是设备驱动程序，所以它们不 [ (DMA) 执行直接内存访问 ](../kernel/using-direct-i-o-with-dma.md)。

  - 不同于设备筛选器驱动程序（可附加在目标设备的功能驱动程序之上或之下），文件系统筛选器驱动程序只能附加在目标文件系统驱动程序之上。 因此，在设备驱动程序条款中，文件系统筛选器驱动程序只能是上限筛选器，而不能是较低的筛选器。