---
title: DispatchFlushBuffers 例程
description: DispatchFlushBuffers 例程
ms.assetid: 091ce55c-e867-4ba4-aa25-5c20af45d9c2
keywords:
- 调度例程 WDK 内核，DispatchFlushBuffers 例程
- DispatchFlushBuffers 例程
- IRP_MJ_FLUSH_BUFFERS i/o 函数代码
- 刷新缓冲区调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5306fc37299eedbfa7799db1aec04d60f4f63479
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838729"
---
# <a name="dispatchflushbuffers-routines"></a>DispatchFlushBuffers 例程





驱动程序的[*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程为[**irp\_MJ\_FLUSH\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)I/o 函数代码处理 irp。 此 i/o 函数代码的驱动程序支持是可选的，但维护内部数据缓冲区的所有文件系统和筛选器驱动程序都必须处理它，以便在系统关闭时保留对文件数据或元数据的更改。 当缓冲数据需要刷新到磁盘时，i/o 管理器和其他操作系统组件以及其他内核模式驱动程序将发送此请求。 例如，在用户模式应用程序调用[**FlushFileBuffers**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-flushfilebuffers)时发送。

 

 




