---
title: 调试器引擎 API 概述
description: 调试器引擎 API 概述
keywords:
- 调试器引擎 API，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: efed73846f11ff5a68f390946e22b7449de75dd9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788811"
---
# <a name="debugger-engine-api-overview"></a>调试器引擎 API 概述


## <span id="ddk_debugger_engine_overview_dbx"></span><span id="DDK_DEBUGGER_ENGINE_OVERVIEW_DBX"></span>


本节包括：

[与引擎交互](interacting-with-the-engine.md)

[使用输入和输出](using-input-and-output.md)

[监视事件](monitoring-events.md)

[使用断点](using-breakpoints2.md)

[内存访问](memory-access.md)

[检查堆栈跟踪](examining-the-stack-trace.md)

[控制线程和进程](controlling-threads-and-processes.md)

[使用符号](using-symbols.md)

[使用源文件](using-source-files.md)

[连接到目标](connecting-to-targets.md)

[目标信息](target-information.md)

[目标状态](target-state.md)

[调用扩展和扩展函数](calling-extensions-and-extension-functions.md)

[汇编和反汇编指令](assembling-and-disassembling-instructions.md)

**重要提示**  IDebug \* 接口（如 COM like）不是正确的 Com api，如 [**IDebugEventCallbacks**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks) 接口。 从托管代码调用这些接口是不受支持的方案。 当通过托管代码调用这些接口时，会导致系统不稳定的问题，例如垃圾回收和线程所有权。

 

 

