---
title: OID_PNP_CAPABILITIES
description: OID_PNP_CAPABILITIES OID 请求微型端口驱动程序返回其网络适配器的唤醒功能，或请求中间驱动程序返回中间驱动程序的唤醒功能。
ms.assetid: f2e3a867-d7d2-4d09-b84b-e8f8610b8535
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 00e74bb683c85ca09deecb9190bfd741c459b663
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844041"
---
# <a name="oid_pnp_capabilities"></a>OID\_PNP\_功能


OID\_PNP\_功能 OID 请求微型端口驱动程序返回其网络适配器的唤醒功能，或请求中间驱动程序返回中间驱动程序的唤醒功能。 唤醒功能的格式为**NDIS\_PNP\_功能**结构，定义如下：

```C++
    typedef struct _NDIS_PNP_CAPABILITIES {
         ULONG Flags;
         NDIS_PM_WAKE_UP_CAPABILITIES WakeUpCapabilities;
    } NDIS_PNP_CAPABILITIES, *PNDIS_PNP_CAPABILITIES;  
```




此结构的成员包含以下信息：

<a href="" id="flags"></a>**随意**  
**NDIS\_设备\_唤醒\_\_启用**

如果基础微型端口驱动程序支持一个或多个唤醒功能，NDIS 将设置此标志。 协议驱动程序可以测试此标志，以确定基础微型端口驱动程序是否具有唤醒功能。 微型端口驱动程序不应访问此标志。

<a href="" id="wakeupcapabilities"></a>**WakeUpCapabilities**  
**NDIS\_PM\_唤醒\_** 指定微型端口驱动程序网络适配器的唤醒功能的\_功能结构。 **NDIS\_PM\_唤醒\_\_** 按如下方式定义功能结构：

```C++
typedef struct _NDIS_PM_WAKE_UP_CAPABILITIES {
         NDIS_DEVICE_POWER_STATE MinMagicPacketWakeUp;
         NDIS_DEVICE_POWER_STATE MinPatternWakeUp;
         NDIS_DEVICE_POWER_STATE MinLinkChangeWakeUp;
       } NDIS_PM_WAKE_UP_CAPABILITIES, *PNDIS_PM_WAKE_UP_CAPABILITIES;
```

此结构的成员包含以下信息：

<a href="" id="minmagicpacketwakeup"></a>**MinMagicPacketWakeUp**  
指定最小的设备电源状态，微型端口驱动程序的网络适配器可以使用该电源状态在收到幻数据包时发出唤醒信号。 （*幻数据包*是包含接收网络适配器的以太网地址的16个连续副本的数据包。）设备电源状态指定为下列[**NDIS\_设备之一\_电源\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)值：

<a href="" id="ndisdevicestateunspecified"></a>**NdisDeviceStateUnspecified**  
网络适配器不支持幻数据包唤醒。

<a href="" id="ndisdevicestated0"></a>**NdisDeviceStateD0**  
网络适配器可以从设备电源状态 D0 发出幻数据包唤醒信号。 因为 D0 是完全支持的状态，所以这不会导致唤醒，但可以用作运行时事件。

<a href="" id="ndisdevicestated1"></a>**NdisDeviceStateD1**  
网络适配器可以从设备电源状态 D1 和 D0 发出幻数据包唤醒信号。

<a href="" id="ndisdevicestated2"></a>**NdisDeviceStateD2**  
网络适配器可以从设备状态 D2、D1 和 D0 发出幻数据包唤醒信号。

<a href="" id="ndisdevicestated3"></a>**NdisDeviceStateD3**  
网络适配器可以从设备电源状态 D3、D2、D1 和 D0 发出幻数据包唤醒信号。

<a href="" id="minpatternwakeup"></a>**MinPatternWakeUp**  
指定最小的设备电源状态，微型端口驱动程序的网络适配器可以在收到包含协议驱动程序指定模式的网络帧时发出唤醒事件信号。 电源状态指定为下列[**NDIS\_设备之一\_电源\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)值：

<a href="" id="ndisdevicestateunspecified"></a>**NdisDeviceStateUnspecified**  
网络适配器不支持模式匹配唤醒。

<a href="" id="ndisdevicestated0"></a>**NdisDeviceStateD0**  
网络适配器可以从设备电源状态 D0 发出模式匹配唤醒信号。 因为 D0 是完全支持的状态，所以这不会导致唤醒，但可以用作运行时事件。

<a href="" id="ndisdevicestated1"></a>**NdisDeviceStateD1**  
网络适配器可以从设备电源状态 D1 和 D0 通知模式匹配唤醒。

<a href="" id="ndisdevicestated2"></a>**NdisDeviceStateD2**  
网络适配器可以从设备电源状态 D2、D1 和 D0 发出模式匹配唤醒信号。

<a href="" id="ndisdevicestated3"></a>**NdisDeviceStateD3**  
网络适配器可以从设备电源状态 D3、D2、D1 和 D0 发出模式匹配唤醒信号。

<a href="" id="minlinkchangewakeup"></a>**MinLinkChangeWakeUp**  
保留。 NDIS 忽略此成员。

**对于微型端口驱动程序**

小型端口驱动程序完成初始化后，协议驱动程序和 NDIS 都可以通过此 OID 查询微型端口驱动程序来确定以下各项：

-   微型端口驱动程序是否可识别 PM。

-   网络适配器的功能，指示网络唤醒事件。

如果微型端口驱动程序将**NDIS\_状态\_SUCCESS**返回到\_PNP\_功能的 OID 查询成功，ndis 会将微型端口驱动程序视为可识别 PM。 如果微型端口驱动程序返回**NDIS\_状态\_不\_支持**，ndis 会将微型端口驱动程序视为不能识别 PM 的旧版微型端口驱动程序。

当调用[**NdisMSetAttributesEx**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553623(v=vs.85))时，不支持唤醒功能但可以在电源状态转换中保存和还原其网络适配器状态的微型端口驱动程序可以将**NDIS\_属性设置\_no\_暂停\_暂停标志\_** 。 设置此标志可防止 NDIS 在系统转换到低功耗（睡眠）状态之前调用驱动程序的*MiniportHalt*函数。 但是，如果微型端口驱动程序返回**NDIS\_状态\_不\_** 为响应查询 OID 而支持\_PNP\_功能，ndis 将忽略**ndis\_属性，\_** 如果系统进入低功耗状态，\_挂起标志并停止网络适配器。

微型端口驱动程序的网络适配器可以支持唤醒事件的任意组合，包括无唤醒事件。 即使其网络适配器无法对唤醒事件发出信号，微型端口驱动程序仍可以支持电源管理。 在这种情况下，除了\_PNP\_功能的 OID 以外，微型端口驱动程序支持的唯一电源管理 Oid 是[oid\_pnp\_查询\_电源](oid-pnp-query-power.md)和[OID\_pnp\_\_电源](oid-pnp-set-power.md)。

如果微型端口驱动程序的网络适配器不支持特定的唤醒事件，微型端口驱动程序应指示[**NDIS\_设备\_POWER\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)值为**NdisDeviceStateUnspecified**的唤醒事件**NDIS\_PM\_唤醒\_\_功能**结构。

OID\_PNP\_功能仅指示微型端口驱动程序的网络适配器的唤醒功能;它不启用此类功能。 [OID\_PNP\_启用\_唤醒\_](oid-pnp-enable-wake-up.md)用于启用网络适配器的唤醒功能。

**用于中间驱动程序**

如果基础网络适配器是 PM 可识别的，则中间驱动程序应将**NDIS\_状态**返回到\_PNP\_功能的 OID 查询成功\_。 在**NDIS\_PM\_唤醒\_** 此 OID 返回的\_功能结构，中间驱动程序应为每个唤醒功能指定**NdisDeviceStateUnspecified**的设备电源状态（ **MinMagicPacketWakeUp**或**MinPatternWakeUp**）。 此类响应表示中间驱动程序可感知，但不管理物理设备。

如果基础网络适配器不能识别 PM，中间驱动程序应将**NDIS\_状态返回\_不\_支持**\_PNP\_功能的 OID 查询。

**请注意**  有关 NDIS 6.20 和更高的微型端口驱动程序如何报告电源管理功能的信息，请参阅[报告电源管理功能](https://docs.microsoft.com/windows-hardware/drivers/network/reporting-power-management-capabilities)。

 

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
<td><p>在 NDIS 6.0 和 NDIS 6.1 中受支持。 对于 NDIS 6.20 和更高版本，请改用<a href="oid-pm-current-capabilities.md" data-raw-source="[OID_PM_CURRENT_CAPABILITIES](oid-pm-current-capabilities.md)">OID_PM_CURRENT_CAPABILITIES</a> 。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_设备\_电源\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)

[**NdisMSetAttributesEx**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553623(v=vs.85))

[\_PM\_当前\_功能的 OID](oid-pm-current-capabilities.md)

[OID\_PNP\_启用\_唤醒\_](oid-pnp-enable-wake-up.md)

[OID\_PNP\_QUERY\_POWER](oid-pnp-query-power.md)

[OID\_PNP\_集\_电源](oid-pnp-set-power.md)

[报告电源管理功能](https://docs.microsoft.com/windows-hardware/drivers/network/reporting-power-management-capabilities)

 

 




