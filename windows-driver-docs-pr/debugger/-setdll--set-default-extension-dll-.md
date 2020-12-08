---
title: .setdll（设置默认扩展 DLL）
description: Setdll 命令更改调试器的默认扩展 DLL。
keywords:
- " () 命令设置默认扩展 DLL"
- 扩展命令 ( 命令) ，请设置默认扩展 DLL ( setdll) 命令
- setdll (设置默认扩展 DLL) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .setdll (Set Default Extension DLL)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a46b0ff0b263a62777faf4def1b0b97f5d03fcdb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802063"
---
# <a name="setdll-set-default-extension-dll"></a>.setdll（设置默认扩展 DLL）


**Setdll** 命令更改调试器的默认扩展 DLL。

```dbgcmd
.setdll DLLName 
!DLLName.setdll 
```

## <a name="span-idddk_meta_set_default_extension_dll_dbgspanspan-idddk_meta_set_default_extension_dll_dbgspanparameters"></a><span id="ddk_meta_set_default_extension_dll_dbg"></span><span id="DDK_META_SET_DEFAULT_EXTENSION_DLL_DBG"></span>参数


<span id="_______DLLName______"></span><span id="_______dllname______"></span><span id="_______DLLNAME______"></span>*DLLName*   
扩展 DLL 的名称和路径。 如果在加载 DLL 时指定了完整路径，则还需在此处提供完整路径。

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

有关加载、卸载和控制扩展的详细信息，请参阅 [加载调试器扩展 dll](loading-debugger-extension-dlls.md)。 有关执行扩展命令的详细信息，请参阅 [使用调试器扩展命令](using-debugger-extension-commands.md)。

<a name="remarks"></a>备注
-------

调试器会保留一个默认扩展 DLL，该 DLL 在调试器启动时隐式加载。 这样，用户无需首先加载扩展 DLL 即可指定扩展命令。 此命令允许修改作为默认 DLL 加载的 DLL。

发出命令后，调试器首先在默认扩展中查找它。 如果找不到匹配项，则将按照加载它们的顺序搜索其他所有加载的扩展 Dll。

 

 





