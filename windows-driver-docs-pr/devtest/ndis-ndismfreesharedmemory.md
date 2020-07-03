---
title: NdisMFreeSharedMemory 规则（ndis）
description: 不能从 MiniportShutdownEx 函数调用 NdisMFreeSharedMemory。
ms.assetid: 86109F0F-38ED-4A20-9BFF-7738D7944DD8
ms.date: 05/21/2018
keywords:
- NdisMFreeSharedMemory 规则（ndis）
topic_type:
- apiref
api_name:
- NdisMFreeSharedMemory
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ff604bdbdb387f3a8a48bda71bc8a65185484616
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916112"
---
# <a name="ndismfreesharedmemory-rule-ndis"></a>NdisMFreeSharedMemory 规则（ndis）


不能从[*MiniportShutdownEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)函数调用[**NdisMFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory) 。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>NdisMFreeSharedMemory</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**NdisMFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory)
 

 





