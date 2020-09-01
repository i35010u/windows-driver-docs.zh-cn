---
title: NDIS_STATUS_WDI_INDICATION_DISASSOCIATION
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_DISASSOCIATION 指示端口与网络断开连接。
ms.assetid: 4e3ed3ed-1b96-49ea-b60f-a36d2a3fc082
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_DISASSOCIATION 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3b3aabeb608c4db3a6760340c696ffdc44210963
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217827"
---
# <a name="ndis_status_wdi_indication_disassociation"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ 解除了


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI 指示解除与网络的 \_ \_ 连接。

| 对象 |
|--------|
| 端口   |

 

断开连接可能是由操作系统中的命令或从网络触发的。 网络触发的断开连接可能是从接收的解除关联或 deauthentication 数据包中显式的，或者当端口无法检测到它连接到的对等节点时，可能是隐式的。

在发送解除关联指示之前，端口必须清除与此对等方关联的状态。 这包括与此对等方关联的任何密钥和 802.1 x 端口授权信息。 端口不能自行触发漫游。

## <a name="payload-data"></a>负载数据


| 类型 | 允许多个 TLV 实例 | 可选 | 说明 |
| --- | --- | --- | --- |
| [**WDI \_ TLV \_ 解除 \_ 指示 \_ 参数**](./wdi-tlv-disassociation-indication-parameters.md) |   |   | 解除标识参数。 |
| [**WDI \_ TLV \_ 断开 \_ DEAUTH \_ 帧**](./wdi-tlv-disconnect-deauth-frame.md) |   | X | 收到的 deauthentication 帧。 这不包括 802.11 MAC 标头。 |
| [**WDI \_ TLV \_ 断开解除连接的 \_ \_ 范围**](./wdi-tlv-disconnect-disassociation-frame.md) |   | X | 接收到的解除其的解除。 这不包括 802.11 MAC 标头。 | 

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
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ WDI \_ TASK \_ 断开连接](oid-wdi-task-disconnect.md)

[OID \_ WDI \_ 任务 \_ 漫游](oid-wdi-task-roam.md)

 

