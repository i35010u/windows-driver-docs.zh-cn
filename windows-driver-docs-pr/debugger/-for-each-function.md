---
title: for_each_function
description: For_each_function 扩展为指定模块中的每个函数执行一个调试器命令，其名称与指定的模式匹配。
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
ms.openlocfilehash: b6ff0929ec446d58b96c5ddf38bc89c35415dd49
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823651"
---
# <a name="for_each_function"></a>！对于 \_ 每个 \_ 函数


**对于 \_ 每个 \_ 函数** 扩展，将为指定模块中的每个函数执行一个调试器命令，其名称与指定的模式匹配。

```dbgcmd
!for_each_function -m:ModuleName -p:Pattern -c:CommandString
!for_each_function -?
```

## <a name="span-idddk__vad_dbgspanspan-idddk__vad_dbgspanparameters"></a><span id="ddk__vad_dbg"></span><span id="DDK__VAD_DBG"></span>参数


<span id="_______-m_ModuleName______"></span><span id="_______-m_modulename______"></span><span id="_______-M_MODULENAME______"></span> -m：*ModuleName*   
指定模块名称。 此名称通常是没有文件扩展名的文件名。 在某些情况下，模块名称与文件名明显不同。

<span id="-p_Pattern______"></span><span id="-p_pattern______"></span><span id="-P_PATTERN______"></span>-p：*Pattern*   
指定要匹配的模式。

<span id="_______-c_CommandString______"></span><span id="_______-c_commandstring______"></span><span id="_______-C_COMMANDSTRING______"></span> -c：*command.commandstring*   
为指定模块中与模式匹配的每个函数指定要执行的调试器命令。

可以在 *command.commandstring* 中使用以下别名。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Alias</th>
<th align="left">数据类型</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>@ #SymbolName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>符号名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@ #SymbolAddress</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>符号地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@ #ModName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>模块名。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@ #FunctionName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>函数名称。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-_______"></span> -?   
显示此扩展的帮助。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ext.dll

<a name="remarks"></a>备注
-------

下面的示例演示如何列出 PCI 模块中与读取的模式匹配的所有函数名称 \* \* 。

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

如果别名后面不跟空格，则必须将该别名放入 [**$ {} alias 解释**](-------alias-interpreter-.md) 器标记中。

下面的示例演示如何列出所有模块中其函数名称与模式 CreateFile 匹配的所有符号 \* \* 。 别名 @ \# ModuleName 前面没有空格。 因此，将其放入 [**$ {} Alias 解释**](-------alias-interpreter-.md) 器标记中。

**注意**  不要将 @ \# ModuleName 别名与 @ \# ModName 别名混淆。 @ \# ModuleName 别名属于 [**\_ 每个 \_ 模块**](-for-each-module.md) 扩展的！，@ \# ModName 别名属于 **\_ 每个 \_ 函数** 扩展的！。

 

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

您可以在命令文件中放置一系列命令，并使用 [**$$ &gt; &lt; (运行脚本文件)**](-----------------------a---run-script-file-.md)为每个与模式匹配的函数执行这些命令。 假设名为 Commands.txt 的文件包含以下命令：

```dbgcmd
.echo
.echo @#FunctionName
u @#SymbolAddress L1
```

在下面的示例中，为 PCI 模块中的每个函数执行了文本文件中的命令，该文件与读取的模式匹配 \* \* 。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**！对于 \_ 每个 \_ 模块**](-for-each-module.md)

 

 






