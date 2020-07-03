---
title: DoubleComplete 规则（ndis）
description: DoubleComplete 规则指定 NDIS 驱动程序不得多次完成对象标识符（OID）请求。
ms.assetid: b79aaf92-3536-4409-ac8d-420a5999409c
ms.date: 05/21/2018
keywords:
- DoubleComplete 规则（ndis）
topic_type:
- apiref
api_name:
- DoubleComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fba082fb48123d34f6913ec170c9910e22f9acfa
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917913"
---
# <a name="doublecomplete-rule-ndis"></a>DoubleComplete 规则（ndis）


DoubleComplete 规则指定 NDIS 驱动程序不得多次完成对象标识符（OID）请求。

此规则验证当**MiniportOidRequest**回调函数返回 NDIS \_ 状态成功时 \_ ，不得为该请求调用**NdisMOidRequestComplete**函数。 此规则还指定当**MiniportOidRequest**返回状态 "挂起" 时，驱动程序不得为该请求多次调用**NdisMOidRequestComplete**函数。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>DoubleComplete</strong>规则。</p>
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

[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)
 

 





