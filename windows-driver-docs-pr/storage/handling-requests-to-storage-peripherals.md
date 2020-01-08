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
ms.openlocfilehash: 75be72bcfdaa2debf81970f3b24fec05de5d46c8
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606509"
---
# <a name="handling-requests-to-storage-peripherals"></a>处理对存储外设的请求

对于要求存储端口驱动程序通过基础总线执行请求的所有请求，类驱动程序必须使用包含 SCSI 命令描述符块（CDB）的 SCSI 请求块（SRB）设置 IRP。 因此，大多数存储类驱动程序具有一个或多个内部*BuildRequest*例程来构建 SRBs。 有关此类例程的详细信息，请参阅[存储类驱动程序的 BuildRequest 例程](storage-class-driver-s-buildrequest-routine.md)。

存储类驱动程序还会将 IRP_MJ_SCSI 请求传递到基础存储端口驱动程序。 此类请求可能源自[存储筛选器驱动程序](storage-filter-drivers.md)。

对于[处理 SCSI 传递请求](handling-scsi-pass-through-requests.md)中所述的[**IOCTL_SCSI_PASS_THROUGH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)请求，类驱动程序负责将**MinorFunction**代码设置为在将 IRP_MJ_DEVICE_CONTROL 请求传入到端口驱动程序并将其传递给[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)之前，将其设置为在 IRP 的端口驱动程序的 i/o 堆栈位置中 IRP_MJ_DEVICE_CONTROL。

每个存储类驱动程序负责拆分超过基础 HBA 功能的传输请求（IRP_MJ_READ 和/或 IRP_MJ_WRITE）。 因此，大多数类驱动程序还会调用[存储类驱动程序的 SplitTransferRequest 例程](storage-class-driver-s-splittransferrequest-routine.md)中所述的内部*SplitTransferRequest*例程，或在调度例程中为读取和写入请求实现相同的功能。

有关处理对存储外围设备的请求的其他信息，请参阅以下主题：

[处理 SCSI 传递请求](handling-scsi-pass-through-requests.md)

[处理对存储外围设备的 PnP 请求](handling-pnp-requests-to-storage-peripherals.md)

[处理对存储外围设备的电源请求](handling-power-requests-to-storage-peripherals.md)

[排队存储请求](queuing-storage-requests.md)
