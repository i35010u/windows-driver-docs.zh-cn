---
title: Irql\_协议\_驱动程序\_函数规则 (ndis)
description: Irql\_协议\_驱动程序\_函数规则指定必须在正确的 IRQL 级别上名为的 CoNDIS 客户端的 NDIS 函数。
ms.assetid: 9461c3d9-cb31-4ffd-b057-fd9978808c2f
ms.date: 05/21/2018
keywords:
- Irql_Protocol_Driver_Function 规则 (ndis)
topic_type:
- apiref
api_name:
- Irql_Protocol_Driver_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9feba708928250e45a0093e89c69c047dace89ff
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392302"
---
# <a name="irqlprotocoldriverfunction-rule-ndis"></a>Irql\_协议\_驱动程序\_函数规则 (ndis)


Irql\_协议\_驱动程序\_函数规则指定必须在正确的 IRQL 级别上名为的 CoNDIS 客户端的 NDIS 函数。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>Irql_Protocol_Driver_Function</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用对象
----------

[**NdisClAddParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscladdparty)
[**NdisClCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclcloseaddressfamily)
[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclclosecall) 
 [ **NdisClDeregisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclderegistersap)
[**NdisClDropParty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscldropparty)
 [ **NdisClGetProtocolVcContextFromTapiCallId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclgetprotocolvccontextfromtapicallid)
[**NdisClIncomingCallComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclincomingcallcomplete)
 [ **NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmakecall)
[**NdisClModifyCallQoS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclmodifycallqos) 
 [**NdisClNotifyCloseAddressFamilyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclnotifycloseaddressfamilycomplete)
[**NdisClOpenAddressFamilyEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclopenaddressfamilyex) 
[ **NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)
[**NdisClRegisterSap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclregistersap) 
[ **NdisCompleteBindAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscompletebindadapterex)
[**NdisCompleteNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscompletenetpnpevent) 
 [ **NdisCompleteUnbindAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscompleteunbindadapterex)
[**NdisDeregisterProtocolDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisderegisterprotocoldriver) 
 [ **NdisMNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismnetpnpevent) 
 [ **NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)
[**NdisRegisterProtocolDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver) 
 [**NdisUnbindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisunbindadapter)








