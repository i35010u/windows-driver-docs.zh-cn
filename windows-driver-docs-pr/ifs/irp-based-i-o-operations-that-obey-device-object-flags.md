---
title: 基于 IRP 的 I/O 操作，遵循设备对象标志
description: 基于 IRP 的 I/O 操作，遵循设备对象标志
ms.assetid: d322aeda-a753-4616-8a35-1a5ae5a37cf2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d7e1150aebabf4d8cd0d705666bd3c90edb6b2f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568239"
---
# <a name="irp-based-io-operations-that-obey-device-object-flags"></a>基于 IRP 的 I/O 操作，遵循设备对象标志


## <span id="ddk_irp_based_io_operations_that_obey_device_object_flags_if"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_OBEY_DEVICE_OBJECT_FLAGS_IF"></span>


以下基于 IRP 的 I/O 操作的缓冲方法确定的值**标志**的成员[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)结构文件系统卷：

-   IRP\_MJ\_DIRECTORY\_控件

-   IRP\_MJ\_查询\_EA

-   IRP\_MJ\_查询\_配额

-   IRP\_MJ\_READ

-   IRP\_MJ\_SET\_EA

-   IRP\_MJ\_SET\_QUOTA

-   IRP\_MJ\_WRITE

DO\_缓冲\_IO 并执行\_直接\_IO 标志中**标志**成员使用，如下所示：

-   如果执行操作\_缓冲\_设置 IO 标志，该操作将使用缓冲的 I/O。

-   如果执行操作\_直接\_IO 标志是组和 DO\_缓冲\_IO 标志未设置，该操作使用直接 I/O。

-   如果设置了任一标志，该操作使用既不缓冲，也不直接 I/O。

有关设备对象标志的详细信息，请参阅[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)并[初始化设备对象](https://msdn.microsoft.com/library/windows/hardware/ff547807)。

请注意该 IRP\_MJ\_IRP 读\_MJ\_写入可以是基于 IRP 的或快速 I/O 操作。 如果基于 IRP，缓冲的方法是通过按上文所述的设备对象标志确定。 这些操作时快速 I/O，它们始终使用未缓冲也不直接 I/O。 可以是基于 IRP 的或快速 I/O 操作的 I/O 操作的详细信息，请参阅[操作，可以将 IRP 基于或快速 I/O](operations-that-can-be-irp-based-or-fast-i-o.md)。

 

 




