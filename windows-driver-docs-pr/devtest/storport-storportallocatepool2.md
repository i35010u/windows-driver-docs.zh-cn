---
title: StorPortAllocatePool2 规则 (storport)
description: 此规则验证微型端口必须尝试对已分配的缓冲区调用 StorPortAllocatePool，而不首先释放。
ms.assetid: 3ECEDFDA-AE04-4DAC-926C-FB19CD955A38
ms.date: 05/21/2018
keywords:
- StorPortAllocatePool2 规则 (storport)
topic_type:
- apiref
api_name:
- StorPortAllocatePool2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bffeb51948987605535da574532982e32fe3d65c
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391860"
---
# <a name="storportallocatepool2-rule-storport"></a>StorPortAllocatePool2 规则 (storport)


此规则验证微型端口必须尝试调用[ **StorPortAllocatePool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportallocatepool)上而不首先释放的分配的缓冲区。

|              |          |
|--------------|----------|
| 驱动程序模型 | Storport |

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>StorPortAllocatePool2</strong>规则。</p>
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

[**StorPortAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportallocatepool)
[**StorPortFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportfreepool)
 

 





