---
title: 通过 SCSI 传递请求绕过类驱动程序
description: 通过 SCSI 传递请求绕过类驱动程序
ms.assetid: 7f26e0bc-f01b-4430-aa9f-0f684fdbc2ec
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c13629f602bccf1784f857ece563dd159ffb50d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563189"
---
# <a name="bypassing-the-class-driver-with-scsi-pass-through-requests"></a>通过 SCSI 传递请求绕过类驱动程序


## <span id="ddk_bypassing_the_class_driver_with_scsi_pass_through_requests_kg"></span><span id="DDK_BYPASSING_THE_CLASS_DRIVER_WITH_SCSI_PASS_THROUGH_REQUESTS_KG"></span>


在大多数情况下，类驱动程序负责调解 SCSI 端口以及更高级别的驱动程序和应用程序之间的所有通信。 某些目标设备，但是，没有类驱动程序。 通过使用类名为"直通"请求的请求的情况下，此类设备的驱动程序必须直接与 SCSI 端口通信。 若要使用的传递请求，更高级别的组件是必需设置在请求中，使用 CDB，而不是依赖于类驱动程序来执行此操作。

SCSI 传递请求包含类型 IRP 的 IRP\_MJ\_设备\_IOCTL 代码为控件[ **IOCTL\_SCSI\_传递\_通过**](https://msdn.microsoft.com/library/windows/hardware/ff560519)或[ **IOCTL\_SCSI\_传递\_THROUGH\_直接**](https://msdn.microsoft.com/library/windows/hardware/ff560521)。 请求，如果通过类驱动程序的类驱动程序是义务设置 IRP **MinorFunction** IRP 的代码\_MJ\_设备\_控件。 SCSI 端口检查此值以确定是否传递请求跳过的类驱动程序。 它是直接向 SCSI 端口发送传递请求，如果目标设备具有已声明的存储类驱动程序应用程序错误。

SCSI 端口不会检查传递的请求中嵌入的 SCSI 命令的有效性。

从存储类驱动程序的角度来看 SCSI 传递请求的讨论，请参阅[处理 SCSI 传递请求](handling-scsi-pass-through-requests.md)

 

 




