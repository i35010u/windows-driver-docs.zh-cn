---
title: WlanTimedConnectRequest 规则 (ndis)
description: WlanTimedConnectRequest 规则验证 OID\_DOT11\_CONNECT\_请求后跟 NDIS\_状态\_DOT11\_连接\_在 10 分钟内启动秒数。
ms.assetid: F40D92B1-CA48-4060-B9E2-A965900EAF7B
ms.date: 05/21/2018
keywords:
- WlanTimedConnectRequest 规则 (ndis)
topic_type:
- apiref
api_name:
- WlanTimedConnectRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4d927e784940c11874776372280eb90a02fdf54d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392133"
---
# <a name="wlantimedconnectrequest-rule-ndis"></a>WlanTimedConnectRequest 规则 (ndis)


**WlanTimedConnectRequest**规则验证 OID\_DOT11\_CONNECT\_请求后跟 NDIS\_状态\_DOT11\_连接\_在 10 秒内启动。

此外，NDIS\_状态\_DOT11\_连接\_开始指示仅当 OID\_DOT11\_CONNECT\_请求已完成并且 NDIS\_状态\_成功。 此规则仅适用于可扩展站端口 （端口 0）。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00094009) |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a> ，然后选择<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 验证</a>选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用对象
----------

[**MiniportHaltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)
[**MiniportOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)
[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex) 
 [ **NdisMOidRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismoidrequestcomplete)另请参阅
--------

[常规连接操作指南](https://docs.microsoft.com/windows-hardware/drivers/network/general-connection-operation-guidelines)
 

 





