---
title: 'IrqlKeWaitForMutexObject 规则 (wdm) '
ms.assetid: f2e7b733-1746-4db5-b4a9-becd211e40cf
ms.date: 05/21/2018
description: ''
keywords:
- 'IrqlKeWaitForMutexObject 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrqlKeWaitForMutexObject
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 243dc70b8d16b7ac283275ec48d10ec7f59e33f1
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384873"
---
# <a name="irqlkewaitformutexobject-rule-wdm"></a>IrqlKeWaitForMutexObject 规则 (wdm) 


**IrqlKeWaitForMutexObject**规则根据*Timeout*参数的值，指定要在适当 IRQL 处调用[**KeWaitForMutexObject**](https://msdn.microsoft.com/library/windows/hardware/ff553344)例程的驱动程序：

-   如果 *Timeout* 的值为零，则驱动程序将以 IRQL = 调度 \_ 级别执行。

-   如果 *Timeout* 为 **NULL**，或指向非零的任何值，则驱动程序将以 IRQL &lt; = APC \_ 级别执行。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrqlKeWaitForMutexObject</strong> 规则。</p>
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

[**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)
 

