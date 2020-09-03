---
title: 'Irql \_ CallManager \_ 函数规则 (ndis) '
description: Irql \_ CallManager \_ 函数规则指定必须在正确的 Irql 级别调用 ndis CALLMANAGER 的 ndis 函数。
ms.assetid: 3e026fb0-8c5f-40cc-affb-3b35f17f40f7
ms.date: 05/21/2018
keywords:
- 'Irql_CallManager_Function 规则 (ndis) '
topic_type:
- apiref
api_name:
- Irql_CallManager_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ca1ced6fde2d6e0b1e6fc93e0b55727cf32b8873
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383783"
---
# <a name="irql_callmanager_function-rule-ndis"></a>Irql \_ CallManager \_ 函数规则 (ndis) 


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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>Irql_CallManager_Function</strong> 规则。</p>
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

[**NdisCmActivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmactivatevc) 
[**NdisCmAddPartyComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmaddpartycomplete) 
[**NdisCmCloseAddressFamilyComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmcloseaddressfamilycomplete) 
[**NdisCmCloseCallComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmclosecallcomplete) 
[**NdisCmDeactivateVc**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdeactivatevc) 
[**NdisCmDeregisterSapComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmderegistersapcomplete) 
[**NdisCmDispatchCallConnected**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchcallconnected) 
[**NdisCmDispatchIncomingCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcall) 
[**NdisCmDispatchIncomingCallQoSChange**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcallqoschange) 
[**NdisCmDispatchIncomingCloseCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingclosecall) 
[**NdisCmDispatchIncomingDropParty**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingdropparty) 
[**NdisCmDropPartyComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdroppartycomplete) 
[**NdisCmMakeCallComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmmakecallcomplete) 
[**NdisCmModifyCallQoSComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmmodifycallqoscomplete) 
[**NdisCmNotifyCloseAddressFamily**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmnotifycloseaddressfamily) 
[**NdisCmOpenAddressFamilyComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmopenaddressfamilycomplete) 
[**NdisCmRegisterAddressFamilyEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex) 
[**NdisCmRegisterSapComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregistersapcomplete)