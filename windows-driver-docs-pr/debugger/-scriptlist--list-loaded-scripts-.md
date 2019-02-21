---
title: .scriptlist （列出已加载的脚本）
description: .Scriptlist 命令将列出已加载的脚本。
ms.assetid: 98F24BE6-3F34-44E7-9546-3D5AB6D521DD
keywords:
- .scriptlist （列出已加载的脚本） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptlist (List Loaded Scripts)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 85dba9f144d77400de63d6ba9b15f414d4c6ffb3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547416"
---
# <a name="scriptlist-list-loaded-scripts"></a>.scriptlist （列出已加载的脚本）


**.Scriptlist**命令将列出已加载的脚本。

```dbgcmd
.scriptlist 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______________"></span>    
无

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

.Scriptlist 命令将列出已加载通过.scriptload 命令的任何脚本。

如果 TestScript 已成功加载使用.scriptload，.scriptlist 命令将显示加载的脚本的名称。

```dbgcmd
0:000> .scriptlist
Command Loaded Scripts:
    JavaScript script from 'C:\WinDbg\Scripts\TestScript.js'
```

**要求**

在使用之前的任何.script 命令，脚本编写提供程序需要加载。 使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令，可以加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[脚本编写的 JavaScript 调试器](javascript-debugger-scripting.md)

[**.scriptload （负载脚本）**](-scriptload--load-script-.md)

 

 






