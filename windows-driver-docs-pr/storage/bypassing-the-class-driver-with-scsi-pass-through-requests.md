---
title: 通过 SCSI 传递请求绕过类驱动程序
description: 通过 SCSI 传递请求绕过类驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa7829d8670c94de90b34007550255cd1a2ca50d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811779"
---
# <a name="bypassing-the-class-driver-with-scsi-pass-through-requests"></a>通过 SCSI 传递请求绕过类驱动程序


## <span id="ddk_bypassing_the_class_driver_with_scsi_pass_through_requests_kg"></span><span id="DDK_BYPASSING_THE_CLASS_DRIVER_WITH_SCSI_PASS_THROUGH_REQUESTS_KG"></span>


在大多数情况下，类驱动程序会调节 SCSI 端口和更高级别的驱动程序与应用程序之间的所有通信。 但有些目标设备没有类驱动程序。 此类设备的驱动程序必须使用称为 "传递" 请求的一类请求直接与 SCSI 端口进行通信。 若要使用传递请求，需要较高级别的组件来设置请求中使用的 CDB，而不是依靠类驱动程序来执行此操作。

SCSI 传递请求包括 IRP \_ MJ \_ 设备控件的 irp \_ ，其中包含 ioctl 的 ioctl 代码，并通过 [**\_ \_ \_ \_ 直接**](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through_direct) [**\_ \_ \_**](/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)连接到 ioctl scsi 直通。 如果请求通过类驱动程序，则类驱动程序有义务将 IRP 的 **MinorFunction** 代码设置为 irp \_ MJ \_ 设备 \_ 控制。 SCSI 端口检查此值以确定传递请求是否绕过类驱动程序。 如果目标设备已被存储类驱动程序所声称，将直接向 SCSI 端口发送传递请求是应用程序错误。

SCSI 端口不检查在传递请求中嵌入的 SCSI 命令的有效性。

有关从存储类驱动程序的角度对 SCSI 传递请求的讨论，请参阅 [处理 scsi Pass-Through 请求](handling-scsi-pass-through-requests.md)

 

