---
title: 对存储驱动程序中的可分页代码的限制
description: 对存储驱动程序中的可分页代码的限制
ms.assetid: 1958f22f-5563-41e9-9c3f-dec8a4ac80c0
keywords:
- 存储驱动程序 WDK，代码可分页限制
- 可分页代码限制 WDK 存储
- 死锁 WDK 存储
- 分页路径 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3515a0b9e1a9f87df9679fd1dd1ad0430018aac4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373195"
---
# <a name="restrictions-on-pageable-code-in-storage-drivers"></a>对存储驱动程序中的可分页代码的限制


## <span id="ddk_restrictions_on_pageable_code_in_storage_drivers_kg"></span><span id="DDK_RESTRICTIONS_ON_PAGEABLE_CODE_IN_STORAGE_DRIVERS_KG"></span>


若要防止死锁，到服务使用的存储驱动程序的任何部分读取或写入请求应具有可分页的代码中，也不应不断尝试访问可分页的内存。 这是因为在驱动程序[ **DispatchRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)并[ **DispatchWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程可以调用在 IRQL&gt;被动\_级别和在分页 I/O 服务页错误发生在 IRQL = APC\_级别。

类似的规则适用于存储驱动程序的设备控制调度例程[ **DispatchDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)，具有某些限制。 存储驱动程序的设备控制调度例程不能包含可分页的代码或访问可分页内存。 调度例程必须能够接收 IOCTL 请求适用于任意于 Irql 在其他驱动程序并将它们传递关闭驱动程序堆栈。 驱动程序*必须*堆栈的下层的所有未处理的 IOCTL 请求传递而无需更改的 IRQL 或请求的上下文。

但是，Microsoft 需要的所有*存储*IOCTL 请求提交在被动\_级别，因此虽然调度例程不是本身可分页，可以调用可分页的子例程来处理存储 IOCTL 请求。 这些子例程还可以访问可分页内存。

如例程[ **DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)， [**重新初始化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize)，并[**卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)，，不执行任何 I/O 并运行在 IRQL = 被动\_级别还具有可分页的代码。

特殊的注意事项适用于管理分页路径中的存储设备的驱动程序。 驱动程序是"分页路径"中，如果它参与了分页文件上的 I/O 操作。 存储驱动程序时在分页路径中，其[ **DispatchPower** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程对于 IRP\_MJ\_电源请求不能分页。

默认情况下，内核模式驱动程序的代码不是可分页，也不使用的可分页的内核模式驱动程序的全局内存。 有关如何提高代码的可分页的信息，请参阅[使驱动程序代码或数据可分页](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-driver-code-or-data-pageable)。

 

 




