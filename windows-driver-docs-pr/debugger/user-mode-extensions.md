---
title: User-Mode 扩展
description: User-Mode 扩展
keywords:
- 扩展命令 ( 命令) 、用户模式扩展
- 'ntsdexts.dll (用户模式扩展) '
- 'uext.dll (用户模式扩展) '
- '用户模式扩展 ( # A0 和 uext.dll) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05d55202536badd0c0cc13951a0c40c1a20848c1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803211"
---
# <a name="user-mode-extensions"></a>User-Mode 扩展


## <span id="ddk_user_mode_extensions_dbg"></span><span id="DDK_USER_MODE_EXTENSIONS_DBG"></span>


本参考部分介绍了主要在用户模式调试过程中使用的扩展命令。

调试器将自动加载这些扩展命令的正确版本。 除非您手动加载了不同的版本，否则您不必跟踪所使用的 DLL 版本。 有关默认模块搜索顺序的说明，请参阅 [使用调试器扩展命令](using-debugger-extension-commands.md) 。 有关如何加载扩展模块的说明，请参阅 [加载调试器扩展 dll](loading-debugger-extension-dlls.md) 。

每个扩展命令参考页都列出了公开该命令的 Dll。 使用以下规则来确定要从中加载此扩展 DLL 的正确目录：

-   如果目标应用程序运行在 Windows XP 或更高版本的 Windows 上，请使用 winxp \\Ntsdexts.dll。

此外，还可以在 winextUext.dll 中找到不特定于任何单个操作系统的用户模式扩展 \\ 。

 

 





