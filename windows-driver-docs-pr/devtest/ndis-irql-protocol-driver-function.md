---
title: 'Irql \_ 协议 \_ 驱动程序 \_ 函数规则 (ndis) '
description: Irql \_ 协议 \_ 驱动程序 \_ 函数规则指定 CoNDIS 客户端的 NDIS 函数必须以正确的 Irql 级别进行调用。
ms.assetid: 9461c3d9-cb31-4ffd-b057-fd9978808c2f
ms.date: 05/21/2018
keywords:
- 'Irql_Protocol_Driver_Function 规则 (ndis) '
topic_type:
- apiref
api_name:
- Irql_Protocol_Driver_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7586b977f699532a8b6db9cfb218003ed812112f
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105840"
---
# <a name="irql_protocol_driver_function-rule-ndis"></a>Irql \_ 协议 \_ 驱动程序 \_ 函数规则 (ndis) 


Irql \_ 协议 \_ 驱动程序 \_ 函数规则指定 CoNDIS 客户端的 NDIS 函数必须以正确的 Irql 级别进行调用。

此规则验证以下 NDIS 函数：

**NdisClAddParty** 
**NdisClCloseAddressFamily** 
**NdisClCloseCall** 
**NdisClDeregisterSap** 
**NdisClDropParty** 
**NdisClGetProtocolVcContextFromTapiCallId** 
**NdisClIncomingCallComplete** 
**NdisClMakeCall** 
**NdisClModifyCallQoS** 
**NdisClNotifyCloseAddressFamilyComplete** 
**NdisClOpenAddressFamilyEx** 
**NdisCloseAdapterEx** 
**NdisClRegisterSap** 
**NdisCompleteBindAdapterEx** 
**NdisCompleteNetPnPEvent** 
**NdisCompleteUnbindAdapterEx** 
**NdisDeregisterProtocolDriver** 
**NdisMNetPnPEvent** 
**NdisOpenAdapterEx** 
**NdisRegisterProtocolDriver** 
**NdisUnbindAdapter**

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>Irql_Protocol_Driver_Function</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**NdisClAddParty**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscladdparty) 
[**NdisClCloseAddressFamily**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclcloseaddressfamily) 
[**NdisClCloseCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall) 
[**NdisClDeregisterSap**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclderegistersap) 
[**NdisClDropParty**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty) 
[**NdisClGetProtocolVcContextFromTapiCallId**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclgetprotocolvccontextfromtapicallid) 
[**NdisClIncomingCallComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclincomingcallcomplete) 
[**NdisClMakeCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall) 
[**NdisClModifyCallQoS**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmodifycallqos) 
[**NdisClNotifyCloseAddressFamilyComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclnotifycloseaddressfamilycomplete) 
[**NdisClOpenAddressFamilyEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex) 
[**NdisCloseAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex) 
[**NdisClRegisterSap**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap) 
[**NdisCompleteBindAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompletebindadapterex) 
[**NdisCompleteNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompletenetpnpevent) 
[**NdisCompleteUnbindAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompleteunbindadapterex) 
[**NdisDeregisterProtocolDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisderegisterprotocoldriver) 
[**NdisMNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent) 
[**NdisOpenAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex) 
[**NdisRegisterProtocolDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver) 
[**NdisUnbindAdapter**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisunbindadapter)