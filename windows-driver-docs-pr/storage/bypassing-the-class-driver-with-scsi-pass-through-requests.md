---
title: 通过 SCSI 传递请求绕过类驱动程序
description: 通过 SCSI 传递请求绕过类驱动程序
ms.assetid: 7f26e0bc-f01b-4430-aa9f-0f684fdbc2ec
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46668169e6911e62dc4cbccee4f507643d72cca6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845096"
---
# <a name="bypassing-the-class-driver-with-scsi-pass-through-requests"></a>通过 SCSI 传递请求绕过类驱动程序


## <span id="ddk_bypassing_the_class_driver_with_scsi_pass_through_requests_kg"></span><span id="DDK_BYPASSING_THE_CLASS_DRIVER_WITH_SCSI_PASS_THROUGH_REQUESTS_KG"></span>


在大多数情况下，类驱动程序会调节 SCSI 端口和更高级别的驱动程序与应用程序之间的所有通信。 但有些目标设备没有类驱动程序。 此类设备的驱动程序必须使用称为 "传递" 请求的一类请求直接与 SCSI 端口进行通信。 若要使用传递请求，需要较高级别的组件来设置请求中使用的 CDB，而不是依靠类驱动程序来执行此操作。

SCSI 传递请求包含 IRP 类型为 IRP\_MJ 的 IRP\_设备\_控制，其中包含 ioctl 的 IOCTL 代码[ **\_scsi\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)通过或[**ioctl\_scsi\_通过\_DIRECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through_direct)。 如果请求通过类驱动程序，则类驱动程序有义务将 IRP 的**MinorFunction**代码设置为 IRP\_MJ\_设备\_控件。 SCSI 端口检查此值以确定传递请求是否绕过类驱动程序。 如果目标设备已被存储类驱动程序所声称，将直接向 SCSI 端口发送传递请求是应用程序错误。

SCSI 端口不检查在传递请求中嵌入的 SCSI 命令的有效性。

有关从存储类驱动程序的角度对 SCSI 传递请求的讨论，请参阅[处理 Scsi 传递请求](handling-scsi-pass-through-requests.md)

 

 




