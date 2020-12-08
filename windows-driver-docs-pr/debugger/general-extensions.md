---
title: 常规扩展
description: 常规扩展
keywords:
- 扩展命令 ( 命令) ，一般扩展
- 'exts.dll (常规扩展) '
- 'dbghelp.dll (常规扩展) '
- '常规扩展 ( # A0-dbghelp.dll) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b3dca99fb25574a7c82e6b51b3f7f6af6da061b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822595"
---
# <a name="general-extensions"></a>常规扩展


## <span id="ddk_general_extensions_dbg"></span><span id="DDK_GENERAL_EXTENSIONS_DBG"></span>


本部分介绍在用户模式和内核模式调试过程中经常使用的扩展命令。

调试器会自动加载这些扩展命令的正确版本。 除非您手动加载了不同的版本，否则您不必跟踪正在使用的 DLL 版本。 有关默认模块搜索顺序的详细信息，请参阅 [使用调试器扩展命令](using-debugger-extension-commands.md)。 有关如何加载扩展模块的详细信息，请参阅 [加载调试器扩展 dll](loading-debugger-extension-dlls.md)。

每个扩展命令参考主题列出了公开该命令的 Dll。 使用以下规则来确定要从中加载此扩展 DLL 的适当目录：

-   如果目标计算机运行的是 Microsoft Windows XP 或更高版本的 Windows，请使用 winxp \\kdexts.dll、winxp \\ntsdexts.dll、winxp \\exts.dll、winext \\ext.dll 或 dbghelp.dll。

 

 





