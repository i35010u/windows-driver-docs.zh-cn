---
title: 处理 SCSI 传递请求
description: 处理 SCSI 传递请求
ms.assetid: 61f8dc02-b5ae-4be5-b7e1-d8207304ef7c
keywords:
- 外围设备 WDK 存储，SCSI 传递请求
- 存储外围设备 WDK、 SCSI 传递请求
- SCSI 传递请求 WDK 存储
- 传递请求 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c232392803ca359610f199dd644eb5022b3f0f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378468"
---
# <a name="handling-scsi-pass-through-requests"></a>处理 SCSI 传递请求


## <span id="ddk_handling_scsi_pass_through_requests_kg"></span><span id="DDK_HANDLING_SCSI_PASS_THROUGH_REQUESTS_KG"></span>


生成的类驱动程序[ **IOCTL\_SCSI\_传递\_THROUGH** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)请求或[ **IOCTL\_SCSI\_传递\_THROUGH\_直接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through_direct)请求负责以下：

-   设置在用户缓冲区的长度**Parameters.DeviceIoControl.InputBufferLength**到至少**sizeof**(SCSI\_传递\_THROUGH) 或**sizeof**(SCSI\_传递\_THROUGH\_直接)

-   像往常一样设置存储端口驱动程序的 I/O 堆栈位置

-   设置**MinorFunction** IRP 到 IRP 中\_MJ\_设备\_控件，将标记为具有已由存储类驱动程序处理请求。

在收到 IOCTL\_SCSI\_传递\_THROUGH 或 IOCTL\_SCSI\_传递\_THROUGH\_从更高级别的驱动程序，存储类驱动程序的直接请求[**DispatchDeviceControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程负责检查嵌入的 SCSI 命令 (CDB) 的有效性，并且如果其设备的有效命令，将请求发送到存储端口驱动程序。

如果端口驱动程序的 I/O 堆栈位置 IOCTL\_SCSI\_传递\_THROUGH 或 IOCTL\_SCSI\_传递\_THROUGH\_直接请求不包含其**MinorFunction**字段设置与 IRP\_MJ\_设备\_控件，端口驱动程序假定请求来源直接应用程序和任何类驱动程序存在的目标设备类型. 它是将此类请求直接发送到设备的已声明的存储类驱动程序的端口驱动程序应用程序错误。

端口驱动程序不检查此类传递请求中嵌入的 SCSI 命令的有效性。

 

 




