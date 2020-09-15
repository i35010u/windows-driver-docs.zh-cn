---
title: 'ParentObjectCheck 规则 (kmdf) '
description: ParentObjectCheck 规则指定驱动程序应调用 WdfMemoryCreate，并使用 WDF \_ 对象属性结构来指定父对象 \_ 。
ms.assetid: E0597996-9067-40C3-8DE9-1048B2227F07
ms.date: 05/21/2018
keywords:
- 'ParentObjectCheck 规则 (kmdf) '
topic_type:
- apiref
api_name:
- ParentObjectCheck
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0a3231d88c9aa843f710e5b81c97540dc56dc14e
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103826"
---
# <a name="parentobjectcheck-rule-kmdf"></a>ParentObjectCheck 规则 (kmdf) 


**ParentObjectCheck**规则指定驱动程序应调用[**WdfMemoryCreate**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate) ，并使用[**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构来指定父对象。 如果驱动程序没有为 framework 内存对象设置父对象，则该框架会将该驱动程序设置为默认父级，因此，除非驱动程序显式删除框架内存对象，否则该驱动程序对象将保留在内存中，直到驱动程序对象卸载。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>ParentObjectCheck</strong> 规则。</p>
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

[**WdfMemoryCreate**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate)
