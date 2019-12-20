---
title: 使用调试器扩展命令
description: 使用调试器扩展命令
ms.assetid: 1db9a835-accb-41b9-9ab1-c4c9f0596aa5
keywords:
- 扩展命令（命令），使用
- 扩展命令（命令），默认搜索顺序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 422998f608ed896d9efb7096f874836ab5eed69b
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209673"
---
# <a name="using-debugger-extension-commands"></a>使用调试器扩展命令


## <span id="ddk_using_debugger_extension_commands_dbg"></span><span id="DDK_USING_DEBUGGER_EXTENSION_COMMANDS_DBG"></span>


调试器扩展命令的使用与[调试程序命令](using-debugger-commands.md)的使用非常相似。 命令在调试器命令窗口中键入，在此窗口中生成输出或在目标应用程序或目标计算机中生成更改。

实际的调试器扩展命令是调试器调用的 DLL 中的入口点。

调试器扩展通过以下语法调用：

**！\[** <em>module</em>**\]**<em>扩展</em> **\[**<em>参数</em>**\]**

模块名称后面不应跟 .dll 文件扩展名。 如果*module*包含完整路径，则默认字符串大小限制为255个字符。

如果尚未加载该模块，则使用对**LoadLibrary**（*模块*）的调用将其加载到调试器中。 调试器加载扩展库后，它将调用**GetProcAddress**函数以查找扩展模块中的扩展名称。 扩展名区分大小写，并且必须与扩展模块的 .def 文件中显示的内容完全相同。 如果找到扩展地址，则调用该扩展插件。

### <a name="span-idsearch_orderspanspan-idsearch_orderspansearch-order"></a><span id="search_order"></span><span id="SEARCH_ORDER"></span>搜索顺序

如果未指定模块名称，则调试器将在加载的扩展模块中搜索此导出。

默认搜索顺序如下所示：

1.  适用于所有操作系统和两种模式下的扩展模块： Dbghelp.dll 和 winext\\ext。

2.  在所有模式下工作，但特定于操作系统的扩展模块。 对于 Windows XP 和更高版本的 Windows，这是 winxp\\exts。 

3.  适用于所有操作系统但特定于模式的扩展模块。 对于内核模式，这是 winext\\kext。 对于用户模式，这是 winext\\uext。

4.  既是操作系统特定的又是模式特定的扩展模块。 下表指定了此模块。

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
    <td align="left"><p>winxp \ ntsdexts</p></td>
    <td align="left"><p>winxp \ kdexts</p></td>
    </tr>
    </tbody>
    </table>

     

卸载扩展模块时，将从搜索链中删除该模块。 加载扩展模块时，它将添加到搜索顺序的开头。 可以使用[**setdll （Set Default EXTENSION DLL）**](-setdll--set-default-extension-dll-.md)命令将任何模块提升到搜索链的顶部。 通过重复使用此命令，您可以完全控制搜索链。

使用 "[**链（列出调试器扩展）**](-chain--list-debugger-extensions-.md) " 命令可按当前搜索顺序显示所有加载的扩展模块的列表。

如果你尝试执行不在任何已加载的扩展模块中的扩展命令，你将收到 "找不到导出" 错误消息。

 

 





