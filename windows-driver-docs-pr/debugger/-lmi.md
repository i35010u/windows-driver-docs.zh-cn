---
title: lmi
description: Lmi 扩展显示有关模块的详细的信息。
ms.assetid: 00438edf-618a-401e-818f-24add7861487
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
ms.openlocfilehash: 53e387a16ef145a63b919fc367629643747f96de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523350"
---
# <a name="lmi"></a>！ lmi


**！ Lmi**扩展显示有关模块的详细的信息。

```dbgcmd
!lmi Module
```

## <a name="span-idddklmidbgspanspan-idddklmidbgspanparameters"></a><span id="ddk__lmi_dbg"></span><span id="DDK__LMI_DBG"></span>参数


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *模块*   
指定加载的模块，按名称或基址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

可以使用确定模块地址[ **lm （列表加载模块）** ](lm--list-loaded-modules-.md)命令。

**！ Lmi**扩展分析模块标头，其中显示带格式的信息的摘要。 如果模块标头都分页出来，显示一条错误消息。 若要查看以显示更广泛的标头信息，请使用[ **！ dh** ](-dh.md)扩展命令。

此命令显示多个字段，每个都有不同的标题。 这些标题的一些具有特定含义：

-   **映像名称**字段显示的可执行文件，包括扩展的名称。 通常情况下，完整路径是包含在用户模式下，但不是在内核模式下。

-   **模块**字段显示*模块名称*。 这通常是只是不带扩展名的文件名称。 在少数情况下，模块名称明显不同于的文件的名称。

-   **符号类型**字段显示了有关调试器的尝试加载此模块的符号信息。 有关各种状态的值的说明，请参阅[符号状态缩写](symbol-status-abbreviations.md)。 如果已加载符号，符号文件名称应遵循此。

-   模块中的第一个地址所示**基址**。 模块的大小所示**大小**。 因此，如果**基址**是"faab4000"和**大小**是"2000"模块从 0xFAAB4000 延伸到 0xFAAB5FFF，非独占。

下面是一个示例：

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

有关在所示的缩写的说明**特征**行的此示例中，请参阅[符号状态缩写](symbol-status-abbreviations.md)。

 

 





