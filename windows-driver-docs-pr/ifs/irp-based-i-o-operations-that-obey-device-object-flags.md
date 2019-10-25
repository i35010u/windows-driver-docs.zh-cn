---
title: 基于 IRP 的 I/O 操作，遵循设备对象标志
description: 基于 IRP 的 I/O 操作，遵循设备对象标志
ms.assetid: d322aeda-a753-4616-8a35-1a5ae5a37cf2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dbcb1db232aed838e4f08dccf691140f3e65379
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841185"
---
# <a name="irp-based-io-operations-that-obey-device-object-flags"></a>基于 IRP 的 I/O 操作，遵循设备对象标志


## <span id="ddk_irp_based_io_operations_that_obey_device_object_flags_if"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_OBEY_DEVICE_OBJECT_FLAGS_IF"></span>


以下基于 IRP 的 i/o 操作的缓冲方法由设备的**Flags**成员的值确定\_文件系统卷的[**对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构：

-   IRP\_MJ\_DIRECTORY\_控件

-   IRP\_MJ\_QUERY\_EA

-   IRP\_MJ\_QUERY\_配额

-   IRP\_MJ\_READ

-   IRP\_MJ\_集\_EA

-   IRP\_MJ\_集\_配额

-   IRP\_MJ\_WRITE

DO\_将\_IO 进行缓冲处理，并在**flags**成员中执行\_直接\_IO 标志，如下所示：

-   如果已设置 DO\_缓冲\_IO 标志，则操作将使用缓冲 i/o。

-   如果设置了 DO\_DIRECT\_IO 标志，并且未设置 DO\_缓冲\_IO 标志，则操作将使用直接 i/o。

-   如果这两个标志均未设置，则操作既不使用缓冲的，也不会直接使用 i/o。

有关设备对象标志的详细信息，请参阅[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)和[初始化设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/initializing-a-device-object)。

请注意，IRP\_MJ\_读取和 IRP\_MJ\_WRITE 可以是基于 IRP 的操作，也可以是快速 i/o 操作。 如果它们基于 IRP，则缓冲方法由设备对象标志确定，如上所述。 当这些操作是快速 i/o 时，它们始终不使用缓冲和直接 i/o。 有关可作为基于 IRP 或快速 i/o 操作的 i/o 操作的详细信息，请参阅[可以是基于 irp 或快速](operations-that-can-be-irp-based-or-fast-i-o.md)I/o 的操作。

 

 




