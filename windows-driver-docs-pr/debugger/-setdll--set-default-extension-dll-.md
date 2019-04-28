---
title: .setdll（设置默认扩展 DLL）
description: .Setdll 命令更改默认扩展插件 DLL 的调试程序。
ms.assetid: 9dc5cd9e-d4f2-4112-bf3d-f7061c786ddf
keywords:
- 设置默认扩展 DLL (.setdll) 命令
- 扩展命令 （命令），设置默认的扩展 DLL (.setdll) 命令
- .setdll （设置默认扩展 DLL） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .setdll (Set Default Extension DLL)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 32db5bf0ee2da68d7d1f9d8e71c9c6850cf9c622
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339801"
---
# <a name="setdll-set-default-extension-dll"></a>.setdll（设置默认扩展 DLL）


**.Setdll**命令更改默认扩展插件 DLL 的调试程序。

```dbgcmd
.setdll DLLName 
!DLLName.setdll 
```

## <a name="span-idddkmetasetdefaultextensiondlldbgspanspan-idddkmetasetdefaultextensiondlldbgspanparameters"></a><span id="ddk_meta_set_default_extension_dll_dbg"></span><span id="DDK_META_SET_DEFAULT_EXTENSION_DLL_DBG"></span>参数


<span id="_______DLLName______"></span><span id="_______dllname______"></span><span id="_______DLLNAME______"></span> *DLLName*   
名称和扩展 DLL 的路径。 如果加载 DLL 时指定的完整路径，它需要被授予完整此处也。

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

有关加载的详细信息，卸载，并控制扩展，请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)。 执行扩展命令的详细信息，请参阅[使用调试器扩展命令](using-debugger-extension-commands.md)。

<a name="remarks"></a>备注
-------

调试器维护默认扩展插件将在启动调试器时隐式加载的 DLL。 这样，用户可以指定是扩展命令，而不必首先加载扩展 DLL。 此命令允许的修改这些为默认值 DLL 加载 DLL。

当发出命令时，调试器为其默认扩展插件中首先查找。 如果找不到匹配项，所有其他已加载的扩展 Dll 中加载它们的顺序搜索。

 

 





