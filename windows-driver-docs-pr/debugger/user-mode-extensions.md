---
title: 用户模式下扩展
description: 用户模式下扩展
ms.assetid: 83b0aca1-ad08-4384-a035-3d7bd2c1b4fe
keywords:
- 扩展命令 （命令），用户模式下扩展
- ntsdexts.dll （用户模式下扩展）
- uext.dll （用户模式下扩展）
- 用户模式扩展 （ntsdexts.dll 和 uext.dll）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ff392e2c863b60ef2d81d4037929743688814c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576079"
---
# <a name="user-mode-extensions"></a>用户模式下扩展


## <span id="ddk_user_mode_extensions_dbg"></span><span id="DDK_USER_MODE_EXTENSIONS_DBG"></span>


引用的本部分介绍主要用于在用户模式下调试期间的扩展命令。

调试器将自动加载这些扩展命令的正确版本。 除非你已手动将加载不同版本，您无需跟踪的正在使用的 DLL 版本。 请参阅[使用调试器扩展命令](using-debugger-extension-commands.md)有关默认模块搜索顺序的说明。 请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)有关如何加载扩展模块的说明。

每个扩展命令参考页列出了公开该命令的 Dll。 使用以下规则来确定要从其加载此扩展 DLL 的正确目录：

-   如果目标应用程序正在运行 Windows XP 或更高版本的 Windows 上，使用 winxp\\Ntsdexts.dll。

此外，winext 中找不到任何单个的操作系统特定的用户模式下扩展\\Uext.dll。

 

 





