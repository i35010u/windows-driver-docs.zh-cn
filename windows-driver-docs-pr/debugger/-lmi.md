---
title: lmi
description: Lmi 扩展显示有关模块的详细信息。
keywords:
- lmi Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lmi
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1506647246291b67f5611010a83c0950fa3d5d02
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815496"
---
# <a name="lmi"></a>!lmi


**！ Lmi** 扩展显示有关模块的详细信息。

```dbgcmd
!lmi Module
```

## <a name="span-idddk__lmi_dbgspanspan-idddk__lmi_dbgspanparameters"></a><span id="ddk__lmi_dbg"></span><span id="DDK__LMI_DBG"></span>参数


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span>*模块*   
按名称或按基址指定已加载的模块。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以通过使用 " [**lm (List 已加载模块)**](lm--list-loaded-modules-.md) 命令确定模块地址。

**！ Lmi** extension 分析模块标头，并显示其中所含信息的格式化摘要。 如果模块标头已分页，则显示一条错误消息。 若要查看更广泛的标头信息显示，请使用 [**！ dh**](-dh.md) 扩展命令。

此命令会显示多个字段，每个字段都有不同的标题。 其中一些标题具有特定的含义：

-   " **映像名称** " 字段显示可执行文件的名称（包括扩展名）。 通常，完整路径包含在用户模式下，而不是在内核模式下。

-   " **模块** " 字段显示 *模块名称*。 这通常只是不带扩展名的文件名。 在少数情况下，模块名称与文件名明显不同。

-   " **符号类型** " 字段显示有关调试器尝试加载此模块的符号的信息。 有关各个状态值的说明，请参阅 [符号状态缩写](symbol-status-abbreviations.md)。 如果已加载符号，则符号文件名称将在此之后。

-   模块中的第一个地址显示为 " **基址**"。 模块的大小显示为 **大小**。 因此，如果 **基址** 为 "faab4000" 并且 **大小** 为 "2000"，则该模块将从0xFAAB4000 扩展到0xFAAB5FFF （含）。

以下是示例：

```dbgcmd
0:000> lm 
start    end        module name
00400000 0042d000   Prymes     C (pdb symbols)              Prymes.pdb
77e80000 77f35000   KERNEL32     (export symbols)           C:\WINNT\system32\KERNEL32.dll
77f80000 77ffb000   ntdll        (export symbols)           ntdll.dll

0:000> !lmi 00400000
Loaded Module Info: [00400000] 
         Module: Prymes
   Base Address: 00400000
     Image Name: Prymes.exe
   Machine Type: 332 (I386)
     Time Stamp: 3c76c346 Fri Feb 22 14:16:38 2002
           Size: 2d000
       CheckSum: 0
Characteristics: 230e stripped 
Debug Data Dirs: Type Size     VA  Pointer
                 MISC  110,     0,   77a00 [Data not mapped]
    Symbol Type: EXPORT   - PDB not found
    Load Report: export symbols
```

有关此示例的 " **特性** " 行上显示的缩写的说明，请参阅 [符号状态缩写](symbol-status-abbreviations.md)。

 

 





