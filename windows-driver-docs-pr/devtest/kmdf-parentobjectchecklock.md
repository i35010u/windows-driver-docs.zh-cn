---
title: 'ParentObjectCheckLock 规则 (kmdf) '
description: ParentObjectCheckLock 规则指定驱动程序应调用 WdfWaitLockCreate，并将 WdfSpinLockCreate 设置为父对象。
ms.date: 05/21/2018
keywords:
- 'ParentObjectCheckLock 规则 (kmdf) '
topic_type:
- apiref
api_name:
- ParentObjectCheckLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7cd24f05742a041cef31af4e192971383d8cea5f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833559"
---
# <a name="parentobjectchecklock-rule-kmdf"></a>ParentObjectCheckLock 规则 (kmdf) 


**ParentObjectCheckLock** 规则指定驱动程序应调用 [**WdfWaitLockCreate**](/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockcreate) ，并将 [**WdfSpinLockCreate**](/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfspinlockcreate)设置为父对象。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>ParentObjectCheckLock</strong> 规则。</p>
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

[**WdfSpinLockCreate**](/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfspinlockcreate) 
[ **WdfWaitLockCreate**](/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockcreate)
