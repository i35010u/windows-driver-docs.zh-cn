---
title: PnpRemove 规则 (wdm)
description: PnpRemove 规则指定驱动程序无法完成 IRP\_MN\_惊讶\_删除、 IRP\_MN\_取消\_删除\_设备、 IRP\_MN\_取消\_停止\_设备或 IRP\_MN\_删除\_设备与失败的请求。
ms.assetid: 2713F943-36A2-41B9-B9C0-86FC06B22443
ms.date: 05/21/2018
keywords:
- PnpRemove 规则 (wdm)
topic_type:
- apiref
api_name:
- PnpRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9435b357d99f8b22a569a02709be512728b2a76b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554718"
---
# <a name="pnpremove-rule-wdm"></a>PnpRemove 规则 (wdm)


**PnpRemove**规则指定驱动程序无法完成 IRP\_MN\_惊讶\_删除、 IRP\_MN\_取消\_删除\_设备、 IRP\_MN\_取消\_停止\_设备或 IRP\_MN\_删除\_设备与失败的请求。

> [!NOTE]
> 在 Windows 8.1，你可以测试**PnpRemove**规则使用[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)。 该规则不是当前可用于[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)。

 

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00043006) |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a> ，然后选择<a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[DDI compliance checking](https://msdn.microsoft.com/library/windows/hardware/hh454208)">DDI 符合性检查</a>选项。</p></td>
</tr>
</tbody>
</table>

 

 

 





