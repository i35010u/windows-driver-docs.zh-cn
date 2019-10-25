---
title: 存储筛选器驱动程序的 I/O 请求支持
description: 存储筛选器驱动程序的 I/O 请求支持
ms.assetid: 2899bf91-584f-47fe-9d5c-3feb07b8707e
keywords:
- 存储筛选器驱动程序 WDK，i/o 请求支持
- 筛选器驱动程序 WDK 存储、i/o 请求支持
- SFD WDK 存储，i/o 请求支持
- Irp WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5675573b90e6872fb899c3996d46b72ff14069fb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844468"
---
# <a name="storage-filter-drivers-support-of-io-requests"></a>存储筛选器驱动程序的 I/O 请求支持


## <span id="ddk_storage_filter_driver_s_support_of_i_o_requests_kg"></span><span id="DDK_STORAGE_FILTER_DRIVER_S_SUPPORT_OF_I_O_REQUESTS_KG"></span>


更高级的存储筛选器驱动程序（SFD）从用户应用程序和更高级别的驱动程序中截取 Irp，并在将其传递到下一个较低的驱动程序（存储类驱动程序或其他筛选器驱动程序）之前，根据需要对其进行修改。 此类 SFD 为需要特殊处理的请求提供特定于设备的支持，例如，转换以非标准格式向设备发送或从设备返回的数据，或对设备进行编程以响应[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求。

较低级别的 SFD 监视存储类驱动程序发出的 SRBs 和/或 Irp，并根据需要对其进行修改，然后将它们传递到下一个较低的驱动程序（存储端口驱动程序或其他筛选器驱动程序）。

较高和较低级别的 SFDs 可以让较低级别的驱动程序处理所有不需要特殊处理的 i/o 请求。

与存储类驱动程序一样，SFD 对所有更高级的内核模式驱动程序都具有以下要求：

-   它必须提供一组*调度*例程，i/o 管理器和/或其他级别的驱动程序可以将 irp 发送到相应的 i/o 操作。 SFD 必须支持同一组 IRP\_MJ\_XXX 作为其设备类型的存储类驱动程序。

-   对于[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求，它必须支持许多类驱动程序支持的 i/o 控制代码，因为它的物理设备可以处理并模拟对驱动程序中任何剩余 i/o 控制代码的支持。

-   它必须具有[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程、[*卸载*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程和*调度*例程来处理 PnP 和电源 irp，并可具有任何其他标准更高级的驱动程序例程，如[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程（如有必要）。

-   它必须遵循用于处理 PnP、电源管理和系统控制 Irp 的规则。

如果其设备具有特殊功能，SFD 可以支持一组驱动程序定义的 i/o 控制代码，以及[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求的系统必需的一组特定于设备的 i/o 控制代码。

 

 




