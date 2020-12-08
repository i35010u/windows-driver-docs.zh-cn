---
title: NDIS_STATUS_WWAN_RADIO_STATE
description: 小型端口驱动程序使用 NDIS_STATUS_WWAN_RADIO_STATE 通知来通知 MB 服务，当用户更改硬件无线电功能，或设备的基于软件的无线电电源状态发生变化时，响应 OID 查询或设置 OID_WWAN_RADIO_STATE 的请求。 小型端口驱动程序还可以通过此通知发送未经请求的事件。此通知使用 NDIS_WWAN_RADIO_STATE 结构。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_RADIO_STATE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6255d4bdf36c6a9ee3aac441d04ab9a7525fd8e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839473"
---
# <a name="ndis_status_wwan_radio_state"></a>NDIS \_ 状态 \_ WWAN \_ 无线电 \_ 状态


小型端口驱动程序使用 NDIS \_ 状态 \_ WWAN \_ 无线电 \_ 状态通知来通知 MB 服务用户更改硬件无线电功能，或设备的基于软件的无线电电源状态更改以响应 oid 查询或设置对 [oid \_ WWAN \_ 无线电 \_ 状态](oid-wwan-radio-state.md)的请求。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ 无线电 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state) 结构。

<a name="remarks"></a>备注
-------

小型端口驱动程序应同时返回当前基于硬件和基于软件的无线电电源状态以响应查询请求

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

## <a name="see-also"></a>请参阅


[**NDIS \_ WWAN \_ 无线电 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)

[OID \_ WWAN \_ 无线电 \_ 状态](oid-wwan-radio-state.md)

 

