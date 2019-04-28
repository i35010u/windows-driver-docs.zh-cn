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
ms.openlocfilehash: 8a18fbb363181d3199418d64f441f62103aedc7f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343724"
---
# <a name="checking-flags-in-the-device-object"></a>检查设备对象中的标志





对于每个请求的 I/O 操作向/从可移动介质的 IRP，可移动介质设备驱动程序必须确定是否执行\_验证\_卷已设置其**DeviceObject-&gt;标志**。 如果设置此值，该驱动程序必须执行以下操作：

-   有关[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)， [ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)，和[**IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744)请求，检查是否 SL\_重写\_验证\_中设置卷**标志**驱动程序的成员[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)结构。 如果是，继续请求的操作。

    返回有关基础媒体的逻辑结构的信息的设备控制请求具有 SL\_重写\_验证\_卷在 I/O 堆栈位置设置**标志**成员时IFS 装载或逐可移动介质卷。

-   否则，该驱动程序必须拒绝执行相应的驱动器、 设备或分区时执行操作的 I/O 请求\_验证\_卷中设置其**DeviceObject-&gt;标志**。 可移动媒体驱动程序时不能重复步骤 3 和 4 为每个 IRP FSD 清除之前执行的操作发送到相应的设备，如在上一小节中所述的 Irp\_验证\_可移动媒体驱动中的卷**DeviceObject-&gt;标志**。

如果可移动介质设备驱动程序不会失败 Irp 执行操作时\_验证\_卷是组和 SL\_重写\_验证\_卷未设置为前面的传输请求，文件系统可以不维护的缓存的文件数据的完整性也不会使用户，会提示您重新装载保留打开的文件的介质。

 

 




