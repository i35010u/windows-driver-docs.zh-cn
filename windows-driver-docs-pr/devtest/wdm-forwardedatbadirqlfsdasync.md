---
title: ForwardedAtBadIrqlFsdAsync 规则 (wdm)
description: ForwardedAtBadIrqlFsdAsync 规则指定驱动程序在 IRQL 调度中，调用 IoCallDriver 和 PoCallDriver\_级别，除非要转发的 IRP 主要函数代码是一个以下 IRP\_MJ\_POWERIRP\_MJ\_READIRP\_MJ\_WRITEIRP\_MJ\_设备\_CONTROLIRP\_MJ\_内部\_设备\_控件。
ms.assetid: 9961AE5F-0B36-4E04-A349-CA0461B3E3DC
ms.date: 05/21/2018
keywords:
- ForwardedAtBadIrqlFsdAsync 规则 (wdm)
topic_type:
- apiref
api_name:
- ForwardedAtBadIrqlFsdAsync
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bc8f8485e07802626d3ffa403aaa7749a1063220
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544387"
---
# <a name="forwardedatbadirqlfsdasync-rule-wdm"></a>ForwardedAtBadIrqlFsdAsync 规则 (wdm)


**ForwardedAtBadIrqlFsdAsync**规则指定驱动程序调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)并[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)在 IRQL&lt;调度\_级别，除非要转发的 IRP 主要函数代码是以下值之一：

-   [**IRP\_MJ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff550784)
-   [**IRP\_MJ\_READ**](https://msdn.microsoft.com/library/windows/hardware/ff550794)
-   [**IRP\_MJ\_WRITE**](https://msdn.microsoft.com/library/windows/hardware/ff550819)
-   [**IRP\_MJ\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff550744)
-   [**IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff550766)

|              |     |
|--------------|-----|
| 驱动程序模型 | WDM |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>ForwardedAtBadIrqlFsdAsync</strong>规则。</p>
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

<a name="applies-to"></a>适用于
----------

[**IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)
[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 





