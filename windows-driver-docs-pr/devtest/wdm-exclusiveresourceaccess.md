---
title: ExclusiveResourceAccess 规则 (wdm)
description: ExclusiveResourceAccess 规则指定驱动程序在调用 ExReleaseResourceLite 或 ExReleaseResourceForThreadLite 之前调用 ExAcquireResourceExclusiveLite，并指定驱动程序调用 ExReleaseResourceLite 或ExReleaseResourceForThreadLite 之前 ExAcquireResourceExclusiveLite 对任何后续调用。
ms.assetid: 3de539c0-5af2-4ced-8111-44918f4effc4
ms.date: 05/21/2018
keywords:
- ExclusiveResourceAccess 规则 (wdm)
topic_type:
- apiref
api_name:
- ExclusiveResourceAccess
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 09fcfbe63fb7dc78b280ef5e91a5bf94f14d5a8f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562400"
---
# <a name="exclusiveresourceaccess-rule-wdm"></a>ExclusiveResourceAccess 规则 (wdm)


**ExclusiveResourceAccess**规则指定驱动程序调用[ **ExAcquireResourceExclusiveLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544351)之前调用[ **ExReleaseResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545597)或[ **ExReleaseResourceForThreadLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545585) ，并指定驱动程序调用**ExReleaseResourceLite**或**ExReleaseResourceForThreadLite**之前对任何后续调用**ExAcquireResourceExclusiveLite**。

允许使用嵌套的调用，如果它们是获得和释放不同的资源。 获取或释放相同资源的嵌套的调用违反此规则。

此规则还说明例程结束时，该驱动程序必须具有对资源的独占访问权限。 Static Driver Verifier 监视末尾**DriverEntry**， **AddDevice**， **StartIo**， **StartDevice**， **DpcForIsr**，**取消**，**调度**， **RemoveDevice**，并且**卸载**例程。

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">使用此规则发现的错误检查</td>
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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>ExclusiveResourceAccess</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)
[**ExReleaseResourceForThreadLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545585) 
 [ **ExReleaseResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545597)另请参阅
--------

[**防止错误和死锁，而使用数值调节钮锁定**](https://msdn.microsoft.com/library/windows/hardware/ff559854)
 

 





