---
title: DebugBreakUsage 规则 (wdm)
description: DebugBreakUsage 规则指定驱动程序必须调用 DbgBreakPoint 或 DbgBreakPointWithStatus。 要生成非调试版本的驱动程序，则仅适用于此规则。
ms.assetid: 1f634b7c-6939-41ea-8eed-5207f40e5476
ms.date: 05/21/2018
keywords:
- DebugBreakUsage 规则 (wdm)
topic_type:
- apiref
api_name:
- DebugBreakUsage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: da2a2253449fda6786944549b7d2da53c9bccbaf
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393988"
---
# <a name="debugbreakusage-rule-wdm"></a>DebugBreakUsage 规则 (wdm)


**DebugBreakUsage**规则指定驱动程序必须调用[ **DbgBreakPoint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgbreakpoint)或者[ **DbgBreakPointWithStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgbreakpointwithstatus). 要生成非调试版本的驱动程序，则仅适用于此规则。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>DebugBreakUsage</strong>规则。</p>
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

 

 





