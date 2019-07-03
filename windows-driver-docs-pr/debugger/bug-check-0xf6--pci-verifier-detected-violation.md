---
title: Bug Check 0xF6 PCI_VERIFIER_DETECTED_VIOLATION
description: PCI_VERIFIER_DETECTED_VIOLATION bug 检查具有 0x000000F6 值。 这表示在 BIOS 或另一台设备正在验证 PCI 驱动程序中发生了错误。
ms.assetid: 8d2be46d-52fd-41dc-b33c-67fea7e0e501
keywords:
- Bug Check 0xF6 PCI_VERIFIER_DETECTED_VIOLATION
- PCI_VERIFIER_DETECTED_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PCI_VERIFIER_DETECTED_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7c9d6a37a235cfc0150583d46f8577970487c59f
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518740"
---
# <a name="bug-check-0xf6-pciverifierdetectedviolation"></a>Bug 检查 0xF6：PCI\_VERIFIER\_检测到\_冲突


PCI\_VERIFIER\_检测到\_冲突错误检查的值为 0x000000F6。 这表示在 BIOS 或另一台设备正在验证 PCI 驱动程序中发生了错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="pciverifierdetectedviolation-parameters"></a>PCI\_VERIFIER\_检测到\_冲突参数


参数 1 是感兴趣; 的唯一参数此列标识检测到故障的性质。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>停靠事件期间，active 桥被囿由 BIOS。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>在规范规定的时间内未更新 PMCSR 注册。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>驱动程序已写入到 Windows 控制部分 PCI 设备的配置空间。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

PCI 驱动程序中的设备或正在验证的 BIOS 检测到错误。

 

 




