---
title: Irql \_ MCM \_ 函数规则（ndis）
description: Irql \_ MCM \_ 函数规则指定必须在正确的 Irql 级别调用用于驱动程序的 NDIS MCM 函数。
ms.assetid: 8cd71bf0-92ee-409d-90e3-6bb0c14ebda4
ms.date: 05/21/2018
keywords:
- Irql_MCM_Function 规则（ndis）
topic_type:
- apiref
api_name:
- Irql_MCM_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 71097866035e97a367adb8255997922f80c5b15c
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916207"
---
# <a name="irql_mcm_function-rule-ndis"></a>Irql \_ MCM \_ 函数规则（ndis）


**Irql \_ MCM \_ 函数**规则指定必须在正确的 Irql 级别调用用于驱动程序的 NDIS MCM 函数。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>Irql_MCM_Function</strong>规则。</p>
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

[**NdisMCmActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmactivatevc) 
[**NdisMCmAddPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmaddpartycomplete) 
[**NdisMCmCloseAddressFamilyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmcloseaddressfamilycomplete) 
[**NdisMCmCloseCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmclosecallcomplete) 
[**NdisMCmCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmcreatevc) 
[**NdisMCmDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeactivatevc) 
[**NdisMCmDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdeletevc) 
[**NdisMCmDeregisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmderegistersapcomplete) 
[**NdisMCmDispatchCallConnected**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchcallconnected) 
[**NdisMCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingcall) 
[**NdisMCmDispatchIncomingCallQoSChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingcallqoschange) 
[**NdisMCmDispatchIncomingCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingclosecall) 
[**NdisMCmDispatchIncomingDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingdropparty) 
[**NdisMCmDropPartyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdroppartycomplete) 
[**NdisMCmMakeCallComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmmakecallcomplete) 
[**NdisMCmModifyCallQoSComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmmodifycallqoscomplete) 
[**NdisMCmNotifyCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmnotifycloseaddressfamily) 
[**NdisMCmOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequest) 
[**NdisMCmOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmoidrequestcomplete) 
[**NdisMCmOpenAddressFamilyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmopenaddressfamilycomplete) 
[**NdisMCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregisteraddressfamilyex) 
[**NdisMCmRegisterSapComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregistersapcomplete)
 

 





