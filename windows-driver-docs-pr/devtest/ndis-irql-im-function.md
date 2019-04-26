---
title: Irql\_IM\_函数规则 (ndis)
description: Irql\_IM\_函数规则指定必须在正确的 IRQL 级别上名为中间 (IM) 驱动程序的 NDIS 函数。
ms.assetid: f13ee05d-41d5-48e1-aa53-8904d99f94da
ms.date: 05/21/2018
keywords:
- Irql_IM_Function 规则 (ndis)
topic_type:
- apiref
api_name:
- Irql_IM_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8baaa3ad79a4d25ceebd6b427ca60094b3ec4a65
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325107"
---
# <a name="irqlimfunction-rule-ndis"></a>Irql\_IM\_函数规则 (ndis)


Irql\_IM\_函数规则指定必须在正确的 IRQL 级别上名为中间 (IM) 驱动程序的 NDIS 函数。

此规则验证以下 NDIS 函数：

**NdisIMAssociateMiniport**
**NdisIMCancelInitializeDeviceInstance**
**NdisIMDeInitializeDeviceInstance**
**NdisIMGetBindingContext**
**NdisIMInitializeDeviceInstanceEx**

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Irql_IM_Function</strong>规则。</p>
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

[**NdisIMAssociateMiniport**](https://msdn.microsoft.com/library/windows/hardware/ff562717)
[**NdisIMCancelInitializeDeviceInstance** ](https://msdn.microsoft.com/library/windows/hardware/ff562719) 
 [ **NdisIMDeInitializeDeviceInstance**](https://msdn.microsoft.com/library/windows/hardware/ff562721)
[**NdisIMGetBindingContext** ](https://msdn.microsoft.com/library/windows/hardware/ff562724) 
 [ **NdisIMInitializeDeviceInstanceEx**](https://msdn.microsoft.com/library/windows/hardware/ff562727)








