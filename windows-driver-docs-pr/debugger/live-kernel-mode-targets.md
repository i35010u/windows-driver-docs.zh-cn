---
title: 实时内核模式目标
description: 实时内核模式目标
ms.assetid: 88820097-4a47-428d-88dd-d0a08e5debdc
keywords:
- 目标，实时内核模式
- 内核模式目标
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b34235579c9ab5ee99a5c21cc9dfcc99d599b41
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366489"
---
# <a name="live-kernel-mode-targets"></a>实时内核模式目标


## <span id="ddk_live_kernel_mode_targets_dbx"></span><span id="DDK_LIVE_KERNEL_MODE_TARGETS_DBX"></span>


若要将附加[调试器引擎](introduction.md#debugger-engine)到内核模式调试的目标计算机，使用该方法[ **AttachKernel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-attachkernel)。

**请注意**  引擎不会完全将附加到之前的内核[ **WaitForEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent)调用方法。 仅内核已生成事件-例如后,[初始断点](initial-breakpoint.md)-实际上它已成为网络在调试器会话中可用。 请参阅[调试会话和执行模型](debugging-session-and-execution-model.md)的更多详细信息。

 

如果连接不是 eXDI 连接调试器引擎附加到这不是本地的内核的内核，用于查找可以使用查询在目标计算机的连接选项[ **GetKernelConnectionOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getkernelconnectionoptions). 连接还可以重新同步或使用的连接速度更改[ **SetKernelConnectionOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-setkernelconnectionoptions)。

可将调试器附加到本地的内核，但仅在有限的方式且仅当计算机启动时 **/debug**启动开关。 (在某些 Windows 安装时，本地内核调试时，支持使用其他开关，如 **/debugport**，但这不是 Windows 的有保证的功能，并且不应依赖。)[**IsKernelDebuggerEnabled** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-iskerneldebuggerenabled)用于确定是否可用于调试在本地计算机。 详细了解内核调试在一台计算机，请参阅[执行本地内核调试](performing-local-kernel-debugging.md)。

 

 





