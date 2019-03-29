---
title: 调试器引擎 API 概述
description: 调试器引擎 API 概述
ms.assetid: ea8beca6-93b7-4537-af89-78d599b8b982
keywords:
- 调试器引擎 API 概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60d52f3aad2e0363ddba3ad23a1cad7cd46f7cb7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567115"
---
# <a name="debugger-engine-api-overview"></a>调试器引擎 API 概述


## <span id="ddk_debugger_engine_overview_dbx"></span><span id="DDK_DEBUGGER_ENGINE_OVERVIEW_DBX"></span>


本部分包括：

[与引擎进行交互](interacting-with-the-engine.md)

[使用输入和输出](using-input-and-output.md)

[监视事件](monitoring-events.md)

[使用断点](using-breakpoints2.md)

[内存访问](memory-access.md)

[检查堆栈跟踪](examining-the-stack-trace.md)

[控制线程和进程](controlling-threads-and-processes.md)

[使用符号](using-symbols.md)

[使用源代码文件](using-source-files.md)

[连接到目标](connecting-to-targets.md)

[目标信息](target-information.md)

[目标状态](target-state.md)

[调用扩展和扩展函数](calling-extensions-and-extension-functions.md)

[组装和拆装功能说明](assembling-and-disassembling-instructions.md)

**重要**  IDebug\*接口如[ **IDebugEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff550550)接口，尽管类似，COM 不是正确的 COM Api。 从托管代码中调用这些接口是一个不受支持的方案。 如果使用托管代码调用的接口，例如垃圾回收和线程所有权的问题会导致系统不稳定。

 

 

 





