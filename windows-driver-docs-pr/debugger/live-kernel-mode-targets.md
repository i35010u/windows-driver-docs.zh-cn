---
title: 实时内核模式目标
description: 实时内核模式目标
keywords:
- 目标，实时内核模式
- 内核模式目标
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b582f1a4b6fe5597af23f77fecce54b03233771
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806509"
---
# <a name="live-kernel-mode-targets"></a>实时内核模式目标


## <span id="ddk_live_kernel_mode_targets_dbx"></span><span id="DDK_LIVE_KERNEL_MODE_TARGETS_DBX"></span>


若要将 [调试器引擎](introduction.md#debugger-engine) 附加到目标计算机进行内核模式调试，请使用方法 [**AttachKernel**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-attachkernel)。

**注意**   在调用 [**WaitForEvent**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent) 方法之前，引擎不会完全附加到内核。 仅在内核生成事件（例如， [初始断点](initial-breakpoint.md) ）后，它才会在调试器会话中可用。 有关更多详细信息，请参阅 [调试会话和执行模型](debugging-session-and-execution-model.md) 。

 

如果将调试器引擎连接到非本地内核的内核，并且连接不是 eXDI 连接，则可以使用 [**GetKernelConnectionOptions**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-getkernelconnectionoptions)查询用于查找目标计算机的连接选项。 还可以重新同步连接，或使用 [**SetKernelConnectionOptions**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-setkernelconnectionoptions)更改连接速度。

调试器可以附加到本地内核，但只有在使用 **/debug** boot 开关启动计算机的情况下才可以连接到本地内核。  (在某些 Windows 安装中，当使用其他开关（如 **/debugport**）时，支持本地内核调试，但这不是 Windows 的保证功能，不应依赖。 ) [**IsKernelDebuggerEnabled**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-iskerneldebuggerenabled) 用于确定本地计算机是否可用于调试。 有关单个计算机上的内核调试的详细信息，请参阅 [执行本地内核调试](performing-local-kernel-debugging.md)。

 

