---
title: 访问 I/O 操作的用户缓冲区
description: 访问 I/O 操作的用户缓冲区
keywords:
- 缓冲 WDK 文件系统微筛选器
- FLT_PARAMETERS
- 内存描述符列出 WDK 文件系统微筛选器
- MDLs WDK 文件系统
- I/o WDK 文件系统
- 基于 IRP 的 i/o 操作 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee65070bed1a05089445d700dee87a6e4c16f984
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836815"
---
# <a name="accessing-the-user-buffers-for-an-io-operation"></a>访问 I/O 操作的用户缓冲区


## <span id="ddk_accessing_the_user_buffers_for_an_io_operation_if"></span><span id="DDK_ACCESSING_THE_USER_BUFFERS_FOR_AN_IO_OPERATION_IF"></span>


I/o 操作的 [**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters) 结构包含操作特定于操作的参数，其中包括) 操作中使用的任何缓冲区 (MDL 的缓冲区地址和内存描述符列表。

对于基于 IRP 的 i/o 操作，可以使用指定操作的缓冲区：

-   MDL 仅 (通常用于分页 i/o) 

-   仅限缓冲区地址

-   缓冲区地址和 MDL

对于快速 i/o 操作，仅指定用户空间缓冲区地址。 具有缓冲区的快速 i/o 操作始终不使用缓冲和直接 i/o，因此永远不会有 MDL 参数。

以下主题提供有关在微筛选器驱动程序 [**preoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback) 和 [**postoperation 回调例程**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_post_operation_callback)中处理基于 IRP 和快速 i/o 操作的缓冲区地址和 MDLs 的准则：

[访问 Preoperation 回调例程中的用户缓冲区](accessing-user-buffers-in-a-preoperation-callback-routine.md)

[访问 Postoperation 回调例程中的用户缓冲区](accessing-user-buffers-in-a-postoperation-callback-routine.md)

 

