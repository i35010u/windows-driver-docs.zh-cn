---
title: .scriptload（卸载脚本）
description: .Scriptunload 命令将卸载指定的脚本。
ms.assetid: 015703C2-31E2-46B4-8F89-1EA52DB7E6FC
keywords:
- .scriptunload （卸载脚本） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptunload (Unload Script)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6968ad77c18353f619432b2c7fc85256c9c02995
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330843"
---
# <a name="scriptunload-unload-script"></a>.scriptload（卸载脚本）


**.Scriptunload**命令将卸载指定的脚本。

```dbgcmd
.scriptunload ScriptFile
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______ScriptFile______"></span><span id="_______scriptfile______"></span><span id="_______SCRIPTFILE______"></span> *ScriptFile*   
指定要卸载的脚本文件的名称。 *ScriptFile*应包含的.js 文件扩展名。 可以使用绝对或相对路径。 相对路径是相对于目录中启动调试器。 不支持文件路径包含空格。

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

.Scriptunload 命令将卸载加载的脚本。 使用以下命令语法来卸载脚本

```dbgcmd
0:000:x86> .scriptunload C:\WinDbg\Scripts\TestScript.js
JavaScript script unloaded from 'C:\WinDbg\Scripts\TestScript.js'
```

如果有一个脚本中的对象未完成的引用，该脚本的内容会被取消链接，但脚本可能会保留在内存中，直到所有此类引用被释放。

有关使用 JavaScript 的详细信息，请参阅[JavaScript 调试器脚本](javascript-debugger-scripting.md)。 调试器对象相关的详细信息，请参阅[JavaScript 扩展中的本机对象](native-objects-in-javascript-extensions.md)。

**要求**

在使用之前的任何.script 命令，脚本编写提供程序需要加载。 使用[ **.load (加载扩展 DLL)** ](-load---loadby--load-extension-dll-.md)命令，可以加载 JavaScript 提供程序 dll。

```dbgcmd
0:000> .load C:\ScriptProviders\jsprovider.dll
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**.scriptload （负载脚本）**](-scriptload--load-script-.md)

[JavaScript 调试器脚本](javascript-debugger-scripting.md)

 

 






