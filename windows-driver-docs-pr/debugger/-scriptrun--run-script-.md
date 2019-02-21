---
title: .scriptrun （运行脚本）
description: .Scriptrun 命令加载并运行 JavaScript。
ms.assetid: 6481B852-F0B4-4B02-BF7F-81DA21457A40
keywords:
- .scriptrun （运行脚本） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptrun (Run Script)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 97eeb3313a500ef90130631121f435701206973e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526437"
---
# <a name="scriptrun-run-script"></a>.scriptrun （运行脚本）


.Scriptrun 命令加载并运行 JavaScript。

```dbgcmd
.scriptrun ScriptFile  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______ScriptFile______"></span><span id="_______scriptfile______"></span><span id="_______SCRIPTFILE______"></span> *ScriptFile*   
指定要加载和执行的脚本文件的名称。 *ScriptFile*应包含的.js 文件扩展名。 可以使用绝对或相对路径。 相对路径是相对于目录中启动调试器。 不支持文件路径包含空格。

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

.Scriptrun 命令都将加载脚本，并执行下面的代码。

-   根
-   intializeScript
-   invokeScript

加载并执行代码时显示一条确认消息。

```dbgcmd
0:000> .scriptrun C:\WinDbg\Scripts\helloWorld.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\helloWorld.js'
Hello World!  We are in JavaScript!
```

脚本所做的任何对象模型操作将就地保留，直到该脚本随后卸载或重新运行具有不同的内容。

此表总结了由.scriptload 和.scriptrun 执行哪些功能。

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



此代码可用于查看与运行命令.script 调用的函数。

```dbgcmd
// Root of Script
host.diagnostics.debugLog("***>; Code at the very top (root) of the script is always run \n");


function initializeScript()
{
    // Add code here that you want to run every time the script is loaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***>; initializeScript was called \n");
}

function invokeScript()
{
    // Add code here that you want to run every time the script is executed. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***>; invokeScript was called \n");
}
```

有关使用 JavaScript 的详细信息，请参阅[JavaScript 调试器脚本](javascript-debugger-scripting.md)。 调试器对象相关的详细信息，请参阅[JavaScript 扩展中的本机对象](native-objects-in-javascript-extensions.md)。

**要求**

在使用之前的任何.script 命令，脚本编写提供程序需要加载。 使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令，可以加载 JavaScript 提供程序 dll。

```dbgcmd
0:000> .load C:\ScriptProviders\jsprovider.dll
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**.scriptload （负载脚本）**](-scriptload--load-script-.md)

[脚本编写的 JavaScript 调试器](javascript-debugger-scripting.md)










