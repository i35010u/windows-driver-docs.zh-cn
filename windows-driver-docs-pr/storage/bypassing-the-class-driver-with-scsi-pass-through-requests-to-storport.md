---
title: 使用 SCSI 直通请求跳过对 Storport 的类驱动程序
description: 使用 SCSI 直通请求跳过对 Storport 的类驱动程序
ms.assetid: 1162a1e7-a4f8-446f-8106-527f9b916382
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69ef1a01a31c56466e4634e2c594ab4c2a9e7eb5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845100"
---
# <a name="bypass-a-class-driver-with-scsi-pass-through-requests-to-storport"></a>使用 SCSI 直通请求跳过对 Storport 的类驱动程序

在大多数情况下，类驱动程序会调节 Storport 和更高级别的驱动程序与应用程序之间的所有通信。 但有些目标设备没有类驱动程序。 此类设备的驱动程序必须使用称为 "传递" 请求的一类请求直接与 Storport 通信。 若要使用传递请求，需要较高级别的组件来设置请求中使用的 CDB，而不是依靠类驱动程序来执行此操作。

如果存在类驱动程序，并且设备已声明，则必须通过打开相应的设备句柄，将 "传递" 请求定向到类驱动程序。 如果没有设备的类驱动程序，并且未声明设备，则可以通过打开相应的设备句柄，将 "传递" 请求直接发送到适配器。

SCSI 传递请求包含 IRP 类型为 IRP\_MJ 的 IRP\_设备\_控制，其中包含 ioctl 的 IOCTL 代码[ **\_scsi\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)通过或[**ioctl\_\_DIRECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through_direct)。 如果请求通过类驱动程序，则类驱动程序有义务将 IRP 的**MinorFunction**代码设置为 IRP\_MJ\_设备\_控件。 Storport 检查此值以确定传递请求是否绕过类驱动程序。 如果目标设备已被存储类驱动程序所声称，则将传递请求直接发送到 Storport 会出现应用程序错误。

Storport 不检查在传递请求中嵌入的 SCSI 命令的有效性。

有关从存储类驱动程序的角度对 SCSI 传递请求的讨论，请参阅[处理 Scsi 传递请求](handling-scsi-pass-through-requests.md)。

 

 




