---
title: 存储筛选器驱动程序的 I/O 请求支持
description: 存储筛选器驱动程序的 I/O 请求支持
ms.assetid: 2899bf91-584f-47fe-9d5c-3feb07b8707e
keywords:
- 存储筛选器驱动程序 WDK，I/O 请求支持
- 筛选器驱动程序 WDK 存储 I/O 请求支持
- SFD WDK 存储、 I/O 请求支持
- Irp WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c61abbe23d0271fa35c1e0dc826349139ddd05cb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368189"
---
# <a name="storage-filter-drivers-support-of-io-requests"></a>存储筛选器驱动程序的 I/O 请求支持


## <span id="ddk_storage_filter_driver_s_support_of_i_o_requests_kg"></span><span id="DDK_STORAGE_FILTER_DRIVER_S_SUPPORT_OF_I_O_REQUESTS_KG"></span>


更高级别的存储筛选器驱动程序 (SFD) 从用户应用程序和更高级别的驱动程序截获 Irp，并根据需要将其传递给下一个较低驱动程序 （存储类驱动程序或另一个筛选器驱动程序） 之前修改它们。 此类 SFD 提供特定于设备的支持需要特殊处理，如将数据转换发送到或从设备中使用了非标准格式，或编程设备在响应中的返回的请求[ **IRP\_MJ\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求。

较低级别 SFD 监视 Srb 和/或存储类驱动程序发出的 Irp，并根据需要将其传递给下一个较低驱动程序 （存储端口驱动程序或另一个筛选器驱动程序） 之前修改它们。

这两个较高和较低级别 SFDs 可以让处理不要求特殊处理的所有 I/O 请求的较低的驱动程序。

存储类驱动程序，如 SFD 具有普遍适用于所有较高级别的内核模式驱动程序的以下要求：

-   它必须提供一套*调度*I/O 管理器和/或仍更高级别的驱动程序可以发送到 Irp 为相应的 I/O 操作的例程。 SFD 必须支持一组相同的 IRP\_MJ\_XXX 作为其类型的设备的存储类驱动程序。

-   有关[ **IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求时，它必须支持尽可能多的类驱动程序支持 I/O 控制代码，如其物理设备可以处理和如果可能，模拟对驱动程序中任何剩余的 I/O 控制代码的支持。

-   它必须具有[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程， [*卸载*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程，并*调度*例程来处理 PnP 和电源 Irp 和可以具有任何其他标准更高级别的驱动程序例程，如[ *IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，根据需要。

-   它必须遵循处理即插即用、 电源管理和系统控制 Irp 的规则。

如果其设备具有特殊功能，SFD 可以支持一组系统所需集以及特定于设备的类型的 I/O 控制代码的驱动程序定义的 I/O 控制代码[ **IRP\_MJ\_设备\_控件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求。

 

 




