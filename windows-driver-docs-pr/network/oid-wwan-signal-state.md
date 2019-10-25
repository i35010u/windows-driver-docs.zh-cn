---
title: OID_WWAN_SIGNAL_STATE
description: OID_WWAN_SIGNAL_STATE 返回或设置当前信号状态。
ms.assetid: 6f5d8fd6-b4cf-4058-a27e-d4f7cea19f47
ms.date: 04/05/2019
keywords: -从 Windows Vista 开始 OID_WWAN_SIGNAL_STATE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c3ef17d56b2dc7e15d01ad33b2fb22825bbd4156
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843791"
---
# <a name="oid_wwan_signal_state"></a>OID\_WWAN\_信号\_状态


OID\_WWAN\_信号\_状态返回或设置当前信号状态。

微型端口驱动程序必须异步处理集和查询请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后发送[**ndis\_状态\_WWAN\_信号 @no**](ndis-status-wwan-signal-state.md)包含[**NDIS\_WWAN\_信号**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)的 __t_8_ 状态通知\_状态结构，以提供与最终用户显示的当前信号状态指示有关的信息，而不考虑完成的集或查询发出.

请求将当前信号状态指示设置为最终用户的调用方提供[**NDIS\_WWAN\_使用适当的信息将\_信号\_指示结构设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_signal_indication)为微型端口驱动程序。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 信号强度操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-signal-strength-operations)。

在处理查询或设置操作时，微型端口驱动程序不应访问提供程序网络或订阅服务器标识模块（SIM 卡）。

通常，应指示信号状态而不是轮询状态。 但是，当当前信号状态需要由 MB 服务确定时，此 OID 可用。

对于对查询请求的响应，微型端口驱动程序应将 NDIS\_状态发送\_WWAN\_信号\_状态通知。

在来自 MB 服务的集请求上，微型端口驱动程序应：

-   返回 NDIS\_WWAN\_信号\_状态结构中的**Rssi**和**ErrorRate**的当前值，并报告**RssiInterval**和**RssiThreshold**的绝对值，这些值已在微型端口驱动程序。

-   即使设备当前未向任何操作员注册，并且设备在设置参数中施加的任何限制只能是注册后状态，在内部缓存**RssiInterval**和/或**RssiThreshold**值。 小型端口驱动程序应尝试在下一个即时可用情况下应用这些设置。

-   如果硬件和/或软件无线电开关状态为 "已关闭"，则已成功完成请求。 微型端口驱动程序缓存请求数据，并在打开交换机后开始报告信号强度。

-   此请求可能会失败，并出现相应的**uStatus**错误代码集。

当处理来自 MB 服务的查询请求时，微型端口驱动程序可以执行以下操作：

-   返回 NDIS\_WWAN\_信号\_状态结构中的**Rssi**和**ErrorRate**的当前值，并报告**RssiInterval**和**RssiThreshold**的绝对值，这些值已在微型端口驱动程序。

-   此请求失败，并出现相应的**uStatus**错误代码集。

返回值：

不\_支持 NDIS\_状态\_

对于识别设备功能不支持信号强度的特定设备，微型端口驱动程序可以返回此错误代码。

**推荐的实现**

1.  设备必须支持信号强度指示。

2.  驱动程序必须在五分钟的时间段内报告至少50% 的**RssiInterval**设置的信号强度指示。

3.  设备必须避免在以下状态下报告信号强度：
    1.  设备未注册或取消注册，仅适用于 GSM 设备。
    2.  无线电的有效状态为 OFF。
    3.  在上述状态中，使用微型端口驱动程序时，必须使用以下数据返回对信号强度的查询：

        Rssi = WWAN\_RSSI\_未知

        ErrorRate = WWAN\_错误\_速率\_未知;

        RssiInterval = &lt; WWAN\_RSSI\_DISABLE，WWAN\_RSSI\_默认值或上次设置的值&gt;

        RssiThreshold = &lt; WWAN\_RSSI\_DISABLE，WWAN\_RSSI\_默认值或最后设置的值&gt;

### <a name="windows-10-version-1903"></a>Windows 10 版本 1903

从 Windows 10 版本1903开始，OID_WWAN_SIGNAL_STATE 已升级到修订版3。 此修订版本允许主机在微型端口驱动程序中查询新的引用信号接收电源（RSRP）和信噪（SNR）值。 如果驱动程序支持5G，微型端口驱动程序必须使用此 OID 的修订版3及其数据结构。

有关5G 数据类支持的详细信息，请参阅[MB 5G 数据类支持](mb-5g-data-class-support.md)。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_设置\_信号\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_signal_indication)

[WWAN 信号强度操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-signal-strength-operations)

 

 




