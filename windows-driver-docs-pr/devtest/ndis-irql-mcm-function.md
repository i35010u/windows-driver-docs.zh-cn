---
title: Irql\_MCM\_函数规则 (ndis)
description: Irql\_MCM\_函数规则指定必须在正确的 IRQL 级别上名为驱动程序的 NDIS MCM 函数。
ms.assetid: 8cd71bf0-92ee-409d-90e3-6bb0c14ebda4
ms.date: 05/21/2018
keywords:
- Irql_MCM_Function 规则 (ndis)
topic_type:
- apiref
api_name:
- Irql_MCM_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b32d8424fee67e567be122b6ebf84699eaa0d6ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532977"
---
# <a name="irqlmcmfunction-rule-ndis"></a>Irql\_MCM\_函数规则 (ndis)


**Irql\_MCM\_函数**规则指定必须在正确的 IRQL 级别上名为驱动程序的 NDIS MCM 函数。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Irql_MCM_Function</strong>规则。</p>
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

[**NdisMCmActivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff562792)
[**NdisMCmAddPartyComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562798) 
 [ **NdisMCmCloseAddressFamilyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff562800)
[**NdisMCmCloseCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562803) 
 [ **NdisMCmCreateVc**](https://msdn.microsoft.com/library/windows/hardware/ff562812)
[**NdisMCmDeactivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff562818)
[**NdisMCmDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562819) 
 [ **NdisMCmDeregisterSapComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff562821) 
 [ **NdisMCmDispatchCallConnected**](https://msdn.microsoft.com/library/windows/hardware/ff562826)
[**NdisMCmDispatchIncomingCall** ](https://msdn.microsoft.com/library/windows/hardware/ff562830) 
 [ **NdisMCmDispatchIncomingCallQoSChange**](https://msdn.microsoft.com/library/windows/hardware/ff563540)
[**NdisMCmDispatchIncomingCloseCall** ](https://msdn.microsoft.com/library/windows/hardware/ff563541) 
 [ **NdisMCmDispatchIncomingDropParty**](https://msdn.microsoft.com/library/windows/hardware/ff563542)
[**NdisMCmDropPartyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563543) 
 [ **NdisMCmMakeCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563544) 
 [ **NdisMCmModifyCallQoSComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563545)
[**NdisMCmNotifyCloseAddressFamily** ](https://msdn.microsoft.com/library/windows/hardware/ff563546) 
 [**NdisMCmOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff563548)
[**NdisMCmOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563551) 
[ **NdisMCmOpenAddressFamilyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563552)
[**NdisMCmRegisterAddressFamilyEx**](https://msdn.microsoft.com/library/windows/hardware/ff563554) 
 [ **NdisMCmRegisterSapComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563557)
 

 





