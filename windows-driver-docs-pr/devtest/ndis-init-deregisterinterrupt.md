---
title: 'Init \_ DeRegisterInterrupt rule (ndis) '
description: Init \_ DeRegisterInterrupt 规则指定在 MPInitilize 期间至少调用 NdisMRegisterInterruptEx 一次，NdisMDeregisterInterruptEx 应在 MPHaltEx 中至少调用一次。
ms.assetid: C7436321-43DD-4B38-A0A3-9888CFDDA284
ms.date: 05/21/2018
keywords:
- 'Init_DeRegisterInterrupt 规则 (ndis) '
topic_type:
- apiref
api_name:
- Init_DeRegisterInterrupt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2bef7df976aa608a3d0dc42d40c220df699baef2
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101776"
---
# <a name="init_deregisterinterrupt-rule-ndis"></a>Init \_ DeRegisterInterrupt rule (ndis) 


**Init \_ DeRegisterInterrupt**规则指定在 MPInitilize 期间至少调用[**NdisMRegisterInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex)一次， [**NdisMDeregisterInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)应在 MPHaltEx 中至少调用一次。

注册中断（通常发生在初始化期间）应撤消 (取消注册) 如果在初始化过程中出现问题或在停止小型端口过程中出现问题。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>Init_DeRegisterInterrupt</strong> 规则。</p>
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

[**NdisMDeregisterInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex) 
[ **NdisMRegisterInterruptEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex)
