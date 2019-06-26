---
title: 基于 IRP 的 I/O 操作，始终使用缓冲的 I/O
description: 基于 IRP 的 I/O 操作，始终使用缓冲的 I/O
ms.assetid: ac9b62a2-a562-4f40-83af-e1c74d58ce2b
keywords:
- 缓冲的 I/O WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e02664283d22df920f152b950300071b8296e079
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360874"
---
# <a name="irp-based-io-operations-that-always-use-buffered-io"></a>基于 IRP 的 I/O 操作，始终使用缓冲的 I/O


## <span id="ddk_irp_based_io_operations_that_always_use_buffered_io_if"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_ALWAYS_USE_BUFFERED_IO_IF"></span>


以下基于 IRP 的 I/O 操作始终使用缓冲的 I/O，而不考虑的值**标志**的成员[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)结构文件系统卷：

-   IRP\_MJ\_CREATE ([**EaBuffer parameter**](https://docs.microsoft.com/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-create))

-   IRP\_MJ\_QUERY\_INFORMATION

-   IRP\_MJ\_查询\_卷\_信息

-   IRP\_MJ\_SET\_INFORMATION

-   IRP\_MJ\_设置\_卷\_信息

请注意该 IRP\_MJ\_查询\_信息也可以是一个快速的 I/O 操作。 快速的 I/O 操作时，它使用既不缓冲，也不直接 I/O。 可以是基于 IRP 的或快速 I/O 操作的 I/O 操作的详细信息，请参阅[操作，可以将 IRP 基于或快速 I/O](operations-that-can-be-irp-based-or-fast-i-o.md)。

 

 




