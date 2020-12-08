---
title: .scriptproviders（列出脚本提供程序）
description: Scriptproviders 命令列出活动脚本提供程序。
keywords:
- scriptproviders (列出) Windows 调试的脚本提供程序
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptproviders (List Script Providers)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bbb0d3fcab79f259d26f49158ca6cdec02f1ef3d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791665"
---
# <a name="scriptproviders-list-script-providers"></a>.scriptproviders（列出脚本提供程序）


**Scriptproviders** 命令列出活动脚本提供程序。

```dbgcmd
.scriptproviders 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


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
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

Scriptproviders 命令将列出调试器当前可以理解的所有脚本语言及其注册的扩展。 以 "结尾的任何文件。NatVis "被理解为 NatVis 脚本，以" .js "结尾的任何文件都理解为 JavaScript 脚本。 可以通过 scriptload 命令加载任意一种类型的脚本。

在下面的示例中，加载了 JavaScript 和 NatVis 提供程序。

```dbgcmd
0:000> .scriptproviders
Available Script Providers:
    NatVis (extension '.NatVis')
    JavaScript (extension '.js')
```

**惠?**

使用任何脚本命令之前，需要加载脚本提供程序。 使用 [**load (负载扩展 DLL)**](-load---loadby--load-extension-dll-.md) 命令加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[JavaScript 调试器脚本](javascript-debugger-scripting.md)

[**.scriptload（加载脚本）**](-scriptload--load-script-.md)

 

 






