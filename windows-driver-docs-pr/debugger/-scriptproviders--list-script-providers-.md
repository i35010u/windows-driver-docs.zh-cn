---
title: .scriptproviders（列出脚本提供程序）
description: .Scriptproviders 命令列出了活动脚本提供程序。
ms.assetid: DF2FAA60-422F-4600-9E31-0F8EF127E5A9
keywords:
- .scriptproviders （列表脚本提供程序） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptproviders (List Script Providers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ba9ca106317d4f116e36222d75909f51d5f94a4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339845"
---
# <a name="scriptproviders-list-script-providers"></a>.scriptproviders（列出脚本提供程序）


**.Scriptproviders**命令列出了活动脚本提供程序。

```dbgcmd
.scriptproviders 
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

.Scriptproviders 命令将列出其目前能够理解的调试器，并在其下它们要注册的扩展的脚本语言。 以结尾的任何文件"。NatVis"理解为 NatVis 脚本并以".js"结尾的任何文件理解为 JavaScript 脚本。 可以使用.scriptload 命令加载任一类型的脚本。

在下面的示例中，将加载的 JavaScript 和 NatVis 提供程序。

```dbgcmd
0:000> .scriptproviders
Available Script Providers:
    NatVis (extension '.NatVis')
    JavaScript (extension '.js')
```

**要求**

在使用之前的任何.script 命令，脚本编写提供程序需要加载。 使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令，可以加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[JavaScript 调试器脚本](javascript-debugger-scripting.md)

[**.scriptload （负载脚本）**](-scriptload--load-script-.md)

 

 






