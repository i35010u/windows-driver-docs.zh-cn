---
title: .scriptrun（运行脚本）
description: Scriptrun 命令将加载并运行 JavaScript。
keywords:
- scriptrun (运行脚本) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptrun (Run Script)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c771872be88081714763b324f9174635b49394ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793325"
---
# <a name="scriptrun-run-script"></a>.scriptrun（运行脚本）


Scriptrun 命令将加载并运行 JavaScript。

```dbgcmd
.scriptrun ScriptFile  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______ScriptFile______"></span><span id="_______scriptfile______"></span><span id="_______SCRIPTFILE______"></span>*ScriptFile*   
指定要加载和执行的脚本文件的名称。 *ScriptFile* 应包含 .js 文件扩展名。 可以使用绝对路径或相对路径。 相对路径是相对于在其中启动调试器的目录的相对路径。 不支持包含空格的文件路径。

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

Scriptrun 命令将加载脚本并执行以下代码。

-   根
-   intializeScript
-   invokeScript

当加载并执行代码时，将显示一条确认消息。

```dbgcmd
0:000> .scriptrun C:\WinDbg\Scripts\helloWorld.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\helloWorld.js'
Hello World!  We are in JavaScript!
```

脚本所执行的任何对象模型操作都将保持不变，直到脚本随后被卸载或再次使用不同内容运行。

下表汇总了由 scriptload 和. scriptrun 执行的函数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><strong><a href="-scriptload--load-script-.md" data-raw-source="[.scriptload](-scriptload--load-script-.md)">.scriptload</a></strong></td>
<td align="left"><strong>.scriptrun</strong></td>
</tr>
<tr class="even">
<td align="left">根</td>
<td align="left">是</td>
<td align="left">是</td>
</tr>
<tr class="odd">
<td align="left">initializeScript</td>
<td align="left">是</td>
<td align="left">是</td>
</tr>
<tr class="even">
<td align="left">invokeScript</td>
<td align="left"></td>
<td align="left">是</td>
</tr>
<tr class="odd">
<td align="left">uninitializeScript</td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>



您可以使用此代码来查看通过. 脚本运行命令调用的函数。

```dbgcmd
// Root of Script
host.diagnostics.debugLog("***>; Code at the very top (root) of the script is always run \n");


function initializeScript()
{
    // Add code here that you want to run every time the script is loaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("**_>; initializeScript was called \n");
}

function invokeScript()
{
    // Add code here that you want to run every time the script is executed. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("_*_>; invokeScript was called \n");
}
```

有关使用 JavaScript 的详细信息，请参阅 [Javascript 调试器脚本](javascript-debugger-scripting.md)。 有关调试器对象的详细信息，请参阅 [JavaScript 扩展中的本机对象](native-objects-in-javascript-extensions.md)。

_ *要求**

使用任何脚本命令之前，需要加载脚本提供程序。 使用 [**load (负载扩展 DLL)**](-load---loadby--load-extension-dll-.md) 命令加载 JavaScript 提供程序 dll。

```dbgcmd
0:000> .load C:\ScriptProviders\jsprovider.dll
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**.scriptload（加载脚本）**](-scriptload--load-script-.md)

[JavaScript 调试器脚本](javascript-debugger-scripting.md)










