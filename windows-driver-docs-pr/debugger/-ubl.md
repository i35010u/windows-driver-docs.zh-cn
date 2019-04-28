---
title: ubl
description: Ubl 扩展列出所有用户空间断点及其当前状态。
ms.assetid: c2c40fa5-888f-49bb-a616-a139d7d2874d
keywords:
- 用户空间断点的断点
- ubl Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ubl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c7f0bf65957902c5260c22242a1416d52e6f7829
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334151"
---
# <a name="ubl"></a>!ubl


**！ Ubl**扩展列出所有用户空间断点及其当前状态。

```dbgcmd
!ubl
```

## <span id="ddk__ubl_dbg"></span><span id="DDK__UBL_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

下面是使用的示例和显示用户空间断点：

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

在此列表中的每个行包含该断点次、 状态 (**e**启用的或**d**已禁用)，用于设置所需断点，实际的断点，物理地址的虚拟地址字节位置，并在设置了断点时此内存位置的内容。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**!ubc**](-ubc.md)

[**!ubd**](-ubd.md)

[**!ube**](-ube.md)

[**!ubp**](-ubp.md)

[用户空间和系统空间](user-space-and-system-space.md)

 

 






