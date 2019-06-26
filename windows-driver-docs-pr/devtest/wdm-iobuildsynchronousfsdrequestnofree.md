---
title: IoBuildSynchronousFsdRequestNoFree 规则 (wdm)
description: IoBuildSynchronousFsdRequestNoFree 规则指定调用 IoBuildSynchronousFsdRequest 的驱动程序必须调用 IoFreeIrp。
ms.assetid: 516D6B53-866D-477D-AB9C-6E44BB285BA8
ms.date: 05/21/2018
keywords:
- IoBuildSynchronousFsdRequestNoFree 规则 (wdm)
topic_type:
- apiref
api_name:
- IoBuildSynchronousFsdRequestNoFree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 94afe660f549f5ffee12239cd5bef04dc4ff0a01
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393935"
---
# <a name="iobuildsynchronousfsdrequestnofree-rule-wdm"></a>IoBuildSynchronousFsdRequestNoFree 规则 (wdm)


**IoBuildSynchronousFsdRequestNoFree**规则指定的调用驱动程序[ **IoBuildSynchronousFsdRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)不能调用[ **IoFreeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)。

**IoBuildSynchronousFsdRequestNoFree**规则报告[ **IoFreeIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)不应为此 IRP 调用。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>IoBuildSynchronousFsdRequestNoFree</strong>规则。</p>
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

[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)
[**IoFreeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeirp)
 

 





