---
title: Irql \_ CallManager \_ 函数规则（ndis）
description: Irql \_ CallManager \_ 函数规则指定必须在正确的 Irql 级别调用 ndis CALLMANAGER 的 ndis 函数。
ms.assetid: 3e026fb0-8c5f-40cc-affb-3b35f17f40f7
ms.date: 05/21/2018
keywords:
- Irql_CallManager_Function 规则（ndis）
topic_type:
- apiref
api_name:
- Irql_CallManager_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1a5c275df697433842aa4f782326979a87331f6d
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917795"
---
# <a name="irql_callmanager_function-rule-ndis"></a>Irql \_ CallManager \_ 函数规则（ndis）


**Irql \_ CallManager \_ 函数**规则指定必须在正确的 Irql 级别调用 ndis CallManager 的 ndis 函数。

此规则检查以下 NDIS 函数：

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

**驱动程序模型： NDIS**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>Irql_CallManager_Function</strong>规则。</p>
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

[**NdisCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmactivatevc) 
[**NdisCmAddPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmaddpartycomplete) 
[**NdisCmCloseAddressFamilyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmcloseaddressfamilycomplete) 
[**NdisCmCloseCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmclosecallcomplete) 
[**NdisCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc) 
[**NdisCmDeregisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmderegistersapcomplete) 
[**NdisCmDispatchCallConnected**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchcallconnected) 
[**NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcall) 
[**NdisCmDispatchIncomingCallQoSChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcallqoschange) 
[**NdisCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingclosecall) 
[**NdisCmDispatchIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingdropparty) 
[**NdisCmDropPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdroppartycomplete) 
[**NdisCmMakeCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmmakecallcomplete) 
[**NdisCmModifyCallQoSComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmmodifycallqoscomplete) 
[**NdisCmNotifyCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmnotifycloseaddressfamily) 
[**NdisCmOpenAddressFamilyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmopenaddressfamilycomplete) 
[**NdisCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex) 
[**NdisCmRegisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregistersapcomplete)








