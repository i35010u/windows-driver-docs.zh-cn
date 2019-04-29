---
title: 常规扩展
description: 常规扩展
ms.assetid: 99ff4111-9f65-4e3d-beb3-0aa49f35a015
keywords:
- 扩展命令 （命令） 常规扩展
- exts.dll （常规扩展）
- dbghelp.dll （常规扩展）
- 常规扩展 (exts.dll-dbghelp.dll)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a77af36b80803c529eafaf0dc865cce09df67290
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380199"
---
# <a name="general-extensions"></a>常规扩展


## <span id="ddk_general_extensions_dbg"></span><span id="DDK_GENERAL_EXTENSIONS_DBG"></span>


本部分介绍在用户模式和内核模式调试期间经常使用的扩展命令。

调试器会自动加载这些扩展命令的正确版本。 除非你已手动将加载不同版本，您无需跟踪的正在使用的 DLL 版本。 有关默认模块搜索顺序的详细信息，请参阅[使用调试器扩展命令](using-debugger-extension-commands.md)。 有关如何加载扩展模块的详细信息，请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)。

每个扩展命令参考主题列出了公开该命令的 Dll。 使用以下规则来确定要加载此扩展 DLL 的正确目录中：

-   如果目标计算机正在运行 Microsoft Windows XP 或更高版本的 Windows，使用 winxp\\kdexts.dll、 winxp\\ntsdexts.dll、 winxp\\exts.dll、 winext\\ext.dll 或 dbghelp.dll。

 

 





