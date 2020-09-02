---
title: 'PcPoRequestPowerIrp 规则 (音频) '
description: 此规则验证 PortCls 微型端口驱动程序不应使用 IRP \_ MN 设置电源来调用 PoRequestPowerIrp \_ \_ 。
ms.assetid: 9AF26E98-CB8A-41F1-BF40-1B5FBFD04550
ms.date: 05/21/2018
keywords:
- 'PcPoRequestPowerIrp 规则 (音频) '
topic_type:
- apiref
api_name:
- PcPoRequestPowerIrp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: afefd2a46a11c84026dc85931632112aa36cd903
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381533"
---
# <a name="pcporequestpowerirp-rule-audio"></a>PcPoRequestPowerIrp 规则 (音频) 


此规则验证 PortCls 微型端口驱动程序不应使用[**IRP \_ MN \_ 设置 \_ 电源**](../kernel/irp-mn-set-power.md)来调用[**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) 。

**驱动程序模型：音频**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x0007100A) 


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
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定 <strong>/domain 音频</strong>。</p>
<p>例如：</p>
<p><strong>verifier/domain 音频</strong>[<em>options</em>] <strong>/driver</strong> <em> &lt; yourdriver &gt; </em></p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a>。</p></td>
</tr>
</tbody>
</table>

 

 

