---
title: 基于 IRP 的 I/O 操作，使用既不缓冲 Nor 直接 I/O
description: 基于 IRP 的 I/O 操作，通常既不使用缓冲的 I/O，也不使用直接 I/O
ms.assetid: 2d757904-e46c-476d-896c-77beacfe4b7c
keywords:
- 既不缓冲，也不直接 I/O WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec3c38a424d9c1ceb3fc6346245a5d82cb8b8dc8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353386"
---
# <a name="irp-based-io-operations-that-always-use-neither-buffered-nor-direct-io"></a>基于 IRP 的 I/O 操作，通常既不使用缓冲的 I/O，也不使用直接 I/O


## <span id="ddk_irp_based_io_operations_that_always_use_neither_buffered_nor_direc"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_ALWAYS_USE_NEITHER_BUFFERED_NOR_DIREC"></span>


以下基于 IRP 的 I/O 操作始终使用未缓冲也不直接 I/O，而不考虑的值**标志**的成员[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)文件系统卷的结构：

-   IRP\_MJ\_PNP

-   IRP\_MJ\_查询\_安全

-   IRP\_MJ\_SET\_SECURITY

-   IRP\_MJ\_SYSTEM\_CONTROL

 

 




