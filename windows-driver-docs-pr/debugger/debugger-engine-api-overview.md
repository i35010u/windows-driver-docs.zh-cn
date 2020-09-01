---
title: 调试器引擎 API 概述
description: 调试器引擎 API 概述
ms.assetid: ea8beca6-93b7-4537-af89-78d599b8b982
keywords:
- 调试器引擎 API，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 411fd2a59420cefd26c85e9d5598a2e19d2b1d73
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211195"
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

**重要提示**   IDebug \* 接口（如 COM like）不是正确的 Com api，如[**IDebugEventCallbacks**](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks)接口。 从托管代码调用这些接口是不受支持的方案。 当通过托管代码调用这些接口时，会导致系统不稳定的问题，例如垃圾回收和线程所有权。

 

 

