---
title: 配置 NetAdapterCx 电源管理
description: 配置电源管理
ms.assetid: 0EAE26D0-C191-422F-8A73-28A71C272D4D
keywords:
- NetAdapterCx 配置电源管理，NetCx 配置电源管理
ms.date: 11/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: 22b653bff2bc2fe0fd079023374daf6445286c55
ms.sourcegitcommit: 661e1f3bd629d316394e4468eccda6489273209f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2020
ms.locfileid: "84753995"
---
# <a name="configuring-netadaptercx-power-management"></a>配置 NetAdapterCx 电源管理

所有 NetAdapterCx 客户端驱动程序都是 Windows 驱动程序框架（WDF）驱动程序，其电源管理功能与所有 WDF 驱动程序类似。 NetAdapterCx 驱动程序需要其他特定于网络的电源配置，如本文中所述。

典型的网络设备支持3个常见电源管理功能：

- 当操作系统指示网络设备时，网络设备可以进入低功耗（Dx）状态。
  - 客户端驱动程序将注册可选的 WDF 事件回调以接收电源转换的通知，如在[功能驱动程序中支持 PnP 和电源管理](../wdf/supporting-pnp-and-power-management-in-function-drivers.md)中所述。

  - 如果网络设备在系统保持正常运行（S0）状态时可以进入 Dx 状态，则客户端驱动程序应支持空闲关机。 请参阅[支持空闲电源关闭](../wdf/supporting-idle-power-down.md)。

- 当网络设备处于 Dx 状态时，如果已预配置的唤醒条件已发生，则它可以触发唤醒信号。
  - 若要详细了解 WDF 设备如何从系统范围低功耗状态唤醒系统，请参阅[支持系统唤醒](../wdf/supporting-system-wake-up.md)。

  - NetAdapterCx 为客户端驱动程序提供 Api，以声明其硬件对其具有唤醒支持的网络事件。 请参阅下面的 "[设置网络适配器的电源功能](#setting-power-capabilities-of-the-network-adapter)" 部分。

- 当网络设备处于 Dx 状态时，它仍然可以响应一些常用的网络请求，以维护主机系统在网络上的存在，而不会唤醒主机系统。 请参阅下面的 "[设置网络适配器的电源功能](#setting-power-capabilities-of-the-network-adapter)" 部分。

## <a name="setting-power-capabilities-of-the-network-adapter"></a>设置网络适配器的电源功能

配置 WDF 电源管理功能后，下一步是设置网络适配器的电源功能。 电源功能分为两类：[低功率协议卸载功能](#low-power-protocol-offload-capabilities)和[唤醒功能](#wake-up-capabilities)。

### <a name="low-power-protocol-offload-capabilities"></a>低功率协议卸载功能

有关 Windows 网络堆栈如何利用此功能的背景信息，请参阅[NDIS 电源管理的协议卸载](../network/protocol-offloads-for-ndis-power-management.md)。

客户端驱动程序通过调用适用于其硬件的以下方法来设置低功率协议卸载功能：

- [**NetAdapterPowerOffloadSetArpCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterpoweroffloadsetarpcapabilities)
- [**NetAdapterPowerOffloadSetNSCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterpoweroffloadsetnscapabilities)

### <a name="wake-up-capabilities"></a>唤醒功能

客户端驱动程序调用以下任一方法，设置在设备处于低功率状态（Dx）时其硬件支持的唤醒功能：

- [**NetAdapterWakeSetBitmapCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetbitmapcapabilities)
- [**NetAdapterWakeSetMagicPacketCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetmagicpacketcapabilities)
- [**NetAdapterWakeSetMediaChangeCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetmediachangecapabilities)
- [**NetAdapterWakeSetPacketFilterCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetpacketfiltercapabilities)

### <a name="power-consumption-and-resume-latency"></a>功率消耗和恢复延迟

当网络设备处于 Dx 时，它仍然会消耗电来执行卸载和用于唤醒的 arm。 设备启动来自 Dx 的唤醒后，会有一段延迟，直到设备再次传输数据包。 内部电源状态越深，设备进入的能力越少，在 Dx 中就会消耗更长时间，但恢复延迟时间越长。

下表描述了有关每个唤醒功能的能耗与恢复延迟之间的权衡的一般准则。

> [!IMPORTANT]
> 某些信息与 prereleased 产品相关，这些信息可能会在正式发布之前经过重大修改。 对于提供的信息，Microsoft 不做任何明示或默示的保证。 有关特定设备类型的详细信息，请参阅媒体特定的文档和[Windows 硬件兼容性计划（WHCP）](https://docs.microsoft.com/windows-hardware/design/compatibility/) 。
  
| 唤醒功能 | 唤醒事件 | 功率消耗 | 恢复延迟
|-|-|-|-|
| PacketFilter | ReceivePacketFilter 配置的任何数据包匹配 | 应低于 D0 中的时间，并且设备需要保持在适当的状态，以便恢复延迟非常小  | <= 10 毫秒
| Bitmap |任何数据包匹配已配置的位图模式 | 应低于提供 PacketFilter 的时间，因为它在恢复延迟中具有更多纬度 | <= 300 ms
| MagicPacket | 幻数据包 | 类似于位图 | <= 300 ms
| MediaChange | 媒体已连接或已断开连接 | 类似于位图 | <= 300 ms

下面的示例说明了客户端驱动程序如何初始化其电源功能。 它在启动网络适配器时，但在调用[**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)之前执行此过程。 在此示例中，客户端驱动程序将设置其位图、媒体更改和数据包筛选器唤醒功能。

```cpp
//
// Set bitmap wake capabilities
//
NET_ADAPTER_WAKE_BITMAP_CAPABILITIES bitmapCapabilities;
NET_ADAPTER_WAKE_BITMAP_CAPABILITIES_INIT(&bitmapCapabilities);

bitmapCapabilities.BitmapPattern = TRUE;
bitmapCapabilities.MaximumPatternCount = deviceContext->PowerFiltersSupported;
bitmapCapabilities.MaximumPatternSize = 256;

NetAdapterWakeSetBitmapCapabilities(Adapter, &bitmapCapabilities);

//
// Set media change wake capabilities
//
NET_ADAPTER_WAKE_MEDIA_CHANGE_CAPABILITIES mediaChangeCapabilities;
NET_ADAPTER_WAKE_MEDIA_CHANGE_CAPABILITIES_INIT(&mediaChangeCapabilities);

mediaChangeCapabilities.MediaConnect = TRUE;
mediaChangeCapabilities.MediaDisconnect = TRUE;

NetAdapterWakeSetMediaChangeCapabilities(Adapter, &mediaChangeCapabilities);

//
// Set packet filter wake capabilities
//
if(deviceContext->SelectiveSuspendSupported)
{
    NET_ADAPTER_WAKE_PACKET_FILTER_CAPABILITIES packetFilterCapabilities;
    NET_ADAPTER_WAKE_PACKET_FILTER_CAPABILITIES_INIT(&packetFilterCapabilities);

    packetFilterCapabilities.PacketFilterMatch = TRUE;

    NetAdapterWakeSetPacketFilterCapabilities(Adapter, &packetFilterCapabilities);
}
```

客户端可以选择注册[*EVT_NET_DEVICE_PREVIEW_POWER_OFFLOAD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdevice/nc-netdevice-evt_net_device_preview_power_offload)和[*EVT_NET_DEVICE_PREVIEW_WAKE_SOURCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdevice/nc-netdevice-evt_net_device_preview_wake_source)回调函数，以接受或拒绝传入的协议卸载和唤醒模式。

## <a name="programming-protocol-power-offload-and-wake-patterns"></a>编程协议电源卸载和唤醒模式

在设备的[关机顺序](../wdf/power-down-and-removal-sequence-for-a-function-or-filter-driver.md)中，驱动程序将循环访问已启用的唤醒模式和协议电源卸载，并将其程序写入硬件。 该驱动程序在其[*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)和[*EvtDeviceArmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)回调函数中执行此功能。

下面的示例演示客户端驱动程序如何循环访问唤醒模式列表以检查幻数据包条目的唤醒，然后循环访问电源卸载列表来处理 IPv4 ARP 协议卸载：

```cpp
NTSTATUS
EvtDeviceArmWakeFromSx(
    WDFDEVICE     Device
)
{
    NETADAPTER adapter = GetDeviceContext(Device)->Adapter;

    //
    // Process wake source list
    //
    NET_WAKE_SOURCE_LIST wakeSourceList;
    NET_WAKE_SOURCE_LIST_INIT(&wakeSourceList);

    NetDeviceGetWakeSourceList(Device, &wakeSourceList);

    for(UINT32 i = 0; i < NetWakeSourceListGetCount(&wakeSourceList; i++); i++)
    {
        NETWAKESOURCE wakeSource = NetWakeSourceListGetElement(&wakeSourceList, i);
        NET_WAKE_SOURCE_TYPE const wakeSourceType = NetWakeSourceGetType(wakeSource);

        if(wakeSourceType == NetWakeSourceTypeMagicPacket)
        {
            // Enable magic packet wake for the adapter
            ..
            //
        }
    }

    //
    // Process power offload list
    //
    NET_POWER_OFFLOAD_LIST powerOffloadList;
    NET_POWER_OFFLOAD_LIST_INIT(&powerOffloadList);

    NetDeviceGetPowerOffloadList(Device, &powerOffloadList);

    for(UINT32 i = 0; i < NetPowerOffloadListGetCount(&powerOffloadList); i++)
    {
        NETPOWEROFFLOAD powerOffload = NetPowerOffloadGetElement(&powerOffloadList, i);
        NET_POWER_OFFLOAD_TYPE const powerOffloadType = NetPowerOffloadGetType(powerOffload);

        if(powerOffloadType == NetPowerOffloadTypeArp)
        {
            // Enable ARP protocol offload for the adapter
            ..
            //
        }
    }

    return STATUS_SUCCESS;
}
```

[回到高性能](../wdf/power-up-sequence-for-a-function-or-filter-driver.md)，驱动程序通常会在相应的[*EvtDeviceDisarmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_sx)和[*EvtDeviceDisarmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_disarm_wake_from_s0)回调中禁用先前编程的协议电源卸载和唤醒模式。

## <a name="power-management-scenarios-for-modern-standby-system"></a>新式备用系统的电源管理方案

> [!IMPORTANT]
> 对于新式备用平台，网络设备驱动程序必须：
>
> - 调用[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)注册电源回调。
> - 当系统处于工作状态（S0）时，调用[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)以支持设备置于空闲状态。
> - 调用[**WdfDeviceInitSetPowerPolicyEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpowerpolicyeventcallbacks)以注册唤醒回调。
> - 支持适用于设备类型的[低功率协议卸载功能](#low-power-protocol-offload-capabilities)。
> - 支持适合于设备类型的[唤醒功能](#wake-up-capabilities)。
>
> 有关设备类型的完整新式备用要求，请参阅媒体特定的文档和 WHCP。

操作系统负责网络设备的电源策略决策。 例如，OS 控制设备何时必须使用 Dx 以及设备应该唤醒的网络事件类型。 设备驱动程序的责任是在操作系统请求时可靠地执行电源转换顺序，然后针对操作系统设置的唤醒条件对其硬件进行正确的编程。

操作系统基于多种因素（包括系统范围内的电源策略和用户选择）制定电源策略决策。 下面是新式备用系统上用于网络设备的一些常见电源策略：

> [!IMPORTANT]
> 这些电源策略可能会随操作系统更新而更改，下面提供了以下信息作为示例。 应避免对操作系统的特定端到端行为的依赖关系。

- 当 PC 屏幕开启并且网络设备被置于空闲状态时，操作系统会要求设备转向 Dx，并将其与 PacketFilter 和 MediaChange 唤醒连接在一起。

- 当电脑进入新式备用状态并且网络设备被置于空闲状态时，操作系统会要求 NIC 进入 Dx，并将其与 MediaChange 和幻数据包唤醒连接在一起。

- 当 PC 进入休眠状态时，操作系统会要求 NIC 进入 Dx，并对其进行魔术包唤醒。
