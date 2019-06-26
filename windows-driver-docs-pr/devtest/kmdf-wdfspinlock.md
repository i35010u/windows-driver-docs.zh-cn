---
title: WdfSpinlock 规则 (kmdf)
description: WdfSpinlock 规则指定对 WdfSpinLockAcquire 方法的调用在与 WdfSpinlockRelease 严格替换中使用。
ms.assetid: bf95509a-29f7-462d-b883-39aca4193ebb
ms.date: 05/21/2018
keywords:
- WdfSpinlock 规则 (kmdf)
topic_type:
- apiref
api_name:
- WdfSpinlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c6214b39a7c09a7795c8e99e9f575198be4b6d1e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392813"
---
# <a name="wdfspinlock-rule-kmdf"></a>WdfSpinlock 规则 (kmdf)


**WdfSpinlock**规则指定的调用[ **WdfSpinLockAcquire** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))方法可在使用逻辑或 strict [ **WdfSpinlockRelease**](kmdf-wdfspinlockrelease.md)。 在任何 KMDF 回调例程结束时，该驱动程序不应阻止 framework 旋转锁对象，它通过以前调用获得**WdfSpinLockAcquire**。

|              |      |
|--------------|------|
| 驱动程序模型 | KMDF |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>WdfSpinlock</strong>规则。</p>
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

[**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))
[**WdfSpinLockCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfspinlockcreate)
[**WdfSpinLockRelease**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550044(v=vs.85))
 

 





