---
title: 使用 SCSI 直通请求跳过对 Storport 的类驱动程序
description: 使用 SCSI 直通请求跳过对 Storport 的类驱动程序
ms.assetid: 1162a1e7-a4f8-446f-8106-527f9b916382
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3ac6f981d6bac9f216a7209fbd0bfee6e6632fa
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191649"
---
# <a name="bypass-a-class-driver-with-scsi-pass-through-requests-to-storport"></a>使用 SCSI 直通请求跳过对 Storport 的类驱动程序

在大多数情况下，类驱动程序会调节 Storport 和更高级别的驱动程序与应用程序之间的所有通信。 但有些目标设备没有类驱动程序。 此类设备的驱动程序必须使用称为 "传递" 请求的一类请求直接与 Storport 通信。 若要使用传递请求，需要较高级别的组件来设置请求中使用的 CDB，而不是依靠类驱动程序来执行此操作。

如果存在类驱动程序，并且设备已声明，则必须通过打开相应的设备句柄，将 "传递" 请求定向到类驱动程序。 如果没有设备的类驱动程序，并且未声明设备，则可以通过打开相应的设备句柄，将 "传递" 请求直接发送到适配器。

SCSI 传递请求由 IRP \_ MJ 设备控制的 irp 组成 \_ \_ ，其中包含 ioctl 的 ioctl 代码、 [** \_ \_ \_ 通过**](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through) ioctl 执行的 ioctl 代码， [**或者 \_ \_ \_ 通过 \_ 直接执行的 ioctl scsi 直通**](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through_direct)。 如果请求通过类驱动程序，则类驱动程序有义务将 IRP 的 **MinorFunction** 代码设置为 irp \_ MJ \_ 设备 \_ 控制。 Storport 检查此值以确定传递请求是否绕过类驱动程序。 如果目标设备已被存储类驱动程序所声称，则将传递请求直接发送到 Storport 会出现应用程序错误。

Storport 不检查在传递请求中嵌入的 SCSI 命令的有效性。

有关从存储类驱动程序的角度对 SCSI 传递请求的讨论，请参阅 [处理 Scsi 传递请求](handling-scsi-pass-through-requests.md)。

 

