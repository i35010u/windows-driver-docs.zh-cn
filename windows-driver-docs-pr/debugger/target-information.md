---
title: 目标信息
description: 目标信息
ms.assetid: e818c0bb-ba91-4752-8baf-00fff759106f
keywords:
- 调试器引擎 API、目标、信息
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ed93e2ef996d526cc9d34ac5e465c278bd361d0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218189"
---
# <a name="target-information"></a>目标信息


方法 [**GetDebuggeeType**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getdebuggeetype) 返回当前目标 (的性质，例如，是指内核模式或用户模式目标) ，以及 [调试器引擎](introduction.md#debugger-engine) 如何连接到该目标。

如果目标是故障转储文件文件，则方法 [**GetDumpFormatFlags**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getdumpformatflags) 将指示转储中包含的信息。

### <a name="span-idtarget_s_computerspanspan-idtarget_s_computerspantargets-computer"></a><span id="target_s_computer"></span><span id="TARGET_S_COMPUTER"></span>目标计算机

[**GetPageSize**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getpagesize)返回目标计算机的页面大小。 [**IsPointer64Bit**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-ispointer64bit) 将指示计算机使用32位还是64位地址。

**注意**   在内部，调试器引擎始终对目标使用64位地址。 如果目标仅使用32位地址，则当与目标通信时，引擎将自动对其进行转换。

 

[**GetNumberProcessors**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumberprocessors)返回目标计算机中的处理器数。

有三种不同的处理器类型与目标计算机关联：

-   *实际的处理器类型*是目标计算机中物理处理器的类型。 这由 [**GetActualProcessorType**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getactualprocessortype)返回。

-   *执行处理器类型*是当前正在执行的处理器上下文中使用的处理器的类型。 这由 [**GetExecutingProcessorType**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getexecutingprocessortype)返回。

-   *有效的处理器类型*是调试器在解释目标中的信息时使用的处理器类型，例如，设置断点、访问寄存器和获取堆栈跟踪。 有效的处理器类型由 [**GetEffectiveProcessorType**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-geteffectiveprocessortype) 返回，可使用 [**SetEffectiveProcessorType**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-seteffectiveprocessortype)进行更改。

有效的处理器类型和执行处理器类型可能不同于实际的处理器类型，例如，当物理处理器是 x64 处理器并且它在 x86 模式下运行时。

[**GetPossibleExecutingProcessorTypes**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getpossibleexecutingprocessortypes)返回了目标计算机上的物理处理器支持的不同的执行处理器类型。 [**GetNumberPossibleExecutingProcessorTypes**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumberpossibleexecutingprocessortypes)返回这些值的数量。

[**GetSupportedProcessorTypes**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getsupportedprocessortypes)返回由调试器引擎支持的处理器类型。 [**GetNumberSupportedProcessorTypes**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnumbersupportedprocessortypes)返回受支持的处理器类型。

[**GetProcessorTypeNames**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getprocessortypenames)将返回名称 (完全和缩写) 处理器类型。

[**GetCurrentTimeDate**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getcurrenttimedate)返回目标计算机上的当前时间。 自上次启动以来目标计算机运行的时间长度由 [**GetCurrentSystemUpTime**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getcurrentsystemuptime)返回。 对于所有目标，时间信息可能不可用。

### <a name="span-idtarget_versionsspanspan-idtarget_versionsspantarget-versions"></a><span id="target_versions"></span><span id="TARGET_VERSIONS"></span>目标版本

在目标计算机上运行的 Windows 版本由 [**GetSystemVersionValues**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getsystemversionvalues) 和 [**请求**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-request) 操作 [**调试 \_ 请求 \_ 获取 \_ WIN32 \_ 主要 \_ 次要 \_ 版本**](debug-request-get-win32-major-minor-versions.md)返回，windows 版本的说明由 [**GetSystemVersionString**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getsystemversionstring)返回。 此信息也由 [**GetSystemVersion**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getsystemversion)返回。

 

