---
title: OID_WWAN_SIGNAL_STATE
description: OID_WWAN_SIGNAL_STATE 返回或设置当前的信号状态。
ms.assetid: 6f5d8fd6-b4cf-4058-a27e-d4f7cea19f47
ms.date: 04/05/2019
keywords: -从 Windows Vista 开始 OID_WWAN_SIGNAL_STATE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e8b2de8da14904a5cd2a1c8a030f9eba1103826a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361155"
---
# <a name="oidwwansignalstate"></a>OID\_WWAN\_SIGNAL\_STATE


OID\_WWAN\_信号\_状态返回或设置当前的信号状态。

微型端口驱动程序必须处理集和查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_信号\_状态**](ndis-status-wwan-signal-state.md)状态通知包含[ **NDIS\_WWAN\_信号\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)结构，以便提供显示给最终用户而不考虑完成设置的当前信号状态指示有关的信息或查询请求。

调用方请求将当前的信号状态指示为最终用户提供[ **NDIS\_WWAN\_设置\_信号\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_signal_indication)结构的相应信息的微型端口驱动程序。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 信号强度操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-signal-strength-operations)。

微型端口驱动程序不能访问提供程序网络或用户识别模块 （SIM 卡），当处理查询或设置操作。

通常情况下，信号状态应指示而轮询一次。 但是，此 OID，可在当前的信号状态需要由 MB 服务情况下。

对查询请求的响应，微型端口驱动程序应发送 NDIS\_状态\_WWAN\_信号\_状态通知。

在从 MB 服务集请求中，微型端口驱动程序应：

-   返回的当前值**Rssi**并**ErrorRate**在 NDIS\_WWAN\_信号\_除了 reporting绝对值状态结构**RssiInterval**并**RssiThreshold**微型端口驱动程序中已设置的。

-   在内部缓存**RssiInterval**和/或**RssiThreshold**值即使该设备当前未注册包含的任何运算符，并可以由中设置参数的设备施加任何限制只能是可能的注册后状态。 微型端口驱动程序应尝试将在下一步的即时可用情况下这些设置应用。

-   请求成功完成，如果硬件和/或软件无线电的开关状态目前处于关闭状态。 微型端口驱动程序缓存请求数据，并启动 reporting 信号强度后切换为打开。

-   无法执行调用此请求与相应**uStatus**错误代码集。

处理来自 MB 服务的查询请求时，微型端口驱动程序可以执行以下操作：

-   返回的当前值**Rssi**并**ErrorRate**在 NDIS\_WWAN\_信号\_除了 reporting绝对值状态结构**RssiInterval**并**RssiThreshold**微型端口驱动程序中已设置的。

-   无法满足此请求与相应**uStatus**错误代码集。

返回值：

NDIS\_状态\_不\_支持

微型端口驱动程序可以返回并注意不支持的信号强度的设备功能的特定设备，此操作可能失败，此错误代码的请求。

**推荐的实现**

1.  设备必须支持信号强度指示。

2.  驱动程序必须报告的在至少 50%的信号强度指示**RssiInterval**五分钟的时间段内设置。

3.  设备必须避免报告处于以下状态的信号强度：
    1.  设备未注册或取消注册和仅适用于 GSM 的设备。
    2.  广播的有效状态为 OFF。
    3.  在上面的状态，对信号强度的查询必须返回以下数据使用微型端口驱动程序：

        Rssi = WWAN\_RSSI\_UNKNOWN

        ErrorRate = WWAN\_ERROR\_RATE\_UNKNOWN;

        RssiInterval = &lt; WWAN\_RSSI\_禁用、 WWAN\_RSSI\_默认或最后一个设置值&gt;

        RssiThreshold = &lt; WWAN\_RSSI\_禁用、 WWAN\_RSSI\_默认值或上次设置的值&gt;

### <a name="windows-10-version-1903"></a>Windows 10 版本 1903

从 Windows 10，版本 1903，开始 OID_WWAN_SIGNAL_STATE 已升级到版本 3。 此修订版本使宿主能够查询新引用接收到信号 power (RSRP) 和-到干扰信号 (SNR) 值从微型端口驱动程序。 如果该驱动程序支持 5g 微型端口驱动程序必须使用修订版 3 的此 OID 和其数据结构。

5 G 数据类支持的详细信息，请参阅[MB 5g 数据类支持](mb-5g-data-class-support.md)。

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
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_SET\_SIGNAL\_INDICATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_signal_indication)

[WWAN 信号强度操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-signal-strength-operations)

 

 




