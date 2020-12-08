---
title: 存储筛选器驱动程序的 I/O 请求支持
description: 存储筛选器驱动程序的 I/O 请求支持
keywords:
- 存储筛选器驱动程序 WDK，i/o 请求支持
- 筛选器驱动程序 WDK 存储、i/o 请求支持
- SFD WDK 存储，i/o 请求支持
- Irp WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c46f690a360ddea1720f6ac4670c909f1f5714dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838545"
---
# <a name="storage-filter-drivers-support-of-io-requests"></a>存储筛选器驱动程序的 I/O 请求支持


## <span id="ddk_storage_filter_driver_s_support_of_i_o_requests_kg"></span><span id="DDK_STORAGE_FILTER_DRIVER_S_SUPPORT_OF_I_O_REQUESTS_KG"></span>


更高级的存储筛选器驱动程序 (SFD) 从用户应用程序和更高级别的驱动程序中截取 Irp，并在将其传递到 (存储类驱动程序或其他筛选器驱动程序) 之前，根据需要进行修改。 此类 SFD 为需要特殊处理的请求提供特定于设备的支持，例如，转换以非标准格式向设备发送或从设备返回的数据，或对设备进行编程以响应 [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md) 请求。

较低级别的 SFD 监视存储类驱动程序发出的 SRBs 和/或 Irp，并根据需要对其进行修改，然后将它们传递到 (存储端口驱动程序或其他筛选器驱动程序) 。

较高和较低级别的 SFDs 可以让较低级别的驱动程序处理所有不需要特殊处理的 i/o 请求。

与存储类驱动程序一样，SFD 对所有更高级的内核模式驱动程序都具有以下要求：

-   它必须提供一组 *调度* 例程，i/o 管理器和/或其他级别的驱动程序可以将 irp 发送到相应的 i/o 操作。 SFD 必须支持同一组 IRP \_ MJ \_ XXX 作为其设备类型的存储类驱动程序。

-   对于 [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md) 请求，它必须支持多个类驱动程序支持的 i/o 控制代码，因为它的物理设备可以处理并模拟对驱动程序中任何剩余 i/o 控制代码的支持。

-   它必须具有 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程、 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程、 [*卸载*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程和 *调度* 例程来处理 PnP 和电源 irp，并可根据需要使用任何其他标准的高级驱动程序例程，如 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。

-   它必须遵循用于处理 PnP、电源管理和系统控制 Irp 的规则。

如果其设备具有特殊功能，SFD 可以支持一组驱动程序定义的 i/o 控制代码，以及用于 [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md) 请求的系统必需的特定于设备类型的 i/o 控制代码。

 

