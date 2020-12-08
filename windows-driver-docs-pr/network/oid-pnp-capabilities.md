---
title: OID_PNP_CAPABILITIES
description: OID_PNP_CAPABILITIES OID 请求微型端口驱动程序返回其网络适配器的唤醒功能，或请求中间驱动程序返回中间驱动程序的唤醒功能。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_CAPABILITIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8d65bf410bda4314db2f2f2e01f6a673461ae942
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827545"
---
# <a name="oid_pnp_capabilities"></a>OID \_ PNP \_ 功能


OID \_ PNP \_ 功能 oid 请求微型端口驱动程序返回其网络适配器的唤醒功能，或请求中间驱动程序返回中间驱动程序的唤醒功能。 唤醒功能的格式为 **NDIS \_ PNP \_ 功能** 结构，定义如下：

```C++
    typedef struct _NDIS_PNP_CAPABILITIES {
         ULONG Flags;
         NDIS_PM_WAKE_UP_CAPABILITIES WakeUpCapabilities;
    } NDIS_PNP_CAPABILITIES, *PNDIS_PNP_CAPABILITIES;  
```




此结构的成员包含以下信息：

<a href="" id="flags"></a>**随意**  
**\_启用 NDIS 设备 \_ 唤醒 \_ \_**

如果基础微型端口驱动程序支持一个或多个唤醒功能，NDIS 将设置此标志。 协议驱动程序可以测试此标志，以确定基础微型端口驱动程序是否具有唤醒功能。 微型端口驱动程序不应访问此标志。

<a href="" id="wakeupcapabilities"></a>**WakeUpCapabilities**  
用于指定微型端口驱动程序网络适配器的唤醒功能的 **NDIS \_ PM \_ 唤醒 \_ \_ 功能** 结构。 **NDIS \_ PM \_ 唤醒 \_ \_ 功能** 结构定义如下：

```C++
typedef struct _NDIS_PM_WAKE_UP_CAPABILITIES {
         NDIS_DEVICE_POWER_STATE MinMagicPacketWakeUp;
         NDIS_DEVICE_POWER_STATE MinPatternWakeUp;
         NDIS_DEVICE_POWER_STATE MinLinkChangeWakeUp;
       } NDIS_PM_WAKE_UP_CAPABILITIES, *PNDIS_PM_WAKE_UP_CAPABILITIES;
```

此结构的成员包含以下信息：

<a href="" id="minmagicpacketwakeup"></a>**MinMagicPacketWakeUp**  
指定最小的设备电源状态，微型端口驱动程序的网络适配器可以使用该电源状态在收到幻数据包时发出唤醒信号。  (*幻数据包* 是包含接收网络适配器的以太网地址的16个连续副本的数据包。 ) 设备电源状态指定为下列 [**NDIS \_ 设备 \_ 电源 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state) 值之一：

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
指定最小的设备电源状态，微型端口驱动程序的网络适配器可以在收到包含协议驱动程序指定模式的网络帧时发出唤醒事件信号。 电源状态指定为下列 [**NDIS \_ 设备 \_ 电源 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state) 值之一：

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

如果微型端口驱动程序将 **NDIS \_ 状态 \_ 成功** 返回到 OID \_ PNP 功能的查询 \_ ，NDIS 会将微型端口驱动程序视为可识别 PM。 如果微型端口驱动程序 **返回 \_ \_ 不 \_ 受支持的 NDIS 状态**，ndis 会将微型端口驱动程序视为不能识别 PM 的旧版微型端口驱动程序。

当调用 [**NdisMSetAttributesEx**](/previous-versions/windows/hardware/network/ff553623(v=vs.85))时，不支持唤醒功能但可以在电源状态转换中保存和还原其网络适配器状态的微型端口驱动程序可以设置 **NDIS \_ 属性 " \_ \_ \_ \_ 挂起" 标志上的 "不暂停** "。 设置此标志可防止 NDIS 在系统转换到低功耗 (睡眠) 状态之前调用驱动程序的 *MiniportHalt* 函数。 但是，如果微型端口驱动程序返回了 **\_ \_ 不 \_ 支持的 ndis 状态** 以响应查询 OID \_ PNP \_ 功能，ndis 将忽略 "挂起" 标志 **上的 ndis 属性 " \_ \_ 不 \_ 暂停 \_ \_** "，并在系统进入低功耗状态时停止网络适配器。

微型端口驱动程序的网络适配器可以支持唤醒事件的任意组合，包括无唤醒事件。 即使其网络适配器无法对唤醒事件发出信号，微型端口驱动程序仍可以支持电源管理。 在这种情况下，除了 OID pnp 功能外，微型端口驱动程序支持的电源管理 Oid 只有 \_ \_ [oid \_ Pnp \_ 查询 \_ 能力](oid-pnp-query-power.md) 和 [oid \_ pnp \_ 集 \_ ](oid-pnp-set-power.md)功能。

如果微型端口驱动程序的网络适配器不支持特定的唤醒事件，微型端口驱动程序应在 **ndis \_ PM \_ 唤醒 \_ \_ 功能** 结构中为唤醒事件指示 [**ndis \_ 设备 \_ 电源 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)值 **NdisDeviceStateUnspecified** 。

OID \_ PNP \_ 功能仅指示微型端口驱动程序的网络适配器的唤醒功能; 它不启用此类功能。 [OID \_PNP \_ 启用 \_ 唤醒 \_ ](oid-pnp-enable-wake-up.md) 用于启用网络适配器的唤醒功能。

**用于中间驱动程序**

如果基础网络适配器支持 PM，则中间驱动程序应将 **NDIS \_ 状态 \_ 成功** 返回到 OID PNP 功能的查询 \_ \_ 。 在此 OID 返回的 **NDIS \_ PM \_ 唤醒 \_ \_ 功能** 结构中，中间驱动程序应为每个唤醒功能 ( **MinMagicPacketWakeUp** 或 **MinPatternWakeUp**) 指定设备电源状态 " **NdisDeviceStateUnspecified** "。 此类响应表示中间驱动程序可感知，但不管理物理设备。

如果基础网络适配器不是 PM 可识别的，则中间驱动程序应将 **\_ \_ 不 \_ 支持的 NDIS 状态** 返回给 OID \_ PNP 功能的查询 \_ 。

**注意**  有关 NDIS 6.20 和更高版本的微型端口驱动程序如何报告电源管理功能的信息，请参阅 [报告电源管理功能](./reporting-power-management-capabilities.md)。

 

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
<td><p>在 NDIS 6.0 和 NDIS 6.1 中受支持。 对于 NDIS 6.20 和更高版本，请改用 <a href="oid-pm-current-capabilities.md" data-raw-source="[OID_PM_CURRENT_CAPABILITIES](oid-pm-current-capabilities.md)">OID_PM_CURRENT_CAPABILITIES</a> 。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 设备 \_ 电源 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_device_power_state)

[**NdisMSetAttributesEx**](/previous-versions/windows/hardware/network/ff553623(v=vs.85))

[OID \_ PM \_ 当前 \_ 功能](oid-pm-current-capabilities.md)

[OID \_ PNP \_ 启用 \_ 唤醒 \_](oid-pnp-enable-wake-up.md)

[OID \_ PNP \_ 查询 \_ 能力](oid-pnp-query-power.md)

[OID \_ PNP \_ 设置 \_ 电源](oid-pnp-set-power.md)

[报告电源管理功能](./reporting-power-management-capabilities.md)

 

