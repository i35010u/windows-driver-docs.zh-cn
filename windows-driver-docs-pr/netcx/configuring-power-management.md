---
title: 配置电源管理
description: 配置电源管理
ms.assetid: 0EAE26D0-C191-422F-8A73-28A71C272D4D
keywords:
- NetAdapterCx 配置电源管理，NetCx 配置电源管理
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17468822a966aafe4e6cdf5dd79f149e9dfe87c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835531"
---
# <a name="configuring-power-management"></a>配置电源管理

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

本主题介绍如何在 NetAdapterCx 客户端驱动程序中配置电源管理功能。

因为客户端驱动程序是一个 WDF 驱动程序，所以很多实现与任何其他 WDF 驱动程序相同，然后有一些特定于 NetAdapterCx 的选项，您可以在其中添加这些选项。

有关常见 WDF 行为的详细信息，请参阅以下页面：

*  客户端注册可选的 WDF 事件回调以接收电源转换的通知，如在[功能驱动程序中支持 PnP 和电源管理](../wdf/supporting-pnp-and-power-management-in-function-drivers.md)中所述。
*  有关在 WDF 客户端中注册 PnP 和 power 回调函数的信息，请参阅[在函数驱动程序中创建设备对象](../wdf/creating-device-objects-in-a-function-driver.md)。
*  有关设备如何从系统范围低功耗状态唤醒系统的详细信息，请参阅[支持系统唤醒](../wdf/supporting-system-wake-up.md)。

## <a name="setting-power-capabilities-of-the-network-adapter"></a>设置网络适配器的电源功能

配置标准 WDF 电源管理功能后，下一步是调用[**NetAdapterSetPowerCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptersetpowercapabilities)来设置网络适配器的电源功能。

下面的示例演示如何初始化和配置 NETPOWERSETTINGS 对象，客户端通常在启动网络适配器时执行此操作，但在调用[**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)之前：

```C++
NET_ADAPTER_POWER_CAPABILITIES     powerCaps;
NET_ADAPTER_POWER_CAPABILITIES_INIT(&powerCaps);

powerCaps.Flags = NET_ADAPTER_POWER_WAKE_PACKET_INDICATION;

powerCaps.SupportedMediaSpecificWakeUpEvents = NET_ADAPTER_WLAN_WAKE_ON_AP_ASSOCIATION_LOST;
powerCaps.SupportedProtocolOffloads = NET_ADAPTER_PROTOCOL_OFFLOAD_ARP | NET_ADAPTER_PROTOCOL_OFFLOAD_NS;
powerCaps.SupportedWakePatterns = NET_ADAPTER_WAKE_BITMAP_PATTERN;
powerCaps.SupportedWakeUpEvents = NET_ADAPTER_WAKE_ON_MEDIA_CONNECT | NET_ADAPTER_WAKE_ON_MEDIA_DISCONNECT;

powerCaps.EvtAdapterPreviewWakePattern = EvtAdapterPreviewWakePattern;
powerCaps.EvtAdapterPreviewProtocolOffload = EvtAdapterPreviewProtocolOffload;

NetAdapterSetPowerCapabilities(NetAdapter, &powerCaps);
```

客户端可以注册[*EVT_NET_ADAPTER_PREVIEW_PROTOCOL_OFFLOAD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_preview_protocol_offload)和[*EVT_NET_ADAPTER_PREVIEW_WAKE_PATTERN*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_preview_wake_pattern)回调函数，以接受或拒绝传入的协议卸载和唤醒模式。 如果要注册其中任何一个可选的回调，在调用[**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)之前，必须在启动网络适配器时执行此操作。

## <a name="programming-protocol-offload-and-wake-patterns"></a>编程协议卸载和唤醒模式

在其[*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)和[*EvtDeviceArmWakeFromSx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)回调函数中，驱动程序将循环访问已启用的唤醒模式和协议卸载，并将其程序写入硬件。

首先，通过从[*EvtDeviceArmWakeFromS0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)或相关的回调函数中调用[**NetAdapterGetPowerSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptergetpowersettings)来检索与适配器关联的 NETPOWERSETTINGS 对象的句柄。  下面的示例演示如何循环访问唤醒模式：

```C++
NTSTATUS
EvtDeviceArmWakeFromS0(
    WDFDEVICE     Device
)
{

    NETADAPTER adapter = GetDeviceContext(Device)->Adapter;
    NETPOWERSETTINGS powerSettings = NetAdapterGetPowerSettings(adapter);

    ULONG wakeUpFlags = NetPowerSettingsGetEnabledWakeUpFlags(powerSettings);
     
    if (wakeUpFlags & NET_ADAPTER_WAKE_ON_MEDIA_DISCONNNECT)
    {
        // ...
    }

    // Iterate through stored wake patterns and query which ones
    // are enabled and should be programmed to hardware

    for (ULONG i = 0; i < NetPowerSettingsGetWakePatternCount(powerSettings); i++)
    {
        PNDIS_PM_WOL_PATTERN wakePattern = NetPowerSettingsGetWakePattern(powerSettings, i);

        if (NetPowerSettingsIsWakePatternEnabled(powerSettings, wakePattern))
        {
            // ...
        }

    }

    return STATUS_SUCCESS;
}
```

客户端使用相同的机制，使用[**NetPowerSettingsGetProtocolOffloadCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpowersettings/nf-netpowersettings-netpowersettingsgetprotocoloffloadcount)、 [**NetPowerSettingsGetProtocolOffload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpowersettings/nf-netpowersettings-netpowersettingsgetprotocoloffload)和[**NetPowerSettingsIsProtocolOffloadEnabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpowersettings/nf-netpowersettings-netpowersettingsisprotocoloffloadenabled)循环访问协议卸载。
