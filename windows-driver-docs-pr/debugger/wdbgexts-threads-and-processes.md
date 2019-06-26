---
title: WdbgExts 线程和进程
description: WdbgExts 线程和进程
ms.assetid: fa513435-ea91-4dc5-9488-85087d585f96
keywords:
- WdbgExts 扩展线程
- WdbgExts 扩展进程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: df35464621486bccbb32b1eea285ed2bf5540f5f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369418"
---
# <a name="wdbgexts-threads-and-processes"></a>WdbgExts 线程和进程


本主题提供概述的线程和进程可以是操作使用 WdbgExts API。 有关线程和进程中的概述[调试器引擎](introduction.md#debugger-engine)，请参阅[线程和进程](threads-and-processes.md)中[调试器引擎概述](debugger-engine-overview.md)此文档的部分。

### <a name="span-idthreadsspanspan-idthreadsspanthreads"></a><span id="threads"></span><span id="THREADS"></span>线程

若要获取描述当前线程的线程环境块 (TEB) 地址，请使用方法[ **GetTebAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-gettebaddress)。 在内核模式调试，KTHREAD 结构也是可用于描述一个线程。 返回此结构[ **GetCurrentThreadAddr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getcurrentthreadaddr) (在用户模式下调试中， **GetCurrentThreadAddr**返回 TEB 地址)。

[线程上下文](scopes-and-symbol-groups.md#thread-context)通过保留状态切换时的 Windows 线程; 它由上下文结构表示。 此结构因操作系统而异，并使用上下文结构时，应采取平台和护理。 返回的线程上下文[ **GetContext** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545736(v=vs.85))函数，可使用设置[ **SetContext** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556644(v=vs.85))函数。

若要检查当前线程的堆栈跟踪，请使用[ **StackTrace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_stacktrace_routine)函数。 若要暂时更改用于检查堆栈跟踪的线程，请使用[ **SetThreadForOperation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-setthreadforoperation)或[ **SetThreadForOperation64** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-setthreadforoperation64)函数。 请参阅[检查堆栈跟踪](examining-the-stack-trace.md)中[使用调试器引擎 API](using-the-debugger-engine-api.md)有关检查堆栈的其他方法的此文档的部分。

若要在目标中获取有关操作系统线程的信息，请使用[ **Ioctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[ **IG\_获取\_线程\_OS\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_wdbgexts_thread_os_info)。

### <a name="span-idprocessesspanspan-idprocessesspanprocesses"></a><span id="processes"></span><span id="PROCESSES"></span>进程

若要获取描述当前进程环境块 (PEB) 地址进程使用方法[ **GetPebAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getpebaddress)。 在内核模式调试，KPROCESS 结构也是可用于描述流程。 返回此结构[ **GetCurrentProcessAddr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getcurrentprocessaddr) (在用户模式下调试中， **GetCurrentProcessAddr**返回 PEB 的地址)。

该方法[ **GetCurrentProcessHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects-getcurrentprocesshandle)返回当前进程的系统句柄。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

功能更强大的线程操作和的过程操作 API，请参阅[控制线程和进程](controlling-threads-and-processes.md)中[使用调试器引擎 API](using-the-debugger-engine-api.md)此文档的部分。

 

 





