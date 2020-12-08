---
title: 加载调试器扩展 Dll
description: 加载调试器扩展 Dll
keywords:
- 扩展命令 ( 命令) ，加载
- 正在加载扩展命令
- nt4fre 目录
- nt4chk 目录
- w2kfre 目录
- w2kchk 目录
- winxp 目录
- winext 目录
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13a877c0221082ce6aa17fc19b5d5ad8a2fec0cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838165"
---
# <a name="loading-debugger-extension-dlls"></a>加载调试器扩展 Dll


## <span id="ddk_loading_debugger_extension_dlls_dbg"></span><span id="DDK_LOADING_DEBUGGER_EXTENSION_DLLS_DBG"></span>


有多种方法可加载调试器扩展 Dll，还可以控制默认调试器扩展 DLL 和默认调试器扩展路径：

-    (在启动调试器之前) 使用 \_ NT \_ 调试器 \_ 扩展 \_ 路径 [环境变量](environment-variables.md) 来设置扩展 dll 的默认路径。 这可以是多个目录路径，用分号分隔。

-   使用 [**load (负载扩展 DLL)**](-load---loadby--load-extension-dll-.md) 命令加载新的 DLL。

-   使用 [**unload (卸载扩展 dll)**](-unload--unload-extension-dll-.md) 命令卸载 DLL。

-   使用 [**.unloadall (卸载所有扩展 dll)**](-unloadall--unload-all-extension-dlls-.md) 命令以卸载所有调试器扩展。

-   在启动调试器之前 (;仅 CDB) 使用 [tools.ini](configuring-tools-ini.md) 文件设置默认扩展 DLL。

-    (在启动调试器之前) 使用 **-a** [命令行选项](command-line-options.md) 设置默认扩展 DLL。

-   使用 [**. extpath (设置扩展路径)**](-extpath--set-extension-path-.md) 命令设置扩展 DLL 搜索路径。

-   使用 [**. setdll (设置默认扩展 dll)**](-setdll--set-default-extension-dll-.md) 命令设置默认扩展插件 dll。

-   使用 [**链式 (List 调试器 extension)**](-chain--list-debugger-extensions-.md) 命令，以默认搜索顺序显示所有加载的调试器扩展模块。

还可以只使用 full **！**<em>模块</em>**。** 第一次从该模块发出命令时，<em>扩展</em>语法。 有关详细信息，请参阅 [使用调试器扩展命令](using-debugger-extension-commands.md) 。

你正在使用的扩展 Dll 必须与目标计算机的操作系统匹配。 随附于 Windows 的调试工具包附带的扩展 Dll 分别位于安装目录的不同子目录中：

-   Winxp 目录包含可用于 Windows XP 和更高版本的 Windows 的扩展。

-   Winext 目录包含可用于任何 Windows 版本的扩展。 dbghelp.dll 模块位于 Windows 调试工具的基目录中，也包含此类型的扩展。

如果你编写自己的调试器扩展，则可以将其放置在任何目录中。 但建议将其放在新目录中，并将该目录添加到调试器扩展路径。

最多可以加载32个扩展 Dll。

 

 





