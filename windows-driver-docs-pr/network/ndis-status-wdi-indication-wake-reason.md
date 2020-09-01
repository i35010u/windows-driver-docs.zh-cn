---
title: NDIS_STATUS_WDI_INDICATION_WAKE_REASON
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_WAKE_REASON 指示 NIC 唤醒主机时的唤醒原因。 "唤醒原因" 用于调试目的，并且没有功能效果。
ms.assetid: 5f2eb569-be1e-4f24-92f5-8405ffc7b061
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_WAKE_REASON 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1ebb2a56867233a61e7cc7e0a510e09a19c6c2b2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209695"
---
# <a name="ndis_status_wdi_indication_wake_reason"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ 唤醒 \_ 原因


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ 唤醒 \_ 原因指示 NIC 唤醒主机时的唤醒原因。 "唤醒原因" 用于调试目的，并且没有功能效果。

| 对象 |
|--------|
| 端口   |

 

当主机进入低功耗状态时，它会将一些功能卸载到 NIC，并使 NIC 看起来唤醒。 唤醒事件发生时，NIC 将断言唤醒中断行来唤醒主机。 然后，主机会将 NIC 引入 D0 (电源状态) 。 NIC 进入 D0 后，必须指示唤醒原因。

如果唤醒原因为唤醒数据包，则 NIC 还应包括与数据包匹配的唤醒数据包和唤醒模式 ID。 数据包封装为 [**WDI \_ TLV \_ 指示 \_ 唤醒 \_ 数据包**](./wdi-tlv-indication-wake-packet.md)。 唤醒原因还应包括 [**WDI \_ TLV \_ 指示 \_ 唤醒 \_ 数据包 \_ 模式 \_ id**](./wdi-tlv-indication-wake-packet-pattern-id.md) ，以指定与数据包匹配的模式 id。

## <a name="payload-data"></a>负载数据


| 类型                                                                                                      | 允许多个 TLV 实例 | 可选 | 说明                                                                                                 |
|-----------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 指示 \_ 唤醒 \_ 原因**](./wdi-tlv-indication-wake-reason.md)                         |                                |          | 唤醒原因。                                                                                            |
| [**WDI \_ TLV \_ 指示 \_ 唤醒 \_ 数据包**](./wdi-tlv-indication-wake-packet.md)                         |                                | X        | 唤醒数据包。                                                                                            |
| [**WDI \_ TLV \_ 指示 \_ 唤醒 \_ 数据包 \_ 模式 \_ ID**](./wdi-tlv-indication-wake-packet-pattern-id.md) |                                | X        | 与唤醒数据包匹配的模式的 ID。 此 ID 是从模式的 Add 命令获取的。 |

 

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

 

