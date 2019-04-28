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
ms.openlocfilehash: 1a3082c21af570a061f7069cf67941f837955e5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347652"
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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Irql_Protocol_Driver_Function</strong>规则。</p>
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

[**NdisClAddParty**](https://msdn.microsoft.com/library/windows/hardware/ff561625)
[**NdisClCloseAddressFamily**](https://msdn.microsoft.com/library/windows/hardware/ff561626)
[**NdisClCloseCall**](https://msdn.microsoft.com/library/windows/hardware/ff561627) 
 [ **NdisClDeregisterSap**](https://msdn.microsoft.com/library/windows/hardware/ff561628)
[**NdisClDropParty** ](https://msdn.microsoft.com/library/windows/hardware/ff561629)
 [ **NdisClGetProtocolVcContextFromTapiCallId**](https://msdn.microsoft.com/library/windows/hardware/ff561631)
[**NdisClIncomingCallComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561632)
 [ **NdisClMakeCall**](https://msdn.microsoft.com/library/windows/hardware/ff561635)
[**NdisClModifyCallQoS** ](https://msdn.microsoft.com/library/windows/hardware/ff561636) 
 [**NdisClNotifyCloseAddressFamilyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561638)
[**NdisClOpenAddressFamilyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561639) 
[ **NdisCloseAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561640)
[**NdisClRegisterSap** ](https://msdn.microsoft.com/library/windows/hardware/ff561648) 
[ **NdisCompleteBindAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561702)
[**NdisCompleteNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561705) 
 [ **NdisCompleteUnbindAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff561708)
[**NdisDeregisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff561743) 
 [ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616) 
 [ **NdisOpenAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff563715)
[**NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520) 
 [**NdisUnbindAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff564630)








