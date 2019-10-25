---
title: 访问 I/O 操作的用户缓冲区
description: 访问 I/O 操作的用户缓冲区
ms.assetid: 0f4334bf-eec9-4667-af02-537e3357d872
keywords:
- 缓冲 WDK 文件系统微筛选器
- FLT_PARAMETERS
- 内存描述符列出 WDK 文件系统微筛选器
- MDLs WDK 文件系统
- I/o WDK 文件系统
- 基于 IRP 的 i/o 操作 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1062a9341388588e7163b5aa30365d9f65c54750
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841507"
---
# <a name="accessing-the-user-buffers-for-an-io-operation"></a>访问 I/O 操作的用户缓冲区


## <span id="ddk_accessing_the_user_buffers_for_an_io_operation_if"></span><span id="DDK_ACCESSING_THE_USER_BUFFERS_FOR_AN_IO_OPERATION_IF"></span>


I/o 操作的[**FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含操作特定于操作的参数，包括操作中使用的任何缓冲区的缓冲区地址和内存描述符列表（MDL）。

对于基于 IRP 的 i/o 操作，可以使用指定操作的缓冲区：

-   仅 MDL （通常用于分页 i/o）

-   仅限缓冲区地址

-   缓冲区地址和 MDL

对于快速 i/o 操作，仅指定用户空间缓冲区地址。 具有缓冲区的快速 i/o 操作始终不使用缓冲和直接 i/o，因此永远不会有 MDL 参数。

以下主题提供有关在微筛选器驱动程序[**preoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)和[**postoperation 回调例程**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)中处理基于 IRP 和快速 i/o 操作的缓冲区地址和 MDLs 的准则：

[访问 Preoperation 回调例程中的用户缓冲区](accessing-user-buffers-in-a-preoperation-callback-routine.md)

[访问 Postoperation 回调例程中的用户缓冲区](accessing-user-buffers-in-a-postoperation-callback-routine.md)

 

 




