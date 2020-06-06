---
title: .load、.loadby（加载扩展 DLL）
description: Loadby 命令会将新的扩展 DLL 加载到调试器中。
ms.assetid: bf54064a-6f30-4f31-a373-fbc643e2660c
keywords:
- 。 load （加载扩展 DLL）命令
- loadby （加载扩展 DLL）命令
- 加载扩展 DLL （loadby）命令
- 扩展命令（命令）、加载扩展 DLL （loadby）命令
- 。 load，. loadby （加载扩展 DLL） Windows 调试
ms.date: 01/30/2020
topic_type:
- apiref
api_name:
- .load, .loadby (Load Extension DLL)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd4128d46781e0558ff58d9489a8652bd3c31ea4
ms.sourcegitcommit: 581fb777a2376854ca12e767d366e2cb79724b73
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2020
ms.locfileid: "84461828"
---
# <a name="load-loadby-load-extension-dll"></a>.load、.loadby（加载扩展 DLL）

**Loadby**命令**会将新**的扩展 DLL 加载到调试器中。

```dbgcmd
.load DLLName  
!DLLName.load 
.loadby DLLName ModuleName
```

## <a name="span-idddk_meta_load_extension_dll_dbgspanspan-idddk_meta_load_extension_dll_dbgspanparameters"></a><span id="ddk_meta_load_extension_dll_dbg"></span><span id="DDK_META_LOAD_EXTENSION_DLL_DBG"></span>参数


<span id="_______DLLName______"></span><span id="_______dllname______"></span><span id="_______DLLNAME______"></span>*DLLName*   
指定要加载的调试器扩展 DLL。 如果使用**load**命令，则*DLLName*应包含完整路径。 如果使用**loadby**命令，则*DLLName*只应包含文件名。

<span id="_______ModuleName______"></span><span id="_______modulename______"></span><span id="_______MODULENAME______"></span>*ModuleName*   
指定与*DLLName*指定的扩展 DLL 位于同一目录中的模块的模块名称。

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
<td align="left"><p>All</p></td>
</tr>
</tbody>
</table>

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何加载、卸载和控制扩展的详细信息，请参阅[加载调试器扩展 dll](loading-debugger-extension-dlls.md)。

<a name="remarks"></a>注解
-------

如果使用**load**命令，则必须指定完整路径。

如果使用**loadby**命令，则不指定路径。 相反，调试器会找到*ModuleName*参数指定的模块，确定该模块的路径，然后在调试器加载扩展 DLL 时使用该路径。 如果调试器找不到该模块，或找不到扩展 DLL，则您将收到一条错误消息，指出该问题。 指定的模块和扩展 DLL 之间不必存在任何关系。 因此，使用**loadby**命令只是一种避免键入长路径的方法。

完成**load**或 **. loadby**命令后，可以访问在加载的扩展中存储的命令。

若要加载扩展 DLL，可以执行以下操作之一：

- 使用**load**或 **. loadby**命令。

- 通过发出 full **！**<em>DLLName</em>**。**<em>ExtensionCommand</em>语法。 如果调试器尚未加载*DLLName*，则在此时加载 dll （如果它位于当前 dll 搜索路径中）。

使用[链式](-chain--list-debugger-extensions-.md)命令显示有关已加载内容和当前 DLL 搜索路径的信息。

```dbgcmd
0:000> .chain
Extension DLL search Path:
    C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\WINXP;C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\winext;C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\winext\arcade;C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\pri;C:\Program Files (x86)\Windows Kits\10\Debuggers\x64;
Extension DLL chain:
    C:\Windows\Microsoft.NET\Framework64\v4.0.30319\SOS.dll: image 4.8.4084.0, API 1.0.0, built Sun Nov 24 00:38:52 2019
```

例如，托管代码 SOS 不在上面所示的 Dll 的搜索路径中，因此请使用带有完整路径的 load 命令加载该 dll。  

```dbgcmd
0:000> .load C:\Windows\Microsoft.NET\Framework64\v4.0.30319\SOS.dll
```
