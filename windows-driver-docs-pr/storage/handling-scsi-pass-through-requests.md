---
title: 处理 SCSI 传递请求
description: 处理 SCSI 传递请求
ms.assetid: 61f8dc02-b5ae-4be5-b7e1-d8207304ef7c
keywords:
- 外围设备 WDK 存储，SCSI 传递请求
- 存储外围设备 WDK，SCSI 传递请求
- SCSI 传递请求 WDK 存储
- 传递请求 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cceba4833e9da6aab7ea44c538c15bfd19fd293
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189051"
---
# <a name="handling-scsi-pass-through-requests"></a>处理 SCSI 传递请求


## <span id="ddk_handling_scsi_pass_through_requests_kg"></span><span id="DDK_HANDLING_SCSI_PASS_THROUGH_REQUESTS_KG"></span>


类驱动程序通过直接请求生成 [**ioctl \_ scsi \_ 直通 \_ **](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through) 请求或 [**ioctl \_ scsi \_ pass \_ \_ **](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through_direct) 的类驱动程序，负责执行以下操作：

-   将**DeviceIoControl. InputBufferLength**上的用户缓冲区的长度设置为至少为**sizeof** (\_ \_ 通过**sizeof** \_ \_ \_ 直接) 将 scsi 传递) 或 sizeof (

-   照常设置存储端口驱动程序的 i/o 堆栈位置

-   将 IRP 中的 **MinorFunction** 设置为 irp \_ MJ \_ 设备 \_ 控件，该控件将请求标记为已由存储类驱动程序处理。

在通过 \_ \_ \_ \_ \_ \_ \_ 直接请求从更高级别的驱动程序收到 ioctl scsi pass 或 ioctl scsi pass 时，存储类驱动程序的 [**DispatchDeviceControl**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程负责检查嵌入的 scsi 命令 (CDB) 的有效性，如果该命令对于其设备有效，则将请求发送到存储端口驱动程序。

如果用于 IOCTL scsi 直通的端口驱动程序的 i/o 堆栈位置 \_ \_ \_ 或 \_ \_ 通过直接请求的 ioctl SCSI 直通 \_ 请求没有 \_ 使用 IRP MJ 设备控制设置其 **MinorFunction** 字段 \_ \_ \_ ，则端口驱动程序会假设请求直接来自应用程序，并且不存在针对目标设备类型的类驱动程序。 应用程序错误是将此类请求直接发送到存储类驱动程序所声称的设备的端口驱动程序。

端口驱动程序不会检查嵌入在此类传递请求中的 SCSI 命令的有效性。

 

