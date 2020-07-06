---
title: PnpRemove 规则（wdm）
description: PnpRemove 规则指定驱动程序无法完成 IRP \_ MN \_ 意外 \_ 删除、irp \_ MN \_ 取消 \_ 删除 \_ 设备、irp \_ MN \_ cancel \_ 停止 \_ 设备或 irp \_ MN \_ 删除 \_ 设备请求失败。
ms.assetid: 2713F943-36A2-41B9-B9C0-86FC06B22443
ms.date: 05/21/2018
keywords:
- PnpRemove 规则（wdm）
topic_type:
- apiref
api_name:
- PnpRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0c4d2951e9e3e3f5a71b7543aa49056b5e4f7a6b
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968366"
---
# <a name="pnpremove-rule-wdm"></a>PnpRemove 规则（wdm）


**PnpRemove**规则指定驱动程序无法完成 IRP \_ MN \_ 意外 \_ 删除、irp \_ MN \_ 取消 \_ 删除 \_ 设备、irp \_ MN \_ cancel \_ 停止 \_ 设备或 irp \_ MN \_ 删除 \_ 设备请求失败。

> [!NOTE]
> 在 Windows 8.1 中，可以使用[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)测试**PnpRemove**规则。 此规则当前不可用于[静态驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)。

 

**驱动程序模型： WDM**

**找到了具有此规则的 bug 检查**： [**bug 检查0XC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x00043006）


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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">驱动程序验证程序</a>，并选择 " <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 相容性检查</a>" 选项。</p></td>
</tr>
</tbody>
</table>

 

 

 





