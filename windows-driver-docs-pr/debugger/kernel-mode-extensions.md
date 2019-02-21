---
title: 内核模式下扩展
description: 内核模式下扩展
ms.assetid: e8e1e692-d991-427f-a2e7-b9eb1893fe83
keywords:
- 扩展命令 （命令），内核模式下扩展
- kdextx86.dll （内核模式扩展）
- kdexts.dll （内核模式扩展）
- kext.dll （内核模式扩展）
- 内核模式扩展 （kdext.dll 和 kext.dll）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c61a97b92cb83e2a304bdfc7d4300eb415cdb87f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521724"
---
# <a name="kernel-mode-extensions"></a>内核模式下扩展


## <span id="ddk_kernel_mode_extensions_dbg"></span><span id="DDK_KERNEL_MODE_EXTENSIONS_DBG"></span>


引用的本部分介绍主要用于在内核模式调试期间的扩展命令。

调试器将自动加载这些扩展命令的正确版本。 除非你已手动将加载不同版本，您无需跟踪的正在使用的 DLL 版本。 请参阅[使用调试器扩展命令](using-debugger-extension-commands.md)有关默认模块搜索顺序的说明。 请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)有关如何加载扩展模块的说明。

每个扩展命令参考页列出了公开该命令的 Dll。 使用以下规则来确定要从其加载此扩展 DLL 的正确目录：

-   如果目标计算机正在运行 Windows XP 或更高版本的 Windows，使用 winxp\\Kdexts.dll。

此外，winext 中找不到任何单个的操作系统特定的内核模式扩展\\kext.dll。

 

 





