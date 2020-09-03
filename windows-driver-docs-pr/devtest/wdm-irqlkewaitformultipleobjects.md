---
title: 'IrqlKeWaitForMultipleObjects 规则 (wdm) '
description: IrqlKeWaitForMultipleObjects 规则指定 KeWaitForMultipleObjects 例程的调用方必须基于超时参数在适当的 IRQL 上运行。
ms.assetid: FC3E3544-95FB-4283-B030-66D74D0F7848
ms.date: 05/21/2018
keywords:
- 'IrqlKeWaitForMultipleObjects 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlKeWaitForMultipleObjects
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9a716d1a11a34b41c21c28ef23ecf50a2b221225
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384875"
---
# <a name="irqlkewaitformultipleobjects-rule-wdm"></a>IrqlKeWaitForMultipleObjects 规则 (wdm) 


**IrqlKeWaitForMultipleObjects**规则指定[**KeWaitForMultipleObjects**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)例程的调用方必须基于*超时*参数在适当的 IRQL 上运行。

**IrqlKeWaitForMultipleObjects**例程的调用方可以在 IRQL &lt; = 调度 \_ 级别运行，但以下情况除外：

-   如果*超时* &lt; &gt; 0，则必须以 IRQL = APC 级别运行[**KeWaitForMultipleObjects**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)例程的调用方 &lt; \_ 。
-   如果*timeout* ！ = NULL 且 \* *timeout* = 0，则[**KeWaitForMultipleObjects**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)例程的调用方必须以 IRQL = 调度级别运行 \_ 。

-   如果*timeout*  =  **为 NULL**或 \* *timeout* ！ = 0，则[**KeWaitForMultipleObjects**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)例程的调用方必须以 IRQL &lt; = APC \_ 级别运行。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlKeWaitForMultipleObjects</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**KeWaitForMultipleObjects**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)
 

