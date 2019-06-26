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
ms.openlocfilehash: fd654f9e840d118313a262ddf6daa49df6e78871
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363168"
---
# <a name="chklowmem"></a>!chklowmem


**！ Chklowmem**扩展插件确定低于 4GB 的物理内存页将填入与已启动的计算机上的所需的填充图案[ **/pae** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/-pae)并[ **/nolowmem** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/-nolowmem)选项。

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

 

 





