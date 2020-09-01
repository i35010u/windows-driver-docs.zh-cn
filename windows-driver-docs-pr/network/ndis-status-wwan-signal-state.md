---
title: NDIS_STATUS_WWAN_SIGNAL_STATE
description: 小型端口驱动程序使用 NDIS_STATUS_WWAN_SIGNAL_STATE 通知在预定义的时间间隔内，当测量信号强度超出阈值时发送信号强度通知。
ms.assetid: b5d6b2a6-ed19-45d9-85ca-ac66e38f41fd
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SIGNAL_STATE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f0565b356d358e70c4c50c6cfba780c2f8920836
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211691"
---
# <a name="ndis_status_wwan_signal_state"></a>NDIS \_ 状态 \_ WWAN \_ 信号 \_ 状态


小型端口驱动程序使用 NDIS \_ 状态 \_ WWAN \_ 信号 \_ 状态通知在预定义的时间间隔内使用超出阈值的信号强度时发送信号强度通知。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 结构。

<a name="remarks"></a>备注
-------

默认情况下，微型端口驱动程序必须在 Rssi 值更改时从上一次报告的值中至少发生 +/-5 分贝，或每5秒一次指示的最大频率。 阈值是在 NDIS WWAN 信号状态结构的**RssiThreshold**成员中指定的 \_ ， \_ 而 SignalState \_ 成员中指定的最大频率值**SignalState.RssiInterval**为。

NDIS WWAN 设备 cap 结构的 **DeviceCaps. WwanCellularClass** 成员 \_ \_ \_ 控制 MB 服务将如何解释 Rssi 值。 如果 **WwanCellularClass** 为 **WwanCellularClassGSM**，则 Rssi 将报告为设备敏感度噪音楼层以上的分贝。 如果 **WwanCellularClass** 为 **WwanCellularClassCDMA**，则 Rssi 将报告为)  (帐户，以的噪音。

应用程序永远不会轮询信号强度。 仅在特殊情况下（如启动），应用程序可以使用 *查询* 请求来获取信号强度。

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


[**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)

[OID \_ WWAN \_ 信号 \_ 状态](oid-wwan-signal-state.md)

 

