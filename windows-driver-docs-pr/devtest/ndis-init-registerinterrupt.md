---
title: Init\_RegisterInterrupt 规则 (ndis)
description: Init\_RegisterInterrupt 规则指定，是否出现问题或过程停止微型端口驱动程序初始化过程中，注册中断，这通常发生在初始化期间，必须是撤消。如果 NdisMRegisterInterruptEx 调用 MiniportInitializeEx 至少一次，NdisMDeregisterInterruptEx 函数必须在 MiniportHaltEx 调用至少一次。
ms.assetid: f12cc1b9-396b-4351-ad13-c1750b54b709
ms.date: 05/21/2018
keywords:
- Init_RegisterInterrupt 规则 (ndis)
topic_type:
- apiref
api_name:
- Init_RegisterInterrupt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dfe0fe71385432f8f688cec24999f09f09719713
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392387"
---
# <a name="initregisterinterrupt-rule-ndis"></a>Init\_RegisterInterrupt 规则 (ndis)


Init\_RegisterInterrupt 规则指定，是否出现问题或过程停止微型端口驱动程序初始化过程中，注册中断，这通常发生在初始化期间，必须是撤消。

如果**NdisMRegisterInterruptEx**称为至少一次**MiniportInitializeEx**，则**NdisMDeregisterInterruptEx**必须至少一次调用函数在中**MiniportHaltEx**。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>Init_RegisterInterrupt</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterinterruptex)
[**NdisMRegisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterinterruptex)
 

 





