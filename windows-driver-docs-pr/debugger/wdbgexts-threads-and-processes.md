---
title: WdbgExts 线程和进程
description: WdbgExts 线程和进程
ms.assetid: fa513435-ea91-4dc5-9488-85087d585f96
keywords:
- WdbgExts 扩展，线程
- WdbgExts 扩展，进程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a91358ea509e05877a73597fa9dbdee8ca17e92
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209337"
---
# <a name="wdbgexts-threads-and-processes"></a>WdbgExts 线程和进程


本主题简要概述了如何使用 WdbgExts API 来操作线程和进程。 有关[调试器引擎](introduction.md#debugger-engine)中的线程和进程的概述，请参阅本文档的[调试器引擎概述](debugger-engine-overview.md)部分中的[线程和进程](threads-and-processes.md)。

### <a name="span-idthreadsspanspan-idthreadsspanthreads"></a><span id="threads"></span><span id="THREADS"></span>线程

若要获取线程环境块 (TEB) 描述当前线程的地址，请使用方法 [**GetTebAddress**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-gettebaddress)。 在内核模式调试中，还可以使用 KTHREAD 结构来描述线程。 此结构由 [**GetCurrentThreadAddr**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getcurrentthreadaddr) (在用户模式调试中返回， **GetCurrentThreadAddr** 返回 TEB) 的地址。

[线程上下文](scopes-and-symbol-groups.md#thread-context)是在切换线程时由 Windows 保留的状态;它由上下文结构表示。 此结构因操作系统和平台而异，使用上下文结构时应谨慎。 线程上下文由 [**GetContext**](/previous-versions/windows/hardware/previsioning-framework/ff545736(v=vs.85)) 函数返回，可使用 [**SetContext**](/previous-versions/windows/hardware/previsioning-framework/ff556644(v=vs.85)) 函数进行设置。

若要检查当前线程的堆栈跟踪，请使用 [**StackTrace**](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_stacktrace_routine) 函数。 若要临时更改用于检查堆栈跟踪的线程，请使用 [**SetThreadForOperation**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-setthreadforoperation) 或 [**SetThreadForOperation64**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-setthreadforoperation64) 函数。 有关检查堆栈的其他方法，请参阅本文档的[使用调试器引擎 API](using-the-debugger-engine-api.md) [检查堆栈跟踪](examining-the-stack-trace.md)部分。

若要获取有关目标中的操作系统线程的信息，请使用 [**Ioctl**](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine) 操作 [**IG \_ 获取 \_ 线程 \_ 操作系统 \_ 信息**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_wdbgexts_thread_os_info)。

### <a name="span-idprocessesspanspan-idprocessesspanprocesses"></a><span id="processes"></span><span id="PROCESSES"></span>工艺

若要获取进程环境块的地址 (PEB) 描述当前进程，请使用方法 [**GetPebAddress**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getpebaddress)。 在内核模式调试中，还可以使用 KPROCESS 结构来描述进程。 此结构由 [**GetCurrentProcessAddr**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getcurrentprocessaddr) (在用户模式调试中返回， **GetCurrentProcessAddr** 返回 PEB) 的地址。

方法 [**GetCurrentProcessHandle**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects-getcurrentprocesshandle) 返回当前进程的系统句柄。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关更强大的线程操作和处理操作 API，请参阅本文档中的[使用调试器引擎 API](using-the-debugger-engine-api.md) [控制线程和进程](controlling-threads-and-processes.md)部分。

 

