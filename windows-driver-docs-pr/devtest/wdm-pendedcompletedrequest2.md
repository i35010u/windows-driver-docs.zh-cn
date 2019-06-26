---
title: PendedCompletedRequest2 规则 (wdm)
description: PendedCompletedRequest2 规则指定的等待后需要，则调用 IoCallDriver 或 PoCallDriver 因为调度例程无法完成挂起的 IRP。
ms.assetid: 738B9DEE-D7D4-4E6A-AE2D-F363F1255E8A
ms.date: 05/21/2018
keywords:
- PendedCompletedRequest2 规则 (wdm)
topic_type:
- apiref
api_name:
- PendedCompletedRequest2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f80370bdce5c058dd394245bfcc690894e618f30
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393687"
---
# <a name="pendedcompletedrequest2-rule-wdm"></a>PendedCompletedRequest2 规则 (wdm)


**PendedCompletedRequest2**规则指定在调用后等待是必需[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)或者[ **PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)因为调度例程无法完成挂起的 IRP。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>PendedCompletedRequest2</strong>规则。</p>
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

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)
[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)
[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)
[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)
[**RemoveHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-removeheadlist)
 

 





