---
title: CompletionEventChecking 规则（wdm）
description: CompletionEventChecking 规则指定，驱动程序不会在同一 IRP 的完成例程中调用也和 KeSetEvent。
ms.assetid: C319C472-4715-4703-8F8D-4C769615A3BD
ms.date: 05/21/2018
keywords:
- CompletionEventChecking 规则（wdm）
topic_type:
- apiref
api_name:
- CompletionEventChecking
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ad0a78a6765c5b72de8ce0d9b80f63583a54ac47
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916836"
---
# <a name="completioneventchecking-rule-wdm"></a>CompletionEventChecking 规则（wdm）


**CompletionEventChecking**规则指定，驱动程序不会在同一 IRP 的完成例程中调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)和[**KeSetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent) 。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>CompletionEventChecking</strong>规则。</p>
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

[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 
[ **KeSetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)
 

 





