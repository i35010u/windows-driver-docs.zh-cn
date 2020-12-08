---
title: 'Irql \_ 同步 \_ 函数规则 (ndis) '
description: Irql \_ 同步 \_ 函数规则指定必须在正确的 Irql 级别调用 NDIS 中断和同步 DDIs。
ms.date: 05/21/2018
keywords:
- 'Irql_Synch_Function 规则 (ndis) '
topic_type:
- apiref
api_name:
- Irql_Synch_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 20c94508fb9fc302ade590665a85d041f4d05b43
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830165"
---
# <a name="irql_synch_function-rule-ndis"></a>Irql \_ 同步 \_ 函数规则 (ndis) 


**Irql \_ 同步 \_ 函数** 规则指定必须在正确的 Irql 级别调用 NDIS 中断和同步 DDIs。

**驱动程序模型： NDIS**

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>Irql_Synch_Function</strong> 规则。</p>
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

[**NDIS \_RELEASE \_ mutex**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndis_release_mutex) 
 [**NDIS \_ WAIT \_ \_**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndis_wait_for_mutex) 
 [**NdisAcquireReadWriteLock**](/previous-versions/ff560696(v=vs.85)) 
 [**NdisAcquireSpinLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock) 
 [**NdisDprAcquireSpinLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdpracquirespinlock) 
 [**NdisDprReleaseSpinLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdprreleasespinlock) 
 [**NdisReleaseReadWriteLock**](/previous-versions/ff564521(v=vs.85)) 
 [**NdisReleaseSpinLock**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreleasespinlock) 
 [**NdisResetEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisresetevent) 
 [**NdisSetEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetevent) NdisReleaseSpinLock NdisResetEvent NdisSetEvent
