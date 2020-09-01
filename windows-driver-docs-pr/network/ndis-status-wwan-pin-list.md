---
title: NDIS_STATUS_WWAN_PIN_LIST
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PIN_LIST 通知来响应 OID_WWAN_PIN_LIST 的 OID 查询请求。 微型端口驱动程序无法使用此通知发送未经请求的事件。此通知使用 NDIS_WWAN_PIN_LIST 结构。
ms.assetid: fd8e6734-d032-445a-819a-0d5a773e9ea3
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_PIN_LIST 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a9fcf69f03fe9d81f7db3fa37c12be7335594092
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217559"
---
# <a name="ndis_status_wwan_pin_list"></a>NDIS \_ 状态 \_ WWAN \_ PIN \_ 列表


微型端口驱动程序使用 NDIS \_ 状态 \_ wwan \_ pin \_ 列表通知来响应 [oid 的 \_ \_ \_ ](oid-wwan-pin-list.md)oid 查询请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ PIN \_ 列表**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list) 结构。

<a name="remarks"></a>备注
-------

此指示仅响应 OID \_ WWAN PIN 列表的 oid 查询请求 \_ \_ 。 此指示不应为未经请求的指示。

由于 OID wwan pin 启用或禁用操作导致 PIN 输入模式中的任何 \_ 更改 \_ 都不会导致 NDIS \_ 状态 \_ wwan \_ pin \_ 列表指示。

请注意，必须更新设备支持的所有 Pin 的当前 PinMode，以反映每个查询请求上微型端口驱动程序的当前状态。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ WWAN \_ PIN \_ 列表](oid-wwan-pin-list.md)

[**NDIS \_ WWAN \_ PIN \_ 列表**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)

 

