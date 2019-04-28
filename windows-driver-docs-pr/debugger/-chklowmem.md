---
title: chklowmem
description: Chklowmem 扩展插件确定低于 4GB 的物理内存页将填入使用 /pae 和 /nolowmem 选项已启动的计算机上的所需的填充模式。
ms.assetid: cc1054e2-b824-4fcf-b353-9ee8c0d3dbf3
keywords:
- PAE （物理地址扩展）
- chklowmem Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- chklowmem
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4069c87228cf7fab8b0c29c374fcb6fe32c0b6ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334634"
---
# <a name="chklowmem"></a>!chklowmem


**！ Chklowmem**扩展插件确定低于 4GB 的物理内存页将填入与已启动的计算机上的所需的填充图案[ **/pae** ](https://msdn.microsoft.com/library/windows/hardware/ff557168)并[ **/nolowmem** ](https://msdn.microsoft.com/library/windows/hardware/ff557144)选项。

```dbgsyntax
!chklowmem
```

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

此扩展时，你要验证内核模式驱动程序与物理内存超过 4 GB 范围正常运行。 通常情况下，驱动程序失败通过截断到 32 位，然后编写以下 4 GB 范围中的物理地址。 **！ Chklowmem**扩展将检测到 4 GB 范围下面任何写入操作。

 

 





