---
title: 调试器引擎概述
description: 调试器引擎概述
ms.assetid: e3cd8a1d-dd07-480b-bc3b-4f6acc647167
keywords:
- 调试器引擎
- 调试器引擎，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91652788469d68b3745b53fa8de00e752eb500eb
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211193"
---
# <a name="debugger-engine-overview"></a>调试器引擎概述


*调试器引擎* ( # A0) （通常称为*引擎*）提供了一个接口，用于在*用户模式下*检查调试目标并在 Microsoft Windows 上的*内核模式下*操作。

调试器引擎可以获取目标、设置 [断点](multiprocessor-syntax.md#breakpoints)、监视 [事件](events.md#events)、查询 [符号](symbols.md#symbols)、读取和写入内存，以及控制目标中的 [线程](controlling-threads-and-processes.md#threads) 和 [进程](controlling-threads-and-processes.md#processes) 。

您可以使用调试器引擎来编写调试器扩展库和独立应用程序。 此类应用程序称为 " *调试器引擎应用程序*"。 使用调试器引擎全部功能的调试器引擎应用程序称为 " *调试器*"。 例如，WinDbg、CDB、NTSD 和 KD 都是调试器;调试器引擎提供其功能的核心。

**引擎概念：**

[调试会话和执行模型](debugging-session-and-execution-model.md)

[客户端对象](client-objects.md)

[输入和输出](input-and-output.md)

**检查和操作目标：**

[目标](targets.md)

[事件](events.md)

[“断点”](breakpoints3.md)

[符号](symbols.md)

[内存](memory.md)

[线程和进程](threads-and-processes.md)

### <a name="span-idincomplete_documentationspanspan-idincomplete_documentationspanincomplete-documentation"></a><span id="incomplete_documentation"></span><span id="INCOMPLETE_DOCUMENTATION"></span>文档不完整

这是一个初步文档，当前不完整。

对于很多与调试器和调试器引擎相关的概念，此处未介绍这些概念，请参阅本文档的 [调试技术](debugging-techniques.md) 部分。

若要获取调试器引擎 API 的一些当前未记录的功能，请使用 [**execute**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-execute) 方法执行单个调试器命令。

 

