---
title: Kernel-Mode 扩展
description: Kernel-Mode 扩展
keywords:
- 扩展命令 ( 命令) 、内核模式扩展
- 'kdextx86.dll (内核模式扩展) '
- 'kdexts.dll (内核模式扩展) '
- 'kext.dll (内核模式扩展) '
- '内核模式扩展 (kdext 和 kext.dll) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f13459b28aaef4c1f04c56b53f2231e7c2b72c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840833"
---
# <a name="kernel-mode-extensions"></a>Kernel-Mode 扩展


## <span id="ddk_kernel_mode_extensions_dbg"></span><span id="DDK_KERNEL_MODE_EXTENSIONS_DBG"></span>


本参考部分介绍了在内核模式调试过程中主要使用的扩展命令。

调试器将自动加载这些扩展命令的正确版本。 除非您手动加载了不同的版本，否则您不必跟踪所使用的 DLL 版本。 有关默认模块搜索顺序的说明，请参阅 [使用调试器扩展命令](using-debugger-extension-commands.md) 。 有关如何加载扩展模块的说明，请参阅 [加载调试器扩展 dll](loading-debugger-extension-dlls.md) 。

每个扩展命令参考页都列出了公开该命令的 Dll。 使用以下规则来确定要从中加载此扩展 DLL 的正确目录：

-   如果目标计算机运行的是 Windows XP 或更高版本的 Windows，请使用 winxp \\Kdexts.dll。

此外，还可以在 winextkext.dll 中找到不特定于任何单个操作系统的内核模式扩展 \\ 。

 

 





