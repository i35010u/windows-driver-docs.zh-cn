---
title: ubl
description: Ubl 扩展列出了所有用户空间断点及其当前状态。
keywords:
- 断点，用户空间断点
- ubl Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ubl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ec89d45bd46c81e8accf6c7e056e822a7a1ca71a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821661"
---
# <a name="ubl"></a>!ubl


**！ Ubl** extension 列出了所有用户空间断点及其当前状态。

```dbgcmd
!ubl
```

## <span id="ddk__ubl_dbg"></span><span id="DDK__UBL_DBG"></span>


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

下面是使用和显示用户空间断点的示例：

```dbgcmd
kd> !ubp 8014a131
This command is VERY DANGEROUS, and may crash your system!
If you don't know what you are doing, enter "!ubc *" now!

kd> !ubp 801544f4

kd> !ubd 1

kd> !ubl
 0: e ffffffff`8014a131 (ffffffff`82deb000) 1 ffffffff
 1: d ffffffff`801544f4 (ffffffff`82dff000) 0 ffffffff
```

此列表中的每一行都包含断点号、"已启用" 或 " **d** " 状态 (**e** ; 对于 "已禁用") ，用于设置断点的虚拟地址、实际断点的物理地址、字节位置以及设置断点时此内存位置的内容。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**!ubc**](-ubc.md)

[**!ubd**](-ubd.md)

[**!ube**](-ube.md)

[**!ubp**](-ubp.md)

[用户空间和系统空间](user-space-and-system-space.md)

 

 






