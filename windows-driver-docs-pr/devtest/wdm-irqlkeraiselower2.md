---
title: 'IrqlKeRaiseLower2 规则 (wdm) '
description: IrqlKeRaiseLower2 规则指定驱动程序使用 KeLowerIrql 来还原前面调用 KeRaiseIrql 或 KeRaiseIrqlToDpcLevel 引发的原始 IRQL。
ms.assetid: 7e256237-e649-45de-bcd9-b06795a5c5c9
ms.date: 05/21/2018
keywords:
- 'IrqlKeRaiseLower2 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlKeRaiseLower2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f551db38f871a7a8826680f1aa3a80d6d804bc3d
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101684"
---
# <a name="irqlkeraiselower2-rule-wdm"></a>IrqlKeRaiseLower2 规则 (wdm) 


**IrqlKeRaiseLower2**规则指定驱动程序使用[**KeLowerIrql**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)来还原前面调用[**KeRaiseIrql**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)或[**KeRaiseIrqlToDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirqltodpclevel)引发的原始 IRQL。

此规则允许嵌套调用 **KeRaiseIrql**、 **KeRaiseIrqlToDpcLevel** 和 **KeLowerIrql**。

**驱动程序模型： WDM**

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlKeRaiseLower2</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**KeLowerIrql**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql) 
[**KeRaiseIrql**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)另请参阅
--------

[**IrqlKeDispatchLte**](wdm-irqlkedispatchlte.md) 
[ **IrqlKeRaiseLower**](wdm-irqlkeraiselower.md)
