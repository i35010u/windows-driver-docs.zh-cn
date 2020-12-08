---
title: .unload（卸载扩展 DLL）
description: Unload 命令从调试器中卸载扩展 DLL。
keywords:
- 卸载扩展 DLL ( 卸载) 命令
- 扩展命令 ( 命令) ，卸载扩展 DLL () 命令
- 。) Windows 调试卸载 (卸载扩展 DLL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .unload (Unload Extension DLL)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2f9c4db2aea4f75f977971de7f3af408832ebe05
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825265"
---
# <a name="unload-unload-extension-dll"></a>.unload（卸载扩展 DLL）


**Unload** 命令从调试器中卸载扩展 DLL。

```dbgcmd
.unload DLLName 
!DLLName.unload
```

## <a name="span-idddk_meta_unload_extension_dll_dbgspanspan-idddk_meta_unload_extension_dll_dbgspanparameters"></a><span id="ddk_meta_unload_extension_dll_dbg"></span><span id="DDK_META_UNLOAD_EXTENSION_DLL_DBG"></span>参数


<span id="_______DLLName______"></span><span id="_______dllname______"></span><span id="_______DLLNAME______"></span>*DLLName*   
指定要卸载的调试器扩展 DLL 的文件名。 如果在加载 DLL 时指定了完整路径，则还需在此处提供完整路径。 如果省略 *DLLName* ，则会卸载当前扩展 DLL。

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

有关加载、卸载和控制扩展的更多详细信息，请参阅 [加载调试器扩展 dll](loading-debugger-extension-dlls.md)。

<a name="remarks"></a>备注
-------

此命令在测试正在创建的扩展时非常有用。 重新编译扩展时，必须先卸载然后再加载新的 DLL。

 

 





