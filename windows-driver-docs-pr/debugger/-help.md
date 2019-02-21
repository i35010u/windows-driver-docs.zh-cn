---
title: help
description: 帮助扩展显示介绍从扩展 DLL 导出的扩展命令的帮助文本。
ms.assetid: 9d01856e-4906-43cb-a445-71cce011a973
keywords:
- Windows 调试帮助
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- help
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b22a2d256a9ae0ee36489dd2704c1fde5788cbe6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541759"
---
# <a name="help"></a>！ 帮助


**！ 帮助**扩展显示介绍从扩展 DLL 导出的扩展命令的帮助文本。

请不要将此扩展命令混淆[ **？（命令帮助）** ](---command-help-.md)或[ **.help 获取 （Meta-Command 帮助）** ](-help--meta-command-help-.md)命令。

```dbgcmd
![ExtensionDLL.]help [-v] [CommandName] 
```

## <a name="span-idddkhelpdbgspanspan-idddkhelpdbgspanparameters"></a><span id="ddk__help_dbg"></span><span id="DDK__HELP_DBG"></span>参数


<span id="_______ExtensionDLL______"></span><span id="_______extensiondll______"></span><span id="_______EXTENSIONDLL______"></span> *ExtensionDLL*   
显示指定的扩展 DLL 的帮助。 键入不带.dll 文件扩展名对扩展 DLL 的名称。 如果 DLL 文件不在扩展搜索路径中 (通过使用所示[ **.chain （列表调试器扩展）**](-chain--list-debugger-extensions-.md))，包括 DLL 文件的路径。 例如，若要显示 uext.dll 的帮助，请键入 **！ uext.help**或 **！**<em>路径</em>**\\winext\\uext.help**。

如果省略*ExtensionDLL*，调试器将显示加载的 Dll 的列表中的第一个扩展 DLL 的帮助文本。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
显示的最详细的帮助文本。 在所有 Dll 中不支持此功能。

<span id="_______CommandName______"></span><span id="_______commandname______"></span><span id="_______COMMANDNAME______"></span> *CommandName*   
显示仅为指定的命令的帮助文本。 中的所有 Dll 或所有命令，不支持此功能。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展支持大多数扩展 Dll。

<a name="remarks"></a>备注
-------

某些个人命令还显示帮助文本，如果将使用 **/？** 或 **-？** 使用命令名称的参数。

 

 





