---
title: .extpath（设置扩展路径）
description: .Extpath 命令设置或显示的扩展 DLL 搜索路径。
ms.assetid: 957028ff-d8f4-41ab-bdaa-ff1bbe886bec
keywords:
- .extpath （设置扩展路径） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .extpath (Set Extension Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 10fe37d68e0240461f34f5ba75b3ce145b4a9ccc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565077"
---
# <a name="extpath-set-extension-path"></a>.extpath（设置扩展路径）


**.Extpath**命令设置或显示的扩展 DLL 搜索路径。

```dbgcmd
.extpath[+] [Directory[;...]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="______________"></span> +   
表示调试器应附加到以前的扩展 DLL 搜索路径 （而不是替换路径） 的新目录。

<span id="_______Directory______"></span><span id="_______directory______"></span><span id="_______DIRECTORY______"></span> *Directory*   
指定要放入搜索路径中的一个或多个目录。 如果未指定*Directory*，显示当前路径。 可以使用分号分隔多个目录。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>模式</p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关扩展搜索路径和加载扩展 Dll 的详细信息，请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)。

<a name="remarks"></a>备注
-------

扩展 DLL 搜索路径重置为其每个调试会话开始时的默认值。

在实时内核模式调试，重启目标计算机会导致新的调试会话开始。 因此对扩展 DLL 进行任何更改搜索路径在内核模式调试期间将不会保留在重启目标计算机之间。

扩展 DLL 搜索路径的默认值包含调试器已知的所有扩展路径和 %PATH%环境变量中的所有路径。 例如，假设 %PATH%环境变量的值为`C:\Windows\system32;C:\Windows`。 然后 DLL 扩展搜索路径的默认值可能如下所示。

```dbgcmd
0:000> .extpath
Extension search path is: C:\Program Files\Debugging Tools for Windows (x64)\WINXP;C:\Program Files\
Debugging Tools for Windows (x64)\winext;C:\Program Files\Debugging Tools for Windows (x64)\winext\
arcade;C:\Program Files\Debugging Tools for Windows (x64);C:\Program Files\Debugging Tools for 
Windows (x64)\winext\arcade;C:\Windows\system32;C:\Windows
```

 

 





