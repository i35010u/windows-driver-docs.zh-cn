---
title: .scriptload（加载脚本）
description: Scriptload 命令将加载并执行指定的脚本文件。
keywords:
- scriptload (加载脚本) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptload (Load Script)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 274da2fd2c9aadbe692aab51646a956302169e8e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805777"
---
# <a name="scriptload-load-script"></a>.scriptload（加载脚本）


**Scriptload** 命令将加载并执行指定的脚本文件。

```dbgcmd
.scriptload ScriptFile
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______ScriptFile______"></span><span id="_______scriptfile______"></span><span id="_______SCRIPTFILE______"></span>*ScriptFile*   
指定要加载的脚本文件的名称。 *ScriptFile* 应包含 .js 文件扩展名。 可以使用绝对路径或相对路径。 相对路径是相对于在其中启动调试器的目录的相对路径。 不支持包含空格的文件路径。

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

Scriptload 命令将加载脚本并执行脚本。 以下命令显示 TestScript.js 的成功加载。

```dbgcmd
0:000> .scriptload C:\WinDbg\Scripts\TestScript.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\TestScript.js'
```

如果脚本的初始加载和执行中有任何错误，则错误将显示在控制台中，包括行号和错误消息。

```dbgcmd
0:000:x86> .scriptload C:\WinDbg\Scripts\TestScript.js
0:000> "C:\WinDbg\Scripts\TestScript.js" (line 11 (@ 1)): Error (0x80004005): Syntax error
Error: Unable to execute JavaScript script 'C:\WinDbg\Scripts\TestScript.js'
```

Scriptload 命令将在 JavaScript 中执行以下命令。

-   根代码
-   如果脚本中存在 intializeScript 函数 (，则为) 

当使用 scriptload 命令加载脚本时，将执行脚本的 intializeScript 函数和根代码，脚本中存在的名称将桥接到调试器的根命名空间中 (dx 调试器) 并且脚本将保留在内存中，直到它被卸载并释放对其对象的所有引用。

此脚本可以为调试器的表达式计算器提供新函数，修改调试器的对象模型，或以 NatVis 可视化工具的相同方式充当可视化工具。 有关 NavVis 和调试器的详细信息，请参阅 [**dx (显示 NatVis 表达式)**](dx--display-visualizer-variables-.md)。

有关使用 JavaScript 的详细信息，请参阅 [Javascript 调试器脚本](javascript-debugger-scripting.md)。 有关调试器对象的详细信息，请参阅 [JavaScript 扩展中的本机对象](native-objects-in-javascript-extensions.md)。

**惠?**

使用任何脚本命令之前，需要加载脚本提供程序。 使用 [**load (负载扩展 DLL)**](-load---loadby--load-extension-dll-.md) 命令加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**.scriptload（卸载脚本）**](-scriptunload--unload-script-.md)

[JavaScript 调试器脚本](javascript-debugger-scripting.md)

 

 






