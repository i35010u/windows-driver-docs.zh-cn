---
title: 基于 IRP 的 I/O 操作，始终使用缓冲的 I/O
description: 基于 IRP 的 I/O 操作，始终使用缓冲的 I/O
ms.assetid: ac9b62a2-a562-4f40-83af-e1c74d58ce2b
keywords:
- 缓冲 i/o WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e96c871b96c2008d08447d5a9f7f45f15887d67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841188"
---
# <a name="irp-based-io-operations-that-always-use-buffered-io"></a>基于 IRP 的 I/O 操作，始终使用缓冲的 I/O


## <span id="ddk_irp_based_io_operations_that_always_use_buffered_io_if"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_ALWAYS_USE_BUFFERED_IO_IF"></span>


以下基于 IRP 的 i/o 操作始终使用缓冲 i/o，而不考虑设备的**Flags**成员值\_文件系统卷的[**对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构：

-   IRP\_MJ\_CREATE （[**EaBuffer 参数**](https://docs.microsoft.com/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-create)）

-   IRP\_MJ\_QUERY\_INFORMATION

-   IRP\_MJ\_查询\_卷\_信息

-   IRP\_MJ\_SET\_INFORMATION

-   IRP\_MJ\_设置\_卷\_信息

请注意，IRP\_MJ\_查询\_信息也可以是快速的 i/o 操作。 当它是快速 i/o 操作时，它既不使用缓冲也不使用直接 i/o。 有关可作为基于 IRP 或快速 i/o 操作的 i/o 操作的详细信息，请参阅[可以是基于 irp 或快速](operations-that-can-be-irp-based-or-fast-i-o.md)I/o 的操作。

 

 




