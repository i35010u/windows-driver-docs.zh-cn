---
title: .scriptload （负载脚本）
description: .Scriptload 命令加载并执行指定的脚本文件。
ms.assetid: 1D4C9587-1491-4D34-9D09-45587B272641
keywords:
- .scriptload （负载脚本） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptload (Load Script)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 77bd18d5268a62cb7ca21bd99b47c0b63a05a560
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526436"
---
# <a name="scriptload-load-script"></a>.scriptload （负载脚本）


**.Scriptload**命令将加载并执行指定的脚本文件。

```dbgcmd
.scriptload ScriptFile
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______ScriptFile______"></span><span id="_______scriptfile______"></span><span id="_______SCRIPTFILE______"></span> *ScriptFile*   
指定要加载的脚本文件的名称。 *ScriptFile*应包含的.js 文件扩展名。 可以使用绝对或相对路径。 相对路径是相对于目录中启动调试器。 不支持文件路径包含空格。

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

.Scriptload 命令加载脚本并执行脚本。 下面的命令演示 TestScript.js 成功加载。

```dbgcmd
0:000> .scriptload C:\WinDbg\Scripts\TestScript.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\TestScript.js'
```

如果在初始加载和执行脚本中的任何错误，错误将显示到控制台，包括行号和错误消息。

```dbgcmd
0:000:x86> .scriptload C:\WinDbg\Scripts\TestScript.js
0:000> "C:\WinDbg\Scripts\TestScript.js" (line 11 (@ 1)): Error (0x80004005): Syntax error
Error: Unable to execute JavaScript script 'C:\WinDbg\Scripts\TestScript.js'
```

.Scriptload 命令将执行以下操作在 JavaScript 中。

-   根代码
-   intializeScript 函数 （如果存在在脚本中）

加载脚本时使用.scriptload 命令、 intializeScript 函数和脚本的根代码执行、 在脚本中提供的名称被桥接至调试程序 (dx 调试程序) 的根命名空间和脚本一直驻留在中释放内存在卸载之后和对其对象的所有引用。

该脚本可以提供新功能到调试器的表达式计算器，修改的对象模型的调试器，或可充当可视化工具在很大程度的相同的 NatVis 可视化工具的方式处理。 有关 NavVis 和调试器的详细信息，请参阅[ **dx （显示 NatVis 表达式）**](dx--display-visualizer-variables-.md)。

有关使用 JavaScript 的详细信息，请参阅[JavaScript 调试器脚本](javascript-debugger-scripting.md)。 调试器对象相关的详细信息，请参阅[JavaScript 扩展中的本机对象](native-objects-in-javascript-extensions.md)。

**要求**

在使用之前的任何.script 命令，脚本编写提供程序需要加载。 使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令，可以加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**.scriptunload （卸载脚本）**](-scriptunload--unload-script-.md)

[脚本编写的 JavaScript 调试器](javascript-debugger-scripting.md)

 

 






