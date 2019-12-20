---
title: 配置电源管理
description: 配置电源管理
ms.assetid: 0EAE26D0-C191-422F-8A73-28A71C272D4D
keywords:
- NetAdapterCx 配置电源管理，NetCx 配置电源管理
ms.date: 11/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: a3466dfa505558afebc4af2c207470df5d9e695b
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210783"
---
# <a name="configuring-power-management"></a>配置电源管理

本主题介绍如何在 NetAdapterCx 客户端驱动程序中配置电源管理功能。

因为客户端驱动程序是一个 WDF 驱动程序，所以很多实现与任何其他 WDF 驱动程序相同，然后有一些特定于 NetAdapterCx 的选项，您可以在其中添加这些选项。

有关常见 WDF 行为的详细信息，请参阅以下页面：

*  客户端注册可选的 WDF 事件回调以接收电源转换的通知，如在[功能驱动程序中支持 PnP 和电源管理](../wdf/supporting-pnp-and-power-management-in-function-drivers.md)中所述。
*  有关在 WDF 客户端中注册 PnP 和 power 回调函数的信息，请参阅[在函数驱动程序中创建设备对象](../wdf/creating-device-objects-in-a-function-driver.md)。
*  有关设备如何从系统范围低功耗状态唤醒系统的详细信息，请参阅[支持系统唤醒](../wdf/supporting-system-wake-up.md)。

## <a name="setting-power-capabilities-of-the-network-adapter"></a>设置网络适配器的电源功能

配置标准 WDF 电源管理功能后，下一步是设置网络适配器的电源功能。 电源功能分为两类：低功率协议卸载功能和唤醒源功能。 客户端驱动程序通过调用适用于其硬件的以下方法来设置其协议卸载功能：

- [**NetAdapterPowerOffloadSetArpCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterpoweroffloadsetarpcapabilities)
- [**NetAdapterPowerOffloadSetNSCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterpoweroffloadsetnscapabilities)

接下来，客户端驱动程序调用以下任一方法来设置其硬件支持的 LAN 唤醒（WoL）功能：

- [**NetAdapterWakeSetBitmapCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetbitmapcapabilities)
- [**NetAdapterWakeSetMagicPacketCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetmagicpacketcapabilities)
- [**NetAdapterWakeSetMediaChangeCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetmediachangecapabilities)
- [**NetAdapterWakeSetPacketFilterCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterwakesetpacketfiltercapabilities)

下面的示例演示客户端驱动程序如何初始化其电源功能，这是在启动网络适配器时，但在调用[**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)之前。 在此示例中，客户端驱动程序将设置其位图、媒体更改和数据包筛选器唤醒功能。

```C++
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
// Set media change wake capabilties
//
NET_ADAPTER_WAKE_MEDIA_CHANGE_CAPABILITIES mediaChangeCapabilities;
NET_ADAPTER_WAKE_MEDIA_CHANGE_CAPABILITIES_INIT(&mediaChangeCapabilities);

mediaChangeCapabilities.MediaConnect = TRUE;
mediaChangeCapabilities.MediaDisconnect = TRUE;

NetAdapterWakeSetMediaChangeCapabilities(Adapter, &mediaChangeCapabilities);

//
// Set packet filter wake capabilties 
//
if(deviceContext->SelectiveSuspendSupported)
{
    NET_ADAPTER_WAKE_PACKET_FILTER_CAPABILITIES packetFilterCapabilities;
    NET_ADAPTER_WAKE_PACKET_FILTER_CAPABILITIES_INIT(&packetFilterCapabilities);
    
    packetFilterCapabilities.PacketFilterMatch = TRUE;

    NetAdapterWakeSetPacketFilterCapabilities(Adapter, &packetFilterCapabilities);
}
```

客户端可注册[*EVT_NET_DEVICE_PREVIEW_POWER_OFFLOAD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdevice/nc-netdevice-evt_net_device_preview_power_offload)和[*EVT_NET_DEVICE_PREVIEW_WAKE_SOURCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdevice/nc-netdevice-evt_net_device_preview_wake_source)回调函数，以接受或拒绝传入的协议卸载和唤醒模式。 如果要注册其中任何一个可选的回调，在调用[**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)之前，必须在启动网络适配器时执行此操作。

## <a name="programming-protocol-offload-and-wake-patterns"></a>编程协议卸载和唤醒模式

在其[*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)和[*EvtDeviceArmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)回调函数中，驱动程序将循环访问已启用的唤醒模式和协议卸载，并将其程序写入硬件。

下面的示例演示客户端驱动程序如何循环访问唤醒模式列表以检查幻数据包条目的唤醒，然后循环访问电源卸载列表来处理 IPv4 ARP 协议卸载：

```C++
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