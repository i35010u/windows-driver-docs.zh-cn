---
title: vadump
description: Vadump 扩展显示所有虚拟内存范围及其相应的保护信息。
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
ms.openlocfilehash: 2e264e1800f26f5ca5bb348b8b74496267f18c88
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833739"
---
# <a name="vadump"></a>!vadump


**！ Vadump** 扩展显示所有虚拟内存范围及其相应的保护信息。

```dbgcmd
    !vadump [-v] 
```

## <a name="span-idddk__vadump_dbgspanspan-idddk__vadump_dbgspanparameters"></a><span id="ddk__vadump_dbg"></span><span id="DDK__VADUMP_DBG"></span>参数


<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
使显示也包括有关每个原始分配区域的信息。 由于在 **VirtualProtect** 分配内存后，区域内的单个地址可能会更改其保护，例如) ，此较大区域的原始保护状态可能不同于区域内每个范围的 (。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要查看单个虚拟地址的内存保护信息，请使用 [**！ vprot**](-vprot.md)。 有关内存保护的信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制* 。

<a name="remarks"></a>备注
-------

以下是示例：

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

在此显示中，"状态" 行显示从指定 BaseAddress 开始的内存范围状态。 可能的状态值包括 MEM \_ COMMIT、mem \_ FREE 和 mem \_ RESERVE。

保护行显示此内存范围的保护状态。 可能的保护值为 PAGE \_ NOACCESS、page \_ READONLY、page \_ READWRITE、PAGE \_ execute、PAGE \_ execute \_ READ、page \_ execute \_ READWRITE、page \_ WRITECOPY、page \_ execute \_ WRITECOPY 和 page \_ GUARD。

"类型" 行显示内存类型。 可能的值包括 MEM \_ 映像、内存 \_ 映射和内存 \_ 专用。

下面是使用 **-v** 参数的示例：

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

使用 **-v** 时，"AllocationProtect" 行显示创建整个区域时使用的默认保护。 "保护" 行显示了此特定地址的实际保护。

 

 





