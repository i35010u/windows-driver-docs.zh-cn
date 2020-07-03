---
title: ExclusiveResourceAccess 规则（wdm）
description: ExclusiveResourceAccess 规则指定在调用 ExReleaseResourceLite 或 ExReleaseResourceForThreadLite 之前，驱动程序调用 ExAcquireResourceExclusiveLite，并指定驱动程序在对 ExReleaseResourceLite 的任何后续调用之前调用 ExReleaseResourceForThreadLite 或 ExAcquireResourceExclusiveLite。
ms.assetid: 3de539c0-5af2-4ced-8111-44918f4effc4
ms.date: 05/21/2018
keywords:
- ExclusiveResourceAccess 规则（wdm）
topic_type:
- apiref
api_name:
- ExclusiveResourceAccess
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7caee82f64b464d31c2364460283460c8cd2d824
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916135"
---
# <a name="exclusiveresourceaccess-rule-wdm"></a>ExclusiveResourceAccess 规则（wdm）


**ExclusiveResourceAccess**规则指定在调用[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)或[**ExReleaseResourceForThreadLite**](https://msdn.microsoft.com/library/windows/hardware/ff545585)之前，驱动程序调用[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351) ，并指定驱动程序在对**ExReleaseResourceLite**的任何后续调用之前调用**ExReleaseResourceForThreadLite**或**ExAcquireResourceExclusiveLite** 。

如果它们正在获取和释放不同的资源，则允许嵌套调用。 用于获取或释放相同资源的嵌套调用违反了此规则。

此规则还指出，当例程结束时，驱动程序不能以独占方式访问该资源。 静态驱动程序验证器监视**DriverEntry**、 **AddDevice**、 **StartIo**、 **StartDevice**、 **DpcForIsr**、 **Cancel**、**调度**、 **RemoveDevice**和**Unload**例程的结尾。

**驱动程序模型： WDM**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">找到了具有此规则的 Bug 检查</td>
<td align="left"></td>
</tr>
</tbody>
</table>

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>ExclusiveResourceAccess</strong>规则。</p>
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

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351) 
[**ExReleaseResourceForThreadLite**](https://msdn.microsoft.com/library/windows/hardware/ff545585) 
[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)另请参阅
--------

[**使用自旋锁时防止错误和死锁**](https://docs.microsoft.com/windows-hardware/drivers/kernel/preventing-errors-and-deadlocks-while-using-spin-locks)
 

 





