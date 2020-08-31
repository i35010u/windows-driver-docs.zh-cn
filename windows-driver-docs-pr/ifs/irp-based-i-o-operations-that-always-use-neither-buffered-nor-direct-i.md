---
title: 不使用缓冲和直接 i/o 的基于 IRP 的 i/o 操作
description: 基于 IRP 的 I/O 操作，通常既不使用缓冲的 I/O，也不使用直接 I/O
ms.assetid: 2d757904-e46c-476d-896c-77beacfe4b7c
keywords:
- 缓冲和直接 i/o WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f1d12e189bc419b1a6072d32a1941fd3a87f523
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063078"
---
# <a name="irp-based-io-operations-that-always-use-neither-buffered-nor-direct-io"></a>基于 IRP 的 I/O 操作，通常既不使用缓冲的 I/O，也不使用直接 I/O


## <span id="ddk_irp_based_io_operations_that_always_use_neither_buffered_nor_direc"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_ALWAYS_USE_NEITHER_BUFFERED_NOR_DIREC"></span>


对于文件系统卷，以下基于 IRP 的 i/o 操作始终不使用缓冲和直接 i/o，无论[**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构的**Flags**成员值如何：

-   IRP\_MJ\_PNP

-   IRP \_ MJ \_ 查询 \_ 安全性

-   IRP \_ MJ \_ 设置 \_ 安全性

-   IRP\_MJ\_SYSTEM\_CONTROL

 

