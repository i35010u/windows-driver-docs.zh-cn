---
title: 'WdfIoQueueRetrieveFoundRequest 规则 (kmdf) '
description: WdfIoQueueRetrieveFoundRequest 规则指定仅在调用 WdfIoQueueFindRequest 后调用 WdfIoQueueRetrieveFoundRequest 方法，并 \_ 在同一请求上不调用 WdfObjectDereference。
ms.assetid: CF545174-5E6D-429B-AC6D-BA7A84852FC1
ms.date: 05/21/2018
keywords:
- 'WdfIoQueueRetrieveFoundRequest 规则 (kmdf) '
topic_type:
- apiref
api_name:
- WdfIoQueueRetrieveFoundRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4bf654bfeda9ec5b051a95b769d5388513efd514
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103504"
---
# <a name="wdfioqueueretrievefoundrequest-rule-kmdf"></a>WdfIoQueueRetrieveFoundRequest 规则 (kmdf) 


**WdfIoQueueRetrieveFoundRequest**规则指定仅在调用[**WdfIoQueueFindRequest**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest)后调用[**WdfIoQueueRetrieveFoundRequest**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest)方法，并 \_ 在同一请求上不调用[**WdfObjectDereference**](../wdf/wdfobjectdereference.md) 。

如果 [**WdfIoQueueFindRequest**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest) 返回状态 \_ SUCCESS，它会递增输出请求对象的引用计数，驱动程序必须在使用完此请求句柄后调用 [**WdfObjectDereference**](../wdf/wdfobjectdereference.md) 。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>WdfIoQueueRetrieveFoundRequest</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**WdfIoQueueFindRequest**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuefindrequest) 
[**WdfIoQueueRetrieveFoundRequest**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievefoundrequest) 
[**WdfObjectDereference**](../wdf/wdfobjectdereference.md)
