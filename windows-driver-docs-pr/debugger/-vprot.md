---
title: vprot
description: Vprot 扩展显示虚拟内存保护信息。
keywords:
- 内存，内存保护
- vprot Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vprot
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 17b3bc183003c89074be551058656ee65d44883a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838401"
---
# <a name="vprot"></a>!vprot


**！ Vprot** 扩展显示虚拟内存保护信息。

```dbgcmd
!vprot [Address]
```

## <a name="span-idddk__vprot_dbgspanspan-idddk__vprot_dbgspanparameters"></a><span id="ddk__vprot_dbg"></span><span id="DDK__VPROT_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示其内存保护状态的十六进制地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Uext.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要查看目标进程所拥有的所有内存范围的内存保护信息，请使用 [**！ vadump**](-vadump.md)。 有关内存保护的信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制* 。 

<a name="remarks"></a>备注
-------

**！ Vprot** extension 命令可用于实时调试和转储文件调试。

以下是示例：

```dbgcmd
0:000> !vprot 30c191c
BaseAddress: 030c1000
AllocationBase: 030c0000
AllocationProtect: 00000080 PAGE_EXECUTE_WRITECOPY
RegionSize: 00011000
State: 00001000 MEM_COMMIT
Protect: 00000010 PAGE_EXECUTE
Type: 01000000 MEM_IMAGE
```

在此显示中，"AllocationProtect" 行显示了创建整个区域所用的默认保护。 请注意，在分配内存后，此区域中的各个地址可以更改其保护 (例如，如果将 **VirtualProtect** 称为) 。 "保护" 行显示了此特定地址的实际保护。 可能的保护值为 PAGE \_ NOACCESS、page \_ READONLY、page \_ READWRITE、PAGE \_ execute、PAGE \_ execute \_ READ、page \_ execute \_ READWRITE、page \_ WRITECOPY、page \_ execute \_ WRITECOPY 和 page \_ GUARD。

状态行还适用于传递到 **！ vprot** 的特定虚拟地址。 可能的状态值包括 MEM \_ COMMIT、mem \_ FREE 和 mem \_ RESERVE。

"类型" 行显示内存类型。 可能的值包括 MEM \_ 映像、内存 \_ 映射和内存 \_ 专用。

 

 





