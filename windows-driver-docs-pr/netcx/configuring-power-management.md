---
title: 配置电源管理
description: 配置电源管理
ms.assetid: 0EAE26D0-C191-422F-8A73-28A71C272D4D
keywords:
- 配置电源管理，配置电源管理的 NetCx NetAdapterCx
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: de18f627adbca92c95da655f01db06c5db76c29c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372706"
---
# <a name="configuring-power-management"></a>配置电源管理

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

本主题介绍如何在 NetAdapterCx 客户端驱动程序中配置电源管理功能。

由于客户端驱动程序是 WDF 驱动程序，很多实现是与任何其他 WDF 驱动程序，相同另外还有几个选项特定于 NetAdapterCx 您可以在中添加。

有关常见 WDF 行为的详细信息，请参阅以下页面：

*  客户端注册可选 WDF 事件的回调以接收通知的电源转换，如中所述[支持即插即用和功能的驱动程序中的电源管理](../wdf/supporting-pnp-and-power-management-in-function-drivers.md)。
*  WDF 客户端中注册 PnP 和电源的回调函数的信息，请参阅[功能驱动程序中创建设备对象](../wdf/creating-device-objects-in-a-function-driver.md)。
*  你的设备可以从系统范围内低功耗状态系统的唤醒的详细信息，请参阅[支持系统唤醒](../wdf/supporting-system-wake-up.md)。

## <a name="setting-power-capabilities-of-the-network-adapter"></a>设置网络适配器的电源功能

配置标准 WDF 电源管理功能之后, 的下一步是调用[ **NetAdapterSetPowerCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptersetpowercapabilities)若要设置的网络适配器的电源功能。

下面的示例演示如何初始化和配置 NETPOWERSETTINGS 对象，它在客户端通常会从网络适配器，但在通过调用[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart):

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

将客户端可以注册[ *EVT_NET_ADAPTER_PREVIEW_PROTOCOL_OFFLOAD* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_preview_protocol_offload)并[ *EVT_NET_ADAPTER_PREVIEW_WAKE_PATTERN* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_preview_wake_pattern)回调函数以接受或拒绝传入的协议将卸载并唤醒模式。 如果你想要注册这些可选回调之一，则必须启动网络适配器，然后才能调用时执行这样[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart)。

## <a name="programming-protocol-offload-and-wake-patterns"></a>编程协议卸载并唤醒模式

在其[ *EvtDeviceArmWakeFromS0* ](https://msdn.microsoft.com/library/windows/hardware/ff540843)并[ *EvtDeviceArmWakeFromSx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_sx)回调函数，该驱动程序将循环访问已启用唤醒模式和协议将卸载和程序到硬件。

首先要检索的句柄的 NETPOWERSETTINGS 对象通过调用与适配器关联的[ **NetAdapterGetPowerSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptergetpowersettings)从[ *EvtDeviceArmWakeFromS0* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_arm_wake_from_s0)或相关的回调函数。  下面的示例演示如何循环访问唤醒模式：

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

客户端使用相同的机制进行循环访问，协议将卸载，使用[ **NetPowerSettingsGetProtocolOffloadCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpowersettings/nf-netpowersettings-netpowersettingsgetprotocoloffloadcount)， [ **NetPowerSettingsGetProtocolOffload** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpowersettings/nf-netpowersettings-netpowersettingsgetprotocoloffload)并[ **NetPowerSettingsIsProtocolOffloadEnabled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpowersettings/nf-netpowersettings-netpowersettingsisprotocoloffloadenabled)。
