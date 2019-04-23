---
title: NDIS_STATUS_WDI_INDICATION_DISASSOCIATION
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_DISASSOCIATION 指示与网络断开连接的端口。
ms.assetid: 4e3ed3ed-1b96-49ea-b60f-a36d2a3fc082
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_DISASSOCIATION 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6d0cd33ea71914854021d1f815f6cd58cd44f239
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903127"
---
# <a name="ndisstatuswdiindicationdisassociation"></a>NDIS\_状态\_WDI\_指示\_解除关联


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_解除关联以指示与网络断开连接的端口。

| Object |
|--------|
| 端口   |

 

可能会触发从操作系统命令或触发从网络断开连接。 触发的网络断开连接可能显式从接收到的解除关联或 deauthentication 数据包，或者可能隐式端口不能检测连接到的对等方的状态。

解除关联指示在发送之前，该端口必须清除与此对等方关联的状态。 这包括任何密钥以及与此对等方关联的 802.1 x 端口授权信息。 该端口不得触发其自身上的漫游。

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- |
| [**WDI\_TLV\_解除关联\_指示\_参数**](https://msdn.microsoft.com/library/windows/hardware/dn926292) |   |   | 解除关联指示参数。 |
| [**WDI\_TLV\_DISCONNECT\_DEAUTH\_FRAME**](https://msdn.microsoft.com/library/windows/hardware/dn926296) |   | X | 已接收到 deauthentication 帧。 这不包括 802.11 MAC 报头。 |
| [**WDI\_TLV\_DISCONNECT\_DISASSOCIATION\_FRAME**](https://msdn.microsoft.com/library/windows/hardware/dn926298) |   | X | 已接收到解除关联框架。 这不包括 802.11 MAC 报头。 | 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WDI\_TASK\_DISCONNECT](oid-wdi-task-disconnect.md)

[OID\_WDI\_TASK\_ROAM](oid-wdi-task-roam.md)

 

 




