---
title: vadump
description: Vadump 扩展显示所有的虚拟内存范围和其相应的保护信息。
ms.assetid: b13aa852-7333-41fc-ad66-4386040522d8
keywords:
- vadump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vadump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 827b41c8afbd9188f9c41edd072e50012abecb11
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323480"
---
# <a name="vadump"></a>!vadump


**！ Vadump**扩展插件都会显示所有的虚拟内存范围和其相应的保护信息。

```dbgcmd
    !vadump [-v] 
```

## <a name="span-idddkvadumpdbgspanspan-idddkvadumpdbgspanparameters"></a><span id="ddk__vadump_dbg"></span><span id="DDK__VADUMP_DBG"></span>参数


<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
将导致显示以包括有关每个原始的分配区域的信息。 因为在区域内的各个地址可以分配内存后更改其保护 (通过**VirtualProtect**，例如)，此较大区域的原始保护状态可能不相同，每个在区域中的范围。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

若要查看单个虚拟地址的内存保护信息，请使用[ **！ vprot**](-vprot.md)。 有关内存保护的信息，请参阅*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。

<a name="remarks"></a>备注
-------

下面是一个示例：

```dbgcmd
0:000> !vadump
BaseAddress:       00000000
RegionSize:        00010000
State:             00010000  MEM_FREE
Protect:           00000001  PAGE_NOACCESS

BaseAddress:       00010000
RegionSize:        00001000
State:             00001000  MEM_COMMIT
Protect:           00000004  PAGE_READWRITE
Type:              00020000  MEM_PRIVATE
.........
```

在此显示中的状态行显示指定 BaseAddress 开始的内存范围的状态。 可能的状态的值为内存优化\_提交、 内存优化\_免费版和内存优化\_保留。

保护行显示此内存范围内的保护状态。 可能的保护的值为页面\_NOACCESS，页面\_READONLY，页面\_READWRITE，页面\_EXECUTE，页\_EXECUTE\_读取、 页\_EXECUTE\_读写页面\_WRITECOPY，页\_EXECUTE\_WRITECOPY 和页\_防护。

类型行显示的内存类型。 可能的值为内存优化\_图像、 内存优化\_映射，以及内存优化\_专用。

下面是一个示例使用 **-v**参数：

```dbgcmd
0:000> !vadump -v
BaseAddress:       00000000
AllocationBase:    00000000
RegionSize:        00010000
State:             00010000  MEM_FREE
Protect:           00000001  PAGE_NOACCESS

BaseAddress:       00010000
AllocationBase:    00010000
AllocationProtect: 00000004  PAGE_READWRITE
RegionSize:        00001000
State:             00001000  MEM_COMMIT
Protect:           00000004  PAGE_READWRITE
Type:              00020000  MEM_PRIVATE
.........
```

当 **-v** AllocationProtect 行显示的默认的用于创建整个区域时使用的保护。 保护线显示为此特定地址实际的保护。

 

 





