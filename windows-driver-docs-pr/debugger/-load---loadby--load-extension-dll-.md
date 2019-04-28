---
title: .load、.loadby（加载扩展 DLL）
description: .Load 和.loadby 命令加载到调试器中新的扩展 DLL。
ms.assetid: bf54064a-6f30-4f31-a373-fbc643e2660c
keywords:
- .load (加载扩展 DLL) 命令
- loadby (加载扩展 DLL) 命令
- 加载扩展 DLL (.load-.loadby) 命令
- 扩展命令 （命令） 加载扩展 DLL (.load-.loadby) 命令
- .load，.loadby （加载扩展 DLL） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .load, .loadby (Load Extension DLL)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c559509c916563fe1f9fedc459503c407b55fd0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336513"
---
# <a name="load-loadby-load-extension-dll"></a>.load、.loadby（加载扩展 DLL）


**.Load**并 **.loadby**命令加载到调试器中新的扩展 DLL。

```dbgcmd
.load DLLName  
!DLLName.load 
.loadby DLLName ModuleName
```

## <a name="span-idddkmetaloadextensiondlldbgspanspan-idddkmetaloadextensiondlldbgspanparameters"></a><span id="ddk_meta_load_extension_dll_dbg"></span><span id="DDK_META_LOAD_EXTENSION_DLL_DBG"></span>参数


<span id="_______DLLName______"></span><span id="_______dllname______"></span><span id="_______DLLNAME______"></span> *DLLName*   
指定调试器扩展 DLL 加载。 如果您使用 **.load**命令， *DLLName*应包括完整路径。 如果您使用 **.loadby**命令， *DLLName*应包含文件名。

<span id="_______ModuleName______"></span><span id="_______modulename______"></span><span id="_______MODULENAME______"></span> *ModuleName*   
指定位于与扩展 DLL 相同的目录中的模块的模块名称， *DLLName*指定。

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

有关如何加载、 卸载和控件扩展的详细信息，请参阅[加载的调试器扩展 Dll](loading-debugger-extension-dlls.md)。

<a name="remarks"></a>备注
-------

当你使用 **.load**命令时，必须指定完整路径。

当你使用 **.loadby**命令时，你未指定的路径。 相反，调试器发现模块*ModuleName*参数指定、 确定该模块的路径和调试器加载扩展 DLL 时，然后将该路径。 如果调试器无法找到该模块，或者如果它找不到扩展 DLL，则将收到一条错误消息指定问题。 那里没有为任何指定的模块和扩展 DLL 之间的关系。 使用 **.loadby**命令因此是只是为了避免键入长路径一个方法。

之后 **.load**或 **.loadby**命令完成后，你可以访问存储在已加载的扩展中的命令。

若要加载扩展 DLL，可以执行下列任一操作：

- 使用 **.load**或 **.loadby**命令。

- 通过发出完整执行扩展 **！**<em>DLLName</em>**。**<em>ExtensionCommand</em>语法。 如果尚未加载调试器*DLLName*.dll，它此时加载的 DLL。

 

 





