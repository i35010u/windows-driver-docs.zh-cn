---
title: 'PagedCodeAtD0 规则 (kmdf) '
description: PagedCodeAtD0 规则指定驱动程序不得将代码标记为可在开机代码路径中的回调函数内进行分页。
ms.assetid: e3e0ee8f-eebe-4855-be35-3d8b153dd09e
ms.date: 05/21/2018
keywords:
- 'PagedCodeAtD0 规则 (kmdf) '
topic_type:
- apiref
api_name:
- PagedCodeAtD0
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 55466251737edc27d61b5ca0b741f8114b9c91bc
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381975"
---
# <a name="pagedcodeatd0-rule-kmdf"></a>PagedCodeAtD0 规则 (kmdf) 


**PagedCodeAtD0**规则指定驱动程序不得将代码标记为可在开机代码路径中的回调函数内进行分页。

当函数标记为 "可分页" 并且代码部分随后被分页时，该函数将生成页错误，这可能会影响计算机的快速恢复行为。 发生这种情况的原因是客户端驱动程序必须等待系统驱动程序可以为此页错误服务。

**驱动程序模型： KMDF**

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>PagedCodeAtD0</strong> 规则。</p>
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

<a name="applies-to"></a>适用于
----------

[**分页 \_ 代码**](../kernel/mm-bad-pointer.md)
 

