---
title: 使用调试器扩展命令
description: 使用调试器扩展命令
ms.assetid: 1db9a835-accb-41b9-9ab1-c4c9f0596aa5
keywords:
- 扩展命令 （命令），请使用
- 扩展命令 （命令），默认的搜索顺序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5885e7900d7814f34e77949d64394da4feec5821
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371579"
---
# <a name="using-debugger-extension-commands"></a>使用调试器扩展命令


## <span id="ddk_using_debugger_extension_commands_dbg"></span><span id="DDK_USING_DEBUGGER_EXTENSION_COMMANDS_DBG"></span>


使用调试器扩展命令是非常类似于使用[调试器命令](using-debugger-commands.md)。 生成此窗口中的输出，或者目标应用程序或目标计算机中的更改在调试器命令窗口中，键入该命令。

实际的调试器扩展命令为中由调试器调用的 DLL 的入口点。

调试器扩展调用由以下语法：

**!\[** <em>模块</em>**。\]**<em>扩展</em> **\[**<em>参数</em>**\]**

模块名称不应遵循与.dll 文件扩展名。 如果*模块*包含完整路径，默认字符串大小限制为 255 个字符。

如果尚未加载该模块，它将加载到调试器通过调用**LoadLibrary**(*模块*)。 调试器已加载扩展插件库后，它会调用**GetProcAddress**函数来扩展模块中查找扩展插件名称。 扩展插件名称区分大小写，必须输入扩展模块的.def 文件中显示的样子。 如果找到扩展地址，则调用该扩展。

### <a name="span-idsearchorderspanspan-idsearchorderspansearch-order"></a><span id="search_order"></span><span id="SEARCH_ORDER"></span>搜索顺序

如果未指定模块名称，则调试器将搜索此导出的已加载的扩展模块。

默认的搜索顺序是按如下所示：

1.  适用于所有操作系统和在这两种模式中扩展模块：Dbghelp.dll 和 winext\\ext.dll。

2.  在所有模式下工作，但特定于操作系统的扩展模块。 对于 Windows XP 和更高版本的 Windows，这是 winxp\\exts.dll。 没有适用于 Windows 2000 相应模块。

3.  适用于所有操作系统，但特定于模式的扩展模块。 适用于内核模式，这是 winext\\kext.dll。 对于用户模式下，这是 winext\\uext.dll。

4.  是特定于操作系统的和特定于模式的扩展模块。 下表指定了此模块。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">用户模式</th>
    <th align="left">内核模式</th>
    </tr>
    </thead>
    <tbody>
    <tr class="even">
    <td align="left"><p>winxp \ ntsdexts.dll</p></td>
    <td align="left"><p>winxp \ kdexts.dll</p></td>
    </tr>
    </tbody>
    </table>

     

卸载扩展模块时，它是从搜索链中删除。 扩展模块加载时，它被添加到搜索顺序开始。 [ **.Setdll (设置默认的扩展 DLL)** ](-setdll--set-default-extension-dll-.md)命令可用于将提升到搜索链上的任何模块。 通过重复使用此命令，可以完全控制搜索链。

使用[ **.chain （列表调试器扩展）** ](-chain--list-debugger-extensions-.md)命令以在其当前的搜索顺序显示所有已加载的扩展模块的列表。

如果您尝试执行不在任何已加载的扩展模块的扩展命令，则会导出找不到错误消息。

 

 





