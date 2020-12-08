---
title: ubp
description: Ubp 扩展在用户空间中设置一个断点。
keywords:
- ubp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ubp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0cac469e816234e224c06b5bf02cb49eb742813f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833901"
---
# <a name="ubp"></a>!ubp


**！ Ubp** extension 在用户空间中设置一个断点。

```dbgcmd
!ubp Address 
```

## <a name="span-idddk__ubp_dbgspanspan-idddk__ubp_dbgspanparameters"></a><span id="ddk__ubp_dbg"></span><span id="DDK__UBP_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定用户空间中要设置断点的位置的十六进制虚拟地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**！ Ubp** extension 在用户空间中设置一个断点。 断点在实际物理页上设置，而不只是在虚拟页上设置。

设置物理断点会同时修改页面的每个虚拟副本，并产生不可预知的结果。 一个可能的结果是系统状态损坏，可能后跟 bug 检查或其他系统故障。 因此，应慎重使用这些断点（如果有）。

此扩展不能用于在已交换内存的页面上设置断点。 如果在设置断点后将页面交换出内存，则断点将停止存在。

不能在页表或页目录中设置断点。

为每个断点分配一个 *断点号*。 若要确定分配的断点号，请使用 [**！ ubl**](-ubl.md)。 断点在创建时启用。 若要逐过程执行断点，必须先使用 [**！ ubd**](-ubd.md)将其禁用。 若要清除断点，请使用 [**！ ubc**](-ubc.md)。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**!ubc**](-ubc.md)

[**!ubd**](-ubd.md)

[**!ube**](-ube.md)

[**!ubl**](-ubl.md)

[用户空间和系统空间](user-space-and-system-space.md)

 

 






