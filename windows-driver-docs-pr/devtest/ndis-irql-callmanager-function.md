---
title: Irql\_CallManager\_函数规则 (ndis)
description: Irql\_CallManager\_函数规则指定必须在正确的 IRQL 级别上名为 NDIS CallManager 的 NDIS 函数。
ms.assetid: 3e026fb0-8c5f-40cc-affb-3b35f17f40f7
ms.date: 05/21/2018
keywords:
- Irql_CallManager_Function 规则 (ndis)
topic_type:
- apiref
api_name:
- Irql_CallManager_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f453fd4021e215dad8208600ac4c25b062388bc8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554645"
---
# <a name="irqlcallmanagerfunction-rule-ndis"></a>Irql\_CallManager\_函数规则 (ndis)


**Irql\_CallManager\_函数**规则指定必须在正确的 IRQL 级别上名为 NDIS CallManager 的 NDIS 函数。

此规则将检查以下 NDIS 函数：

**NdisCmActivateVc**
**NdisCmAddPartyComplete**
**NdisCmCloseAddressFamilyComplete** 
 **NdisCmCloseCallComplete**
**NdisCmDeactivateVc**
**NdisCmDeregisterSapComplete** 
 **NdisCmDispatchCallConnected**
**NdisCmDispatchIncomingCall**
**NdisCmDispatchIncomingCallQoSChange** 
**NdisCmDispatchIncomingCloseCall**
**NdisCmDispatchIncomingDropParty**
**NdisCmDropPartyComplete**
 **NdisCmMakeCallComplete**
**NdisCmModifyCallQoSComplete**
**NdisCmNotifyCloseAddressFamily**
 **NdisCmOpenAddressFamilyComplete**
**NdisCmRegisterAddressFamilyEx**
**NdisCmRegisterSapComplete**

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Irql_CallManager_Function</strong>规则。</p>
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

[**NdisCmActivateVc**](https://msdn.microsoft.com/library/windows/hardware/ff561649)
[**NdisCmAddPartyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561651)
[**NdisCmCloseAddressFamilyComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561654) 
 [ **NdisCmCloseCallComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561655)
[**NdisCmDeactivateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561657) 
 [ **NdisCmDeregisterSapComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561659)
[**NdisCmDispatchCallConnected** ](https://msdn.microsoft.com/library/windows/hardware/ff561661) 
 [ **NdisCmDispatchIncomingCall**](https://msdn.microsoft.com/library/windows/hardware/ff561664)
[**NdisCmDispatchIncomingCallQoSChange**](https://msdn.microsoft.com/library/windows/hardware/ff561668) 
 [ **NdisCmDispatchIncomingCloseCall**](https://msdn.microsoft.com/library/windows/hardware/ff561670)
[**NdisCmDispatchIncomingDropParty**](https://msdn.microsoft.com/library/windows/hardware/ff561672) 
 [ **NdisCmDropPartyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561674)
[**NdisCmMakeCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561677) 
 [ **NdisCmModifyCallQoSComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561679) 
 [ **NdisCmNotifyCloseAddressFamily**](https://msdn.microsoft.com/library/windows/hardware/ff561680)
[**NdisCmOpenAddressFamilyComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561682) 
[ **NdisCmRegisterAddressFamilyEx**](https://msdn.microsoft.com/library/windows/hardware/ff561685)
[**NdisCmRegisterSapComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561689)








