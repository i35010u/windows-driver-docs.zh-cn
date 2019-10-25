---
title: 检查设备对象中的标志
description: 检查设备对象中的标志
ms.assetid: f7bff7b8-bd30-4489-ab3f-ca5ad4d5c1ba
keywords:
- 可移动媒体 WDK 内核，标志检查
- 标志 WDK 可移动介质
- 检查设备对象标志
- 验证设备对象标志
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98602821338a34e34631b36df88d9b2dc80f3af8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837104"
---
# <a name="checking-flags-in-the-device-object"></a>检查设备对象中的标志





对于每个用于向/从可移动媒体请求 i/o 操作的 IRP，可移动媒体设备驱动程序必须确定是否\_验证是否已在**DeviceObject-&gt;标记**中设置\_卷。 如果设置了此值，则驱动程序必须执行以下操作：

-   对于[**irp\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)、 [**irp\_mj\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)和[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求，请检查 SL\_替代\_验证是否已在将驱动程序的[**IO\_堆栈**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的**标志成员标记**\_位置结构。 如果是，则继续执行请求的操作。

    返回有关基础媒体逻辑结构的信息的设备控制请求具有 SL\_重写\_验证当 IFS 装入或逐时，在 i/o 堆栈位置的**Flags**成员中设置\_卷集可移动介质卷。

-   否则，驱动程序必须拒绝为相应的驱动器、设备或分区执行 i/o 请求，\_验证\_卷是否在其**DeviceObject-&gt;的标志**中进行了设置。 可移动媒体驱动程序必须将 Irp 发送到相应的设备，如前一节所述，为每个 IRP 重复步骤3和4，直到 FSD 清除\_验证可移动媒体驱动程序 DeviceObject 中\_卷。 **&gt;标志**。

如果在执行\_验证时，可移动媒体设备驱动程序不会失败，请验证是否已设置\_卷，SL\_重写\_验证是否未为上述传输请求设置\_卷，则文件系统不能维护缓存的文件数据，也不会导致提示用户重新装载保存打开的文件的媒体。

 

 




