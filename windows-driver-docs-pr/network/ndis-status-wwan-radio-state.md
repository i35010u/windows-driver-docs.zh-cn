---
title: NDIS_STATUS_WWAN_RADIO_STATE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_RADIO_STATE 通知来告知 MB 服务，当用户更改硬件单选强大功能或在 OID 查询响应中的设备的基于软件的单选电源状态更改或设置请求 OID_WWAN_RADIO_状态。 微型端口驱动程序还可以发送未经请求的事件与该通知。此通知使用 NDIS_WWAN_RADIO_STATE 结构。
ms.assetid: 77c10b2a-ab43-4349-947a-e89c7af27f68
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_RADIO_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ef21fbf6deb6098db76301ec423e20596e4c0852
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377586"
---
# <a name="ndisstatuswwanradiostate"></a>NDIS\_STATUS\_WWAN\_RADIO\_STATE


微型端口驱动程序使用 NDIS\_状态\_WWAN\_单选\_状态通知，以在用户更改硬件单选强大功能，或在设备的基于软件的单选电源状态更改时通知 MB 服务对 OID 查询响应或集的请求[OID\_WWAN\_单选\_状态](oid-wwan-radio-state.md)。

微型端口驱动程序还可以发送未经请求的事件与该通知。

使用此通知[ **NDIS\_WWAN\_单选\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)结构。

<a name="remarks"></a>备注
-------

微型端口驱动程序应在查询请求的响应中返回这两种将当前基于硬件的和基于软件的单选电源状态

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_RADIO\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)

[OID\_WWAN\_RADIO\_STATE](oid-wwan-radio-state.md)

 

 




