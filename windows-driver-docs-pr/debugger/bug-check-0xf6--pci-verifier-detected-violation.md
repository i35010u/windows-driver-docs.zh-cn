---
title: Bug 检查 0xF6 PCI_VERIFIER_DETECTED_VIOLATION
description: PCI_VERIFIER_DETECTED_VIOLATION bug 检查的值为0x000000F6。 这表明 BIOS 或 PCI 驱动程序正在验证的其他设备中发生了错误。
keywords:
- Bug 检查 0xF6 PCI_VERIFIER_DETECTED_VIOLATION
- PCI_VERIFIER_DETECTED_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PCI_VERIFIER_DETECTED_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4bb38150b0344e6f585a1357f2e44b12d4f844af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819233"
---
# <a name="bug-check-0xf6-pci_verifier_detected_violation"></a>Bug 检查0xF6： PCI \_ 验证程序 \_ 检测到 \_ 冲突


PCI \_ 验证器 \_ 检测到 \_ 违反 bug 检查的值为0x000000F6。 这表明 BIOS 或 PCI 驱动程序正在验证的其他设备中发生了错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="pci_verifier_detected_violation-parameters"></a>PCI \_ 验证程序 \_ 检测到 \_ 冲突参数


参数1是感兴趣的唯一参数;这会标识检测到的故障的性质。

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
<td align="left"><p>在停靠事件期间，BIOS reprogrammed 了活动桥。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>未在规范规定的时间内更新 PMCSR 注册。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>驱动程序已写入 PCI 设备配置空间的 Windows 控制部分。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

PCI 驱动程序检测到设备或 BIOS 中的错误。

 

 




