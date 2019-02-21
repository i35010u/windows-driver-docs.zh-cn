---
title: for_each_function
description: For_each_function 扩展中指定的模块，其名称与指定的模式匹配执行每个函数的调试器命令。
ms.assetid: D51C3562-3D49-4528-A208-71A8756EBC8E
keywords:
- for_each_function Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d9699254771ad1784fd6009d97c46639f41ad429
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521614"
---
# <a name="foreachfunction"></a>!for\_each\_function


**！ 有关\_每个\_函数**扩展执行每个函数的调试程序命令中指定的模块，其名称与指定的模式匹配。

```dbgcmd
!for_each_function -m:ModuleName -p:Pattern -c:CommandString
!for_each_function -?
```

## <a name="span-idddkvaddbgspanspan-idddkvaddbgspanparameters"></a><span id="ddk__vad_dbg"></span><span id="DDK__VAD_DBG"></span>参数


<span id="_______-m_ModuleName______"></span><span id="_______-m_modulename______"></span><span id="_______-M_MODULENAME______"></span> -m:*ModuleName*   
指定模块名称。 此名称通常是不带文件扩展名的文件名称。 在某些情况下，模块名称明显不同于的文件的名称。

<span id="-p_Pattern______"></span><span id="-p_pattern______"></span><span id="-P_PATTERN______"></span>-p:*模式*   
指定要匹配的模式。

<span id="_______-c_CommandString______"></span><span id="_______-c_commandstring______"></span><span id="_______-C_COMMANDSTRING______"></span> -c:*CommandString*   
指定要执行的每个函数中指定的模块，与模式匹配的调试器命令。

可以使用中的以下别名*CommandString*。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">别名</th>
<th align="left">数据类型</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>@#SymbolName</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>符号名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#SymbolAddress</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>符号地址中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#ModName</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>模块名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#FunctionName</p></td>
<td align="left"><p>字符串</p></td>
<td align="left"><p>函数名称。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-_______"></span> -?   
显示此扩展的帮助。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ext.dll

<a name="remarks"></a>备注
-------

下面的示例演示如何列出所有函数名称，请在 PCI 模块中，与模式匹配\*读取\*。

```dbgcmd
1: kd> !for_each_function -m:pci -p:*read* -c:.echo @#FunctionName

PciReadDeviceConfig
PciReadDeviceSpace
PciReadSlotIdData
PciExternalReadDeviceConfig
PiRegStateReadStackCreationSettingsFromKey
VmProxyReadDevicePathsFromRegistry
PpRegStateReadCreateClassCreationSettings
ExpressRootPortReadConfigSpace
PciReadRomImage
PciDevice_ReadConfig
PciReadDeviceConfigEx
PciReadSlotConfig
```

如果别名不是前面和后面的空白区域，您必须将放在别名[ **${}别名解释器**](-------alias-interpreter-.md)令牌。

下面的示例演示如何列出其函数名称与模式匹配的所有模块中的所有符号\*CreateFile\*。 @ 别名\#ModuleName 前面没有空格。 因此，放置在[ **${}别名解释器**](-------alias-interpreter-.md)令牌。

**请注意**  不要混淆 @\#ModuleName 别名 @\#ModName 别名。 @\#ModuleName 别名属于[ **！ 有关\_每个\_模块**](-for-each-module.md)扩展，和 @\#ModName 别名属于 **！有关\_每个\_函数**扩展。

 

```dbgcmd
1: kd> !for_each_module !for_each_function -m:${@#ModuleName} -p:*CreateFile* -c:.echo @#SymbolName
nt!BiCreateFileDeviceElement
nt!NtCreateFile
...
Wdf01000!FxFileObject::_CreateFileObject
fltmgr!FltCreateFileEx2$fin$0
fltmgr!FltCreateFileEx2
...
Ntfs!TxfIoCreateFile
Ntfs!NtfsCreateFileLock
...
MpFilter!MpTxfpCreateFileEntryUnsafe
mrxsmb10!MRxSmbFinishLongNameCreateFile
...
srv!SrvIoCreateFile
```

可以将一系列命令放在命令文件，并使用[  **$$ &gt; &lt; （运行脚本文件）** ](-----------------------a---run-script-file-.md)执行这些命令为每个匹配的函数模式。 假定一个名为 Commands.txt 文件包含以下命令：

```dbgcmd
.echo
.echo @#FunctionName
u @#SymbolAddress L1
```

在以下示例中，Commands.text 文件中的命令执行的每个函数，在 PCI 模块中，与模式匹配\*读取\*。

```dbgcmd
1: kd> !for_each_function -m:pci -p:*read* -c:$$><Commands.txt

PciReadDeviceConfig
pci!PciReadDeviceConfig [d:\wmm1\drivers\busdrv\pci\config.c @ 349]:
fffff880`00f7b798 48895c2408      mov     qword ptr [rsp+8],rbx

PciReadDeviceSpace
pci!PciReadDeviceSpace [d:\wmm1\drivers\busdrv\pci\config.c @ 1621]:
fffff880`00f7c044 48895c2408      mov     qword ptr [rsp+8],rbx

...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**!for\_each\_module**](-for-each-module.md)

 

 






