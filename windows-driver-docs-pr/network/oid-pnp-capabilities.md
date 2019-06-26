---
title: OID_PNP_CAPABILITIES
description: OID_PNP_CAPABILITIES OID 请求微型端口驱动程序返回其网络适配器的唤醒功能或请求返回中间驱动程序的唤醒功能的中间驱动程序。
ms.assetid: f2e3a867-d7d2-4d09-b84b-e8f8610b8535
ms.date: 08/08/2017
keywords: -OID_PNP_CAPABILITIES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b7f536a86cfcbb8d9a0f95ef55191bdfba1bfee1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380848"
---
# <a name="oidpnpcapabilities"></a>OID\_PNP\_功能


OID\_PNP\_功能 OID 请求微型端口驱动程序返回其网络适配器的唤醒功能或请求返回中间驱动程序的唤醒功能的中间驱动程序。 唤醒功能的格式为**NDIS\_PNP\_功能**结构，定义如下：

```C++
    typedef struct _NDIS_PNP_CAPABILITIES {
         ULONG Flags;
         NDIS_PM_WAKE_UP_CAPABILITIES WakeUpCapabilities;
    } NDIS_PNP_CAPABILITIES, *PNDIS_PNP_CAPABILITIES;  
```




此结构的成员包含下列信息：

<a href="" id="flags"></a>**标志**  
**NDIS\_DEVICE\_WAKE\_UP\_ENABLE**

NDIS 设置此标志，如果基础微型端口驱动程序支持一个或多个唤醒功能。 协议驱动程序可以测试此标志，以确定基础的微型端口驱动程序是否已唤醒功能。 微型端口驱动程序不应访问此标志。

<a href="" id="wakeupcapabilities"></a>**WakeUpCapabilities**  
**NDIS\_PM\_唤醒\_向上\_功能**结构，它指定微型端口驱动程序的网络适配器的唤醒功能。 **NDIS\_PM\_唤醒\_向上\_功能**结构定义，如下所示：

```C++
typedef struct _NDIS_PM_WAKE_UP_CAPABILITIES {
         NDIS_DEVICE_POWER_STATE MinMagicPacketWakeUp;
         NDIS_DEVICE_POWER_STATE MinPatternWakeUp;
         NDIS_DEVICE_POWER_STATE MinLinkChangeWakeUp;
       } NDIS_PM_WAKE_UP_CAPABILITIES, *PNDIS_PM_WAKE_UP_CAPABILITIES;
```

此结构的成员包含下列信息：

<a href="" id="minmagicpacketwakeup"></a>**MinMagicPacketWakeUp**  
指定从其微型端口驱动程序的网络适配器可以指示在接收幻数据包唤醒的最低设备电源状态。 (A*幻数据包*是包含 16 个连续副本接收的网络适配器的以太网地址的数据包。)设备电源状态指定为以下值之一[ **NDIS\_设备\_POWER\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_device_power_state)值：

<a href="" id="ndisdevicestateunspecified"></a>**NdisDeviceStateUnspecified**  
网络适配器不支持幻数据包唤醒 ups。

<a href="" id="ndisdevicestated0"></a>**NdisDeviceStateD0**  
网络适配器，可以从设备电源状态 D0 发出幻数据包唤醒。 由于 D0 是完全通电的状态，这并不会导致唤醒，但可以用作运行时事件。

<a href="" id="ndisdevicestated1"></a>**NdisDeviceStateD1**  
网络适配器，可以从设备的电源状态 D1 和 D0 发出幻数据包唤醒。

<a href="" id="ndisdevicestated2"></a>**NdisDeviceStateD2**  
网络适配器，可以从设备状态 D2、 D1 和 D0 发出幻数据包唤醒。

<a href="" id="ndisdevicestated3"></a>**NdisDeviceStateD3**  
网络适配器，可以从设备的电源状态 D3、 D2，D1 和 D0 发出幻数据包唤醒。

<a href="" id="minpatternwakeup"></a>**MinPatternWakeUp**  
指定从其微型端口驱动程序的网络适配器可以发出信号收到包含通过协议驱动程序指定的模式的网络帧上的唤醒事件的最低设备电源状态。 电源状态指定为以下值之一[ **NDIS\_设备\_POWER\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_device_power_state)值：

<a href="" id="ndisdevicestateunspecified"></a>**NdisDeviceStateUnspecified**  
网络适配器不支持模式匹配之后会唤醒。

<a href="" id="ndisdevicestated0"></a>**NdisDeviceStateD0**  
网络适配器可以从设备电源状态 D0 信号模式匹配唤醒。 由于 D0 是完全通电的状态，这并不会导致唤醒，但可以用作运行时事件。

<a href="" id="ndisdevicestated1"></a>**NdisDeviceStateD1**  
网络适配器可以从设备的电源状态 D1 和 D0 信号模式匹配唤醒。

<a href="" id="ndisdevicestated2"></a>**NdisDeviceStateD2**  
网络适配器可以从设备的电源状态 D2、 D1 和 D0 信号模式匹配唤醒。

<a href="" id="ndisdevicestated3"></a>**NdisDeviceStateD3**  
网络适配器可以从设备的电源状态 D3、 D2，D1 和 D0 信号模式匹配唤醒。

<a href="" id="minlinkchangewakeup"></a>**MinLinkChangeWakeUp**  
保留。 NDIS 将忽略此成员。

**微型端口驱动程序**

微型端口驱动程序完成初始化后，协议驱动程序和 NDIS 可以查询具有可确定以下此 OID 的微型端口驱动程序：

-   微型端口驱动程序是否 PM 感知。

-   网络适配器的功能，该值指示网络唤醒的事件。

如果微型端口驱动程序将返回**NDIS\_状态\_成功**OID 的查询\_PNP\_功能，NDIS 会考虑要注意 PM 的微型端口驱动程序。 如果微型端口驱动程序将返回**NDIS\_状态\_不\_支持**，NDIS 会考虑将并不知道 PM 的旧的微型端口驱动程序微型端口驱动程序。

调用时[ **NdisMSetAttributesEx**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553623(v=vs.85))，可以设置的微型端口驱动程序不支持唤醒功能，但是，可以保存并还原其网络适配器状态跨电源状态转换**NDIS\_特性\_否\_暂停\_ON\_挂起**标志。 设置此标志防止调用驱动程序的 NDIS *MiniportHalt*函数之前，系统将转换为低功耗 （睡眠） 状态。 但是，如果微型端口驱动程序将返回**NDIS\_状态\_不\_支持**以响应查询 OID\_PNP\_功能，将忽略 NDIS **NDIS\_特性\_无\_暂停\_ON\_挂起**标记并停止网络适配器，如果系统进入低功耗状态。

微型端口驱动程序的网络适配器可以支持唤醒事件，不包括任何唤醒事件的任意组合。 微型端口驱动程序仍可以支持电源管理，即使其网络适配器不能向唤醒事件发送信号。 在此情况下，唯一的电源管理的微型端口驱动程序支持除了 OID 的 Oid\_PNP\_功能[OID\_PNP\_查询\_POWER](oid-pnp-query-power.md)和[OID\_PNP\_设置\_POWER](oid-pnp-set-power.md)。

如果微型端口驱动程序的网络适配器不支持特定唤醒事件，微型端口驱动程序应指示[ **NDIS\_设备\_POWER\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_device_power_state)的值**NdisDeviceStateUnspecified**中的唤醒事件**NDIS\_PM\_唤醒\_向上\_功能**结构。

OID\_PNP\_功能仅指示微型端口驱动程序的唤醒功能 s 网络适配器; 它不会启用此类功能。 [OID\_PNP\_启用\_唤醒\_向上](oid-pnp-enable-wake-up.md)用于启用网络适配器的唤醒功能。

**中间驱动程序**

如果是识别 PM 的基础网络适配器，则中间驱动程序应返回**NDIS\_状态\_成功**OID 的查询\_PNP\_功能。 在中**NDIS\_PM\_唤醒\_向上\_功能**结构返回的此 OID，中间驱动程序应指定设备电源状态的**NdisDeviceStateUnspecified**为每个唤醒功能 ( **MinMagicPacketWakeUp**或**MinPatternWakeUp**)。 此类响应指示中间驱动程序是 PM 感知，但不会管理物理设备。

如果不是可识别 PM 的基础网络适配器，则中间驱动程序应返回**NDIS\_状态\_不\_支持**OID 的查询\_PNP\_功能。

**请注意**  NDIS 6.20 和更高版本的微型端口驱动程序报告电源管理功能的方式的信息，请参阅[报告电源管理功能](https://docs.microsoft.com/windows-hardware/drivers/network/reporting-power-management-capabilities)。

 

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
<td><p>NDIS 6.0 和 NDIS 6.1 支持。 NDIS 6.20 和更高版本，使用<a href="oid-pm-current-capabilities.md" data-raw-source="[OID_PM_CURRENT_CAPABILITIES](oid-pm-current-capabilities.md)">OID_PM_CURRENT_CAPABILITIES</a>相反。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_DEVICE\_POWER\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_device_power_state)

[**NdisMSetAttributesEx**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553623(v=vs.85))

[OID\_PM\_当前\_功能](oid-pm-current-capabilities.md)

[OID\_PNP\_ENABLE\_WAKE\_UP](oid-pnp-enable-wake-up.md)

[OID\_PNP\_查询\_电源](oid-pnp-query-power.md)

[OID\_PNP\_SET\_POWER](oid-pnp-set-power.md)

[报告电源管理功能](https://docs.microsoft.com/windows-hardware/drivers/network/reporting-power-management-capabilities)

 

 




