---
title: 检查设备对象中的标志
description: 检查设备对象中的标志
ms.assetid: f7bff7b8-bd30-4489-ab3f-ca5ad4d5c1ba
keywords:
- 可移动媒体 WDK 内核，检查标志
- 标志 WDK 可移动媒体
- 检查设备对象标志
- 验证设备对象标志
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ea3cea627c87b24ef8c4bffb6d5b24a85deedcc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383366"
---
# <a name="checking-flags-in-the-device-object"></a>检查设备对象中的标志





对于每个请求的 I/O 操作向/从可移动介质的 IRP，可移动介质设备驱动程序必须确定是否执行\_验证\_卷已设置其**DeviceObject-&gt;标志**。 如果设置此值，该驱动程序必须执行以下操作：

-   有关[ **IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)， [ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)，和[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求，检查是否 SL\_重写\_验证\_中设置卷**标志**驱动程序的成员[ **IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)结构。 如果是，继续请求的操作。

    返回有关基础媒体的逻辑结构的信息的设备控制请求具有 SL\_重写\_验证\_卷在 I/O 堆栈位置设置**标志**成员时IFS 装载或逐可移动介质卷。

-   否则，该驱动程序必须拒绝执行相应的驱动器、 设备或分区时执行操作的 I/O 请求\_验证\_卷中设置其**DeviceObject-&gt;标志**。 可移动媒体驱动程序时不能重复步骤 3 和 4 为每个 IRP FSD 清除之前执行的操作发送到相应的设备，如在上一小节中所述的 Irp\_验证\_可移动媒体驱动中的卷**DeviceObject-&gt;标志**。

如果可移动介质设备驱动程序不会失败 Irp 执行操作时\_验证\_卷是组和 SL\_重写\_验证\_卷未设置为前面的传输请求，文件系统可以不维护的缓存的文件数据的完整性也不会使用户，会提示您重新装载保留打开的文件的介质。

 

 




