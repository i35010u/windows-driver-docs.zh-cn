---
title: .extpath（设置扩展路径）
description: Extpath 命令设置或显示扩展 DLL 搜索路径。
keywords:
- extpath (设置扩展路径) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .extpath (Set Extension Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 743d0136cb52b8b1d5731a28986c94a41025811d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820409"
---
# <a name="extpath-set-extension-path"></a>.extpath（设置扩展路径）


**Extpath** 命令设置或显示扩展 DLL 搜索路径。

```dbgcmd
.extpath[+] [Directory[;...]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="______________"></span> +   
表示调试器应将新目录追加到以前的扩展 DLL 搜索路径 (而不是替换) 的路径。

<span id="_______Directory______"></span><span id="_______directory______"></span><span id="_______DIRECTORY______"></span>*目录*   
指定要放入搜索路径中的一个或多个目录。 如果未指定 *目录*，则显示当前路径。 可以用分号分隔多个目录。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>模式</p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关扩展搜索路径和加载扩展 Dll 的详细信息，请参阅 [加载调试器扩展 dll](loading-debugger-extension-dlls.md)。

<a name="remarks"></a>备注
-------

扩展 DLL 搜索路径将在每个调试会话开始时重置为其默认值。

在实时内核模式调试期间，重新启动目标计算机将导致开始新的调试会话。 因此，在内核模式调试期间对扩展 DLL 搜索路径所做的任何更改都不会在目标计算机重新启动时保持。

扩展 DLL 搜索路径的默认值包含调试器已知的所有扩展路径以及% PATH% 环境变量中的所有路径。 例如，假设% PATH% 环境变量的值为 `C:\Windows\system32;C:\Windows` 。 否则，DLL 扩展搜索路径的默认值可能与此类似。

```dbgcmd
0:000> .extpath
Extension search path is: C:\Program Files\Debugging Tools for Windows (x64)\WINXP;C:\Program Files\
Debugging Tools for Windows (x64)\winext;C:\Program Files\Debugging Tools for Windows (x64)\winext\
arcade;C:\Program Files\Debugging Tools for Windows (x64);C:\Program Files\Debugging Tools for 
Windows (x64)\winext\arcade;C:\Windows\system32;C:\Windows
```

 

 





