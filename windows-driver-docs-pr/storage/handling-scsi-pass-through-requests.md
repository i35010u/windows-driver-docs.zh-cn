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
ms.openlocfilehash: a5a4c09f21d5d6f2ad5680fd59f63cb07949f499
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826265"
---
# <a name="handling-scsi-pass-through-requests"></a>处理 SCSI 传递请求


## <span id="ddk_handling_scsi_pass_through_requests_kg"></span><span id="DDK_HANDLING_SCSI_PASS_THROUGH_REQUESTS_KG"></span>


一个类驱动程序，用于生成[**IOCTL\_scsi\_通过请求\_通过**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)请求或[**IOCTL\_SCSI\_通过\_直接请求通过\_直接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through_direct)请求负责以下操作：

-   将**DeviceIoControl. InputBufferLength**的用户缓冲区的长度设置为至少为**sizeof**（scsi\_传递\_到）或**sizeof**（scsi\_通过\_直接传递\_）

-   照常设置存储端口驱动程序的 i/o 堆栈位置

-   将 IRP 中的**MinorFunction**设置为 IRP\_MJ\_设备\_控件，该控件将请求标记为已由存储类驱动程序处理。

收到 IOCTL\_SCSI\_通过\_或 IOCTL\_SCSI\_通过更高级别的驱动程序\_直接请求，存储类驱动程序的[**DispatchDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程是负责检查嵌入式 SCSI 命令（CDB）的有效性，如果命令对于其设备有效，则将请求发送到存储端口驱动程序。

如果用于 IOCTL 的端口驱动程序的 i/o 堆栈位置\_SCSI\_\_通过或 IOCTL\_SCSI\_通过\_直接请求未使用 IRP\_MJ 设置其**MinorFunction**字段\_设备\_控制，端口驱动程序假设请求直接来自应用程序，并且目标设备类型不存在类驱动程序。 应用程序错误是将此类请求直接发送到存储类驱动程序所声称的设备的端口驱动程序。

端口驱动程序不会检查嵌入在此类传递请求中的 SCSI 命令的有效性。

 

 




