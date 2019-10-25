---
title: NDIS_STATUS_WWAN_PIN_LIST
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PIN_LIST 通知响应 OID_WWAN_PIN_LIST 的 OID 查询请求。 微型端口驱动程序无法使用此通知发送未经请求的事件。此通知使用 NDIS_WWAN_PIN_LIST 结构。
ms.assetid: fd8e6734-d032-445a-819a-0d5a773e9ea3
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_PIN_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0a27a714d3dbee5c630b683f8fe3f66d9025d03a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844702"
---
# <a name="ndis_status_wwan_pin_list"></a>\_WWAN\_PIN\_列表的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_PIN\_列表通知来响应 oid 的 OID 查询请求， [\_WWAN\_PIN\_列表](oid-wwan-pin-list.md)。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_固定\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)结构。

<a name="remarks"></a>备注
-------

这一指示只响应\_WWAN\_PIN\_列表的 oid 请求 oid 查询。 此指示不应为未经请求的指示。

由于 OID\_WWAN\_PIN 启用或禁用操作导致的 PIN 输入模式中的任何更改都不会导致 NDIS\_状态\_WWAN\_PIN\_列表指示。

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


[OID\_WWAN\_固定\_列表](oid-wwan-pin-list.md)

[**NDIS\_WWAN\_固定\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_list)

 

 




