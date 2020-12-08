---
title: DispatchFlushBuffers 例程
description: DispatchFlushBuffers 例程
keywords:
- 调度例程 WDK 内核，DispatchFlushBuffers 例程
- DispatchFlushBuffers 例程
- IRP_MJ_FLUSH_BUFFERS i/o 函数代码
- 刷新缓冲区调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1321730aeccc63394a0cfb33b85bf66c33f2449
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799467"
---
# <a name="dispatchflushbuffers-routines"></a>DispatchFlushBuffers 例程





驱动程序的 [*DispatchFlushBuffers*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程处理 [**irp \_ MJ \_ 刷新 \_ 缓冲区**](./irp-mj-flush-buffers.md) i/o 函数代码的 irp。 此 i/o 函数代码的驱动程序支持是可选的，但维护内部数据缓冲区的所有文件系统和筛选器驱动程序都必须处理它，以便在系统关闭时保留对文件数据或元数据的更改。 当缓冲数据需要刷新到磁盘时，i/o 管理器和其他操作系统组件以及其他内核模式驱动程序将发送此请求。 例如，在用户模式应用程序调用 [**FlushFileBuffers**](/windows/win32/api/fileapi/nf-fileapi-flushfilebuffers)时发送。

 

