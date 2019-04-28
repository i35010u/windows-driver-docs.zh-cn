---
title: .unload（卸载扩展 DLL）
description: .Unload 命令将卸载扩展 DLL 在调试器中。
ms.assetid: 8399e4a8-0265-4690-b35f-973b69fe2764
keywords:
- 卸载扩展 DLL (.unload) 命令
- 扩展命令 （命令），卸载扩展 DLL (.unload) 命令
- .unload （卸载扩展 DLL） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .unload (Unload Extension DLL)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b25de3865a9d6d04e066fba1eb64f50e15c20ab6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334147"
---
# <a name="unload-unload-extension-dll"></a>.unload（卸载扩展 DLL）


**.Unload**命令将卸载扩展 DLL 在调试器中的。

```dbgcmd
.unload DLLName 
!DLLName.unload
```

## <a name="span-idddkmetaunloadextensiondlldbgspanspan-idddkmetaunloadextensiondlldbgspanparameters"></a><span id="ddk_meta_unload_extension_dll_dbg"></span><span id="DDK_META_UNLOAD_EXTENSION_DLL_DBG"></span>参数


<span id="_______DLLName______"></span><span id="_______dllname______"></span><span id="_______DLLNAME______"></span> *DLLName*   
指定调试器扩展卸载 DLL 的文件名。 如果加载 DLL 时指定的完整路径，它需要被授予完整此处也。 如果*DLLName*是省略，当前扩展 DLL 被卸载。

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

有关加载的详细信息，请卸载，并控制扩展，请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)。

<a name="remarks"></a>备注
-------

此命令时，测试要创建的扩展。 扩展重新编译时，必须卸载，然后加载新 DLL。

 

 





