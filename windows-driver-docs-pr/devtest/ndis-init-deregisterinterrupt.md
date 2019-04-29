---
title: Init\_DeRegisterInterrupt 规则 (ndis)
description: Init\_DeRegisterInterrupt 规则指定是否至少一次在 MPInitilize 过程中调用 NdisMRegisterInterruptEx，NdisMDeregisterInterruptEx 应调用至少一次 MPHaltEx 中。
ms.assetid: C7436321-43DD-4B38-A0A3-9888CFDDA284
ms.date: 05/21/2018
keywords:
- Init_DeRegisterInterrupt 规则 (ndis)
topic_type:
- apiref
api_name:
- Init_DeRegisterInterrupt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 609491b68bd7080e18be58564eb20e16558508ea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360771"
---
# <a name="initderegisterinterrupt-rule-ndis"></a>Init\_DeRegisterInterrupt 规则 (ndis)


**Init\_DeRegisterInterrupt**规则指定，如果[ **NdisMRegisterInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563649)期间 MPInitilize，至少一次调用[ **NdisMDeregisterInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563575) MPHaltEx 应至少一次调用。

注册的中断，通常会发生在初始化期间，应撤消 （取消注册） 如果出现问题或过程的微型端口停止初始化过程中。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Init_DeRegisterInterrupt</strong>规则。</p>
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

[**NdisMDeregisterInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff563575)
[**NdisMRegisterInterruptEx**](https://msdn.microsoft.com/library/windows/hardware/ff563649)
 

 





