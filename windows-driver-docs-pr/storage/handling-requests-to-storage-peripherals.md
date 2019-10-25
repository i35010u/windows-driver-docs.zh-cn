---
title: 处理对存储外设的请求
description: 处理对存储外设的请求
ms.assetid: 3859588e-fc39-4323-a901-8771874e64d2
keywords:
- 存储类驱动程序 WDK、外围设备
- 类驱动程序 WDK 存储、外围设备
- 外设 WDK 存储
- 存储外围设备 WDK
- 外围设备 WDK 存储，关于存储外围设备
- 存储外围设备 WDK，关于存储外围设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c87098ee1648551dc5dcdc792eb0fa5e18e68ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845040"
---
# <a name="handling-requests-to-storage-peripherals"></a>处理对存储外设的请求


## <span id="ddk_handling_requests_to_storage_peripherals_kg"></span><span id="DDK_HANDLING_REQUESTS_TO_STORAGE_PERIPHERALS_KG"></span>


对于要求存储端口驱动程序通过基础总线执行请求的所有请求，类驱动程序必须使用包含 SCSI 命令描述符块（CDB）的 SCSI 请求块（SRB）设置 IRP。 因此，大多数存储类驱动程序具有一个或多个内部*BuildRequest*例程来构建 SRBs。 有关此类例程的详细信息，请参阅[存储类驱动程序的 BuildRequest 例程](storage-class-driver-s-buildrequest-routine.md)。

存储类驱动程序还会将 IRP\_MJ\_SCSI 请求传递到基础存储端口驱动程序。 此类请求可能源自[存储筛选器驱动程序](storage-filter-drivers.md)。

对于[**IOCTL\_SCSI\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)通过请求（如[处理 SCSI 直通请求](handling-scsi-pass-through-requests.md)中所述）传递\_，该类驱动程序负责将**MinorFunction**代码设置为 IRP\_MJ\_设备\_控件在将 IRP 传递到端口驱动程序上，然后将 IRP\_设备\_控制请求传递到端口驱动[**程序，然后**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)再将\_irp 传递到端口驱动程序的 i/o 堆栈位置。

每个存储类驱动程序负责拆分超过基础 HBA 功能的传输请求（IRP\_MJ\_读取和/或 IRP\_MJ\_写入）。 因此，大多数类驱动程序还会调用[存储类驱动程序的 SplitTransferRequest 例程](storage-class-driver-s-splittransferrequest-routine.md)中所述的内部*SplitTransferRequest*例程，或在用于读取和写入的调度例程中实现相同的功能发出.

有关处理对存储外围设备的请求的其他信息，请参阅以下主题：

[处理 SCSI 传递请求](handling-scsi-pass-through-requests.md)

[处理对存储外围设备的 PnP 请求](handling-pnp-requests-to-storage-peripherals.md)

[处理对存储外围设备的电源请求](handling-power-requests-to-storage-peripherals.md)

[排队存储请求](queuing-storage-requests.md)

 

 




