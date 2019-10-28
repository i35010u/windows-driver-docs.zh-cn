---
title: DebugBreakUsage 规则（wdm）
description: DebugBreakUsage 规则指定驱动程序不得调用 DbgBreakPoint 或 DbgBreakPointWithStatus。 仅当构建驱动程序的非调试版本时，此规则才适用。
ms.assetid: 1f634b7c-6939-41ea-8eed-5207f40e5476
ms.date: 05/21/2018
keywords:
- DebugBreakUsage 规则（wdm）
topic_type:
- apiref
api_name:
- DebugBreakUsage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ce1b83c94a6c9554964fe7e12d259ee348b8ab0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839240"
---
# <a name="debugbreakusage-rule-wdm"></a>DebugBreakUsage 规则（wdm）


**DebugBreakUsage**规则指定驱动程序不得调用[**DbgBreakPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint)或[**DbgBreakPointWithStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpointwithstatus)。 仅当构建驱动程序的非调试版本时，此规则才适用。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>DebugBreakUsage</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

 

 





