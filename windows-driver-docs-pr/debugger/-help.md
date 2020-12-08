---
title: help
description: 帮助扩展显示的帮助文本介绍了从扩展 DLL 导出的扩展命令。
keywords:
- 帮助 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- help
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 91442a69d29070c36c749b7c7900e674800cda8d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825845"
---
# <a name="help"></a>!help


**！ Help** extension 显示帮助文本，用于描述从扩展 DLL 导出的扩展命令。

请勿将此扩展命令与 [**？ (命令帮助)**](---command-help-.md) 或 [**。帮助 ()**](-help--meta-command-help-.md) 命令。

```dbgcmd
![ExtensionDLL.]help [-v] [CommandName] 
```

## <a name="span-idddk__help_dbgspanspan-idddk__help_dbgspanparameters"></a><span id="ddk__help_dbg"></span><span id="DDK__HELP_DBG"></span>参数


<span id="_______ExtensionDLL______"></span><span id="_______extensiondll______"></span><span id="_______EXTENSIONDLL______"></span>*ExtensionDLL*   
显示指定扩展 DLL 的帮助。 键入没有 .dll 文件扩展名的扩展 DLL 的名称。 如果 DLL 文件不在扩展搜索路径中 (如使用 [**(显示调试器扩展)**](-chain--list-debugger-extensions-.md)) 中所示，请包括 DLL 文件的路径。 例如，若要显示 uext.dll 的帮助，请键入 **！ uext。** **!**<em>Path</em>**\\ Winext \\ uext**。

如果省略 *ExtensionDLL*，则调试器将在加载的 dll 列表中显示第一个扩展 DLL 的帮助文本。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
显示最详细的可用帮助文本。 所有 Dll 都不支持此功能。

<span id="_______CommandName______"></span><span id="_______commandname______"></span><span id="_______COMMANDNAME______"></span>*CommandName*   
仅显示指定命令的帮助文本。 所有 Dll 或所有命令都不支持此功能。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

大多数扩展 Dll 都支持此扩展。

<a name="remarks"></a>备注
-------

如果使用 **/？** ，一些单独的命令也将显示帮助文本 或 **-？** 命令名为的参数。

 

 





