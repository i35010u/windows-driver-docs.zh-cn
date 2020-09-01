---
title: NDIS_STATUS_WDI_INDICATION_RADIO_STATUS
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_RADIO_STATUS 来指示适配器无线电状态发生的更改。
ms.assetid: c2f90a52-ce55-4819-a66a-cfcc591cb3e9
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_RADIO_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e1e73f40d2ba2a3d70a16b091901e0ac6eb2af29
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209699"
---
# <a name="ndis_status_wdi_indication_radio_status"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ 无线电 \_ 状态


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ 广播 \_ 状态来指示适配器无线电状态发生的更改。 当主机触发软件无线电更改时，以及适配器检测到硬件无线电状态更改时，会发送此未经请求的指示。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 类型                                                                  | 允许多个 TLV 实例 | 可选 | 说明                                              |
|-----------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------|
| [**WDI \_ TLV \_ 无线电 \_ 状态**](./wdi-tlv-radio-state-parameters.md) |                                |          | 硬件和软件中的无线电的当前状态。 |

 

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


[WDI \_ 任务 \_ 集 \_ 无线电 \_ 状态](oid-wdi-task-set-radio-state.md)

 

