---
title: NDIS_STATUS_WWAN_SIGNAL_STATE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SIGNAL_STATE 通知将发送信号强度通知时测量信号强度旅行在阈值之外的预定义的间隔内。
ms.assetid: b5d6b2a6-ed19-45d9-85ca-ac66e38f41fd
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SIGNAL_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7cb20e46bf69c79c37a4bcddbb2ce3486fd0bcd8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386864"
---
# <a name="ndisstatuswwansignalstate"></a>NDIS\_状态\_WWAN\_信号\_状态


微型端口驱动程序使用 NDIS\_状态\_WWAN\_信号\_状态通知将发送信号强度通知时测量信号强度旅行在阈值之外的预定义的间隔内.

微型端口驱动程序还可以发送未经请求的事件与该通知。

使用此通知[ **NDIS\_WWAN\_信号\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)结构。

<a name="remarks"></a>备注
-------

默认情况下，微型端口驱动程序必须通知 MB 服务通过 Rssi 值更改至少 + /-5 分贝自上一个报告的值，或一个指示每隔 5 秒的最大频率。 中指定的阈值**SignalState.RssiThreshold**成员的 NDIS\_WWAN\_信号\_状态结构; 而中指定的最大频率值**SignalState.RssiInterval**成员。

**DeviceCaps.WwanCellularClass**成员的 NDIS\_WWAN\_设备\_CAPS 结构控制 MB 服务将如何解释 Rssi 值。 如果**WwanCellularClass**是**WwanCellularClassGSM**，Rssi 报告为分贝以上设备的敏感度噪音基底。 如果**WwanCellularClass**是**WwanCellularClassCDMA**，Rssi 报告为补偿 RSSI （干扰的帐户）。

应用程序应永远不会轮询信号强度。 应用程序可能只在特殊情况下，如启动时，使用*查询*请求以获取信号强度。

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


[**NDIS\_WWAN\_SIGNAL\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)

[OID\_WWAN\_SIGNAL\_STATE](oid-wwan-signal-state.md)

 

 




