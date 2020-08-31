---
title: 基于 IRP 的 I/O 操作，遵循设备对象标志
description: 基于 IRP 的 I/O 操作，遵循设备对象标志
ms.assetid: d322aeda-a753-4616-8a35-1a5ae5a37cf2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43e6716b33bdc4b3435fe62bf8275137a41999da
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063068"
---
# <a name="irp-based-io-operations-that-obey-device-object-flags"></a>基于 IRP 的 I/O 操作，遵循设备对象标志


## <span id="ddk_irp_based_io_operations_that_obey_device_object_flags_if"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_OBEY_DEVICE_OBJECT_FLAGS_IF"></span>


以下基于 IRP 的 i/o 操作的缓冲方法取决于文件系统卷的[**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构的**Flags**成员值：

-   IRP \_ MJ \_ 目录 \_ 控件

-   IRP \_ MJ \_ 查询 \_ EA

-   IRP \_ MJ \_ 查询 \_ 配额

-   IRP\_MJ\_READ

-   IRP \_ MJ \_ 设置 \_ EA

-   IRP \_ MJ \_ 设置 \_ 配额

-   IRP\_MJ\_WRITE

\_Flags 成员中的 "执行缓冲 \_ io" 和 "执行 \_ 直接 IO" \_ 标志如下**Flags**所示：

-   如果设置了 "按 \_ 缓冲 \_ IO" 标记，则操作将使用缓冲 i/o。

-   如果设置了 "执行 \_ 直接 \_ IO" 标志并且 \_ 未设置 "执行缓冲 io" \_ 标记，则操作将使用直接 i/o。

-   如果这两个标志均未设置，则操作既不使用缓冲的，也不会直接使用 i/o。

有关设备对象标志的详细信息，请参阅 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object) 和 [初始化设备对象](../kernel/initializing-a-device-object.md)。

请注意，IRP \_ mj \_ 读取和 irp \_ mj \_ 写入可以是基于 IRP 的操作或快速 i/o 操作。 如果它们基于 IRP，则缓冲方法由设备对象标志确定，如上所述。 当这些操作是快速 i/o 时，它们始终不使用缓冲和直接 i/o。 有关可作为基于 IRP 或快速 i/o 操作的 i/o 操作的详细信息，请参阅 [可以是基于 irp 或快速](operations-that-can-be-irp-based-or-fast-i-o.md)I/o 的操作。

 

