---
title: 目标信息
description: 目标信息
ms.assetid: e818c0bb-ba91-4752-8baf-00fff759106f
keywords:
- 调试器引擎 API、 目标、 信息
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce9c2e26978decf117de974df89ff601ceaf7bd4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366354"
---
# <a name="target-information"></a>目标信息


该方法[ **GetDebuggeeType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getdebuggeetype)返回的性质的当前目标 （例如，是内核模式或用户模式下的目标），以及如何[调试器引擎](introduction.md#debugger-engine)是连接到它。

如果目标是崩溃转储文件文件，该方法[ **GetDumpFormatFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getdumpformatflags)将指示哪些信息包含在转储。

### <a name="span-idtargetscomputerspanspan-idtargetscomputerspantargets-computer"></a><span id="target_s_computer"></span><span id="TARGET_S_COMPUTER"></span>目标的计算机

返回目标的计算机的页面大小[ **GetPageSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getpagesize)。 [**IsPointer64Bit** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-ispointer64bit)将指示计算机是否使用了 32 位或 64 位地址。

**请注意**  在内部，调试器引擎始终使用 64 位地址的目标。 如果目标只使用 32 位地址，该引擎将自动转换它们与目标进行通信时。

 

将返回目标的计算机中的处理器数[ **GetNumberProcessors**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumberprocessors)。

有三个不同的处理器类型与目标计算机相关联：

-   *实际处理器类型*是目标计算机中物理处理器的类型。 这由返回[ **GetActualProcessorType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getactualprocessortype)。

-   *执行的处理器类型*是当前正在执行的处理器上下文中使用的处理器的类型。 这由返回[ **GetExecutingProcessorType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getexecutingprocessortype)。

-   *有效的处理器类型*是处理器的类型，例如解释来自目标-信息、 设置断点、 访问寄存器中，以及获取堆栈跟踪时，调试器使用。 返回有效的处理器类型[ **GetEffectiveProcessorType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-geteffectiveprocessortype) ，可以使用更改[ **SetEffectiveProcessorType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-seteffectiveprocessortype).

有效的处理器类型和正在执行的处理器类型可能不同于实际处理器类型-例如，当物理处理器 x64 处理器，并且它正在 x86 模式。

返回不同的执行处理器类型支持的目标的计算机上的物理处理器[ **GetPossibleExecutingProcessorTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getpossibleexecutingprocessortypes)。 返回多个[ **GetNumberPossibleExecutingProcessorTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumberpossibleexecutingprocessortypes)。

返回由调试器引擎支持的处理器类型列表[ **GetSupportedProcessorTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getsupportedprocessortypes)。 返回支持的处理器类型数[ **GetNumberSupportedProcessorTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumbersupportedprocessortypes)。

处理器类型的名称 （完整和缩写） 由[ **GetProcessorTypeNames**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getprocessortypenames)。

返回目标的计算机上的当前时间[ **GetCurrentTimeDate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getcurrenttimedate)。 时间长度的目标计算机已经运行了由于返回上一次启动[ **GetCurrentSystemUpTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getcurrentsystemuptime)。 时间信息可能不可用的所有目标。

### <a name="span-idtargetversionsspanspan-idtargetversionsspantarget-versions"></a><span id="target_versions"></span><span id="TARGET_VERSIONS"></span>目标版本

返回目标的计算机上运行的 Windows 版本[ **GetSystemVersionValues** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getsystemversionvalues)并[**请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugadvanced3-request)操作[**调试\_请求\_获取\_WIN32\_主要\_次要\_版本**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-request-get-win32-major-minor-versions)，和描述Windows 版本返回的[ **GetSystemVersionString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getsystemversionstring)。 其中某些信息也会返回[ **GetSystemVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getsystemversion)。

 

 





