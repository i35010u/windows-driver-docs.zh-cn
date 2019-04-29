---
title: 绕过向 Storport SCSI 传递请求的类驱动程序
description: 绕过向 Storport SCSI 传递请求的类驱动程序
ms.assetid: 1162a1e7-a4f8-446f-8106-527f9b916382
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3247c818297208a8ca97d35c0a438dca791b9a81
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380123"
---
# <a name="bypass-a-class-driver-with-scsi-pass-through-requests-to-storport"></a>绕过向 Storport SCSI 传递请求的类驱动程序

在大多数情况下，类驱动程序负责调解 Storport 和更高级别的驱动程序和应用程序之间的所有通信。 某些目标设备，但是，没有类驱动程序。 此类设备的驱动程序必须直接与 Storport 通信通过使用名为"直通"请求的请求的类。 若要使用的传递请求，更高级别的组件是必需设置在请求中，使用 CDB，而不是依赖于类驱动程序来执行此操作。

如果类驱动程序和设备声明，然后"传递"请求必须将定向到的类驱动程序通过打开相应的设备句柄。 如果设备没有类驱动程序且未声明该设备，然后"传递"请求可能会直接发送到适配器，同样，通过打开相应的设备句柄。

SCSI 传递请求包含类型 IRP 的 IRP\_MJ\_设备\_IOCTL 代码控件[ **IOCTL\_SCSI\_传递\_THROUGH** ](https://msdn.microsoft.com/library/windows/hardware/ff560519)或[ **IOCTL\_SCSI\_传递\_THROUGH\_直接**](https://msdn.microsoft.com/library/windows/hardware/ff560521)。 请求，如果通过类驱动程序的类驱动程序是设置有义务**MinorFunction** IRP 到 IRP 代码\_MJ\_设备\_控件。 Storport 检查此值以确定是否传递请求跳过的类驱动程序。 它是应用程序错误将传递请求直接发送到 Storport 如果目标设备具有已声明的存储类驱动程序。

Storport 不会检查传递的请求中嵌入的 SCSI 命令的有效性。

从存储类驱动程序的角度来看 SCSI 传递请求的讨论，请参阅[处理 SCSI 传递请求](handling-scsi-pass-through-requests.md)。

 

 




