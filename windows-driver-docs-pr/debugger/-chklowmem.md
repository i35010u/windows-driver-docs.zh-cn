---
title: chklowmem
description: Chklowmem 扩展在使用/pae 和/nolowmem 选项启动的计算机上，确定低于 4 GB 的物理内存页是否填充了所需的填充模式。
ms.assetid: cc1054e2-b824-4fcf-b353-9ee8c0d3dbf3
keywords:
- 'PAE (物理地址扩展) '
- chklowmem Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- chklowmem
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 82d418dccc68e1b34e309040424be9ccdd2b4b96
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210265"
---
# <a name="chklowmem"></a>!chklowmem


**！ Chklowmem** extension 确定使用[**/pae**](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200)和[**/nolowmem**](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200)选项启动的计算机上是否使用所需的填充模式填充低于 4 GB 的物理内存页。

```dbgsyntax
!chklowmem
```

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
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

当你验证内核模式驱动程序是否正常运行在 4 GB 边界以上的物理内存时，此扩展非常有用。 通常情况下，驱动程序会在以下情况下失败：将物理地址截断到32位，然后在 4 GB 边界下写入。 **！ Chklowmem**扩展将检测到 4 GB 边界以下的所有写入。

 

