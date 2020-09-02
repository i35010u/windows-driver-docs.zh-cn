---
title: 'DebugBreakUsage 规则 (wdm) '
description: DebugBreakUsage 规则指定驱动程序不得调用 DbgBreakPoint 或 DbgBreakPointWithStatus。 仅当构建驱动程序的非调试版本时，此规则才适用。
ms.assetid: 1f634b7c-6939-41ea-8eed-5207f40e5476
ms.date: 05/21/2018
keywords:
- 'DebugBreakUsage 规则 (wdm) '
topic_type:
- apiref
api_name:
- DebugBreakUsage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa8035e7fb3fc60bcd2569fc8e65d4c8c4a21780
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383137"
---
# <a name="debugbreakusage-rule-wdm"></a>DebugBreakUsage 规则 (wdm) 


**DebugBreakUsage**规则指定驱动程序不得调用[**DbgBreakPoint**](/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint)或[**DbgBreakPointWithStatus**](/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpointwithstatus)。 仅当构建驱动程序的非调试版本时，此规则才适用。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>DebugBreakUsage</strong> 规则。</p>
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

 

