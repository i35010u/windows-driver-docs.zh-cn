---
title: .scriptload（卸载脚本）
description: Scriptunload 命令卸载指定的脚本。
keywords:
- scriptunload (卸载脚本) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptunload (Unload Script)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ab4187d087bc6c357157978d7ea0d92b49ffe240
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829983"
---
# <a name="scriptunload-unload-script"></a>.scriptload（卸载脚本）


**Scriptunload** 命令卸载指定的脚本。

```dbgcmd
.scriptunload ScriptFile
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______ScriptFile______"></span><span id="_______scriptfile______"></span><span id="_______SCRIPTFILE______"></span>*ScriptFile*   
指定要卸载的脚本文件的名称。 *ScriptFile* 应包含 .js 文件扩展名。 可以使用绝对路径或相对路径。 相对路径是相对于在其中启动调试器的目录的相对路径。 不支持包含空格的文件路径。

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

Scriptunload 命令卸载已加载的脚本。 使用以下命令语法卸载脚本

```dbgcmd
0:000:x86> .scriptunload C:\WinDbg\Scripts\TestScript.js
JavaScript script unloaded from 'C:\WinDbg\Scripts\TestScript.js'
```

如果脚本中的对象存在未完成的引用，则将取消链接该脚本的内容，但该脚本可能会保留在内存中，直到释放所有此类引用。

有关使用 JavaScript 的详细信息，请参阅 [Javascript 调试器脚本](javascript-debugger-scripting.md)。 有关调试器对象的详细信息，请参阅 [JavaScript 扩展中的本机对象](native-objects-in-javascript-extensions.md)。

**惠?**

使用任何脚本命令之前，需要加载脚本提供程序。 使用 [**load (负载扩展 DLL)**](-load---loadby--load-extension-dll-.md) 命令加载 JavaScript 提供程序 dll。

```dbgcmd
0:000> .load C:\ScriptProviders\jsprovider.dll
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**.scriptload（加载脚本）**](-scriptload--load-script-.md)

[JavaScript 调试器脚本](javascript-debugger-scripting.md)

 

 






