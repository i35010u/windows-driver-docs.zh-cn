---
title: 加载调试器扩展 Dll
description: 加载调试器扩展 Dll
ms.assetid: 6ca70732-cbf6-44fd-a020-c297b40d41f6
keywords:
- 正在加载扩展命令 （命令）
- 正在加载扩展命令
- nt4fre 目录
- nt4chk 目录
- w2kfre 目录
- w2kchk 目录
- winxp 目录
- winext 目录
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 923e30c897fb96983f7b78e9d265528c1d846690
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383332"
---
# <a name="loading-debugger-extension-dlls"></a>加载调试器扩展 Dll


## <span id="ddk_loading_debugger_extension_dlls_dbg"></span><span id="DDK_LOADING_DEBUGGER_EXTENSION_DLLS_DBG"></span>


有几种方法加载调试器扩展 Dll，以及控制默认调试器扩展 DLL 和默认调试器扩展路径：

-   （在之前启动调试器）使用\_NT\_调试器\_扩展\_路径[环境变量](environment-variables.md)设置扩展 Dll 的默认路径。 这可以是目录路径，之间用分号分隔的数字。

-   使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令以加载新 DLL。

-   使用[ **.unload (卸载扩展 DLL)** ](-unload--unload-extension-dll-.md)命令将其卸载 DLL。

-   使用[ **.unloadall (卸载所有扩展 Dll)** ](-unloadall--unload-all-extension-dlls-.md)命令将其卸载所有调试器扩展。

-   （在之前启动调试器;仅 CDB) 使用[tools.ini](configuring-tools-ini.md)文件以设置默认扩展插件 DLL。

-   （在之前启动调试器）使用 **-a** [命令行选项](command-line-options.md)设置默认扩展插件 DLL。

-   使用[ **.extpath （设置扩展路径）** ](-extpath--set-extension-path-.md)命令设置扩展 DLL 搜索路径。

-   使用[ **.setdll (设置默认扩展 DLL)** ](-setdll--set-default-extension-dll-.md)命令设置默认扩展插件 DLL。

-   使用[ **.chain （列表调试器扩展）** ](-chain--list-debugger-extensions-.md)命令以显示所有已加载的调试器扩展模块，其默认的搜索顺序。

您也可以只需通过使用完整加载扩展 DLL **！**<em>模块</em>**。**<em>扩展</em>语法第一次发出从该模块的命令。 请参阅[使用调试器扩展命令](using-debugger-extension-commands.md)有关详细信息。

扩展使用的 Dll 必须与目标计算机的操作系统匹配。 扩展 Dll 附带的 Windows 调试工具包每个不同的安装目录的子目录中放置：

-   Winxp 目录包含可以用于 Windows XP 和更高版本的 Windows 的扩展。

-   Winext 目录包含可用于任何版本的 Windows 的扩展。 有关 Windows 调试工具，在基目录中的 dbghelp.dll 模块还包含此类型的扩展。

如果您编写您自己的调试器扩展，可以将它们放在任何目录中。 但是，建议您将它们放在新目录，并将该目录添加到调试器扩展路径。

可以有多达 32 加载扩展 Dll。

 

 





