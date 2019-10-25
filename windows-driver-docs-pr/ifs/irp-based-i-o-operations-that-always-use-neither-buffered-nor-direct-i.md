---
title: 不使用缓冲和直接 i/o 的基于 IRP 的 i/o 操作
description: 基于 IRP 的 I/O 操作，通常既不使用缓冲的 I/O，也不使用直接 I/O
ms.assetid: 2d757904-e46c-476d-896c-77beacfe4b7c
keywords:
- 缓冲和直接 i/o WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 307caef3d68bf6bdb15769e66152582e70f26367
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841187"
---
# <a name="irp-based-io-operations-that-always-use-neither-buffered-nor-direct-io"></a>基于 IRP 的 I/O 操作，通常既不使用缓冲的 I/O，也不使用直接 I/O


## <span id="ddk_irp_based_io_operations_that_always_use_neither_buffered_nor_direc"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_ALWAYS_USE_NEITHER_BUFFERED_NOR_DIREC"></span>


以下基于 IRP 的 i/o 操作始终不使用缓冲和直接 i/o，无论设备的**Flags**成员的值\_文件系统卷的[**对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构：

-   IRP\_MJ\_PNP

-   IRP\_MJ\_QUERY\_安全性

-   IRP\_MJ\_集\_安全性

-   IRP\_MJ\_SYSTEM\_CONTROL

 

 




