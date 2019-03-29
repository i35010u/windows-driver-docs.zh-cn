---
title: DispatchFlushBuffers 例程
description: DispatchFlushBuffers 例程
ms.assetid: 091ce55c-e867-4ba4-aa25-5c20af45d9c2
keywords:
- 调度例程 WDK 内核，DispatchFlushBuffers 例程
- DispatchFlushBuffers 例程
- IRP_MJ_FLUSH_BUFFERS I/O 函数代码
- 刷新缓冲区调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd86d4df9599650081cb55913e94fa53249dd728
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565265"
---
# <a name="dispatchflushbuffers-routines"></a>DispatchFlushBuffers 例程





驱动程序的[ *DispatchFlushBuffers* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程处理的 Irp [ **IRP\_MJ\_刷新\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff550760) I/O 函数代码。 此 I/O 函数代码的驱动程序支持是可选的但所有文件系统和筛选器驱动程序的维护内部数据缓冲区必须都处理它在系统关闭之间保留对文件数据或元数据的更改。 此请求 I/O 管理器和其他操作系统组件，以及其他内核模式驱动程序时发送缓冲的数据需要刷新到磁盘。 例如，发送时在用户模式应用程序调用[ **FlushFileBuffers**](https://msdn.microsoft.com/library/windows/desktop/aa364439)。

 

 




