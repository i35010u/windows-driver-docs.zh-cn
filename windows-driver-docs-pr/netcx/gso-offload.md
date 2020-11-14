---
title: 一般分段卸载
description: NetAdapterCx 中的一般分段卸载使用情况、规则和示例
ms.assetid: ''
keywords:
- WDF 网络适配器类扩展卸载，NetAdapterCx 硬件卸载，NetAdapterCx 卸载，Get-netadapter 卸载，一般分段卸载，GSO，大型分段卸载，LSO，UDP 分段卸载，USO
ms.date: 10/08/2020
ms.custom: Fe
ms.openlocfilehash: 96a3090bf18641d4d54519291136127acf8f4624
ms.sourcegitcommit: 5587af31b12cf96c1a31d42f7b40e8f72e3d739c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2020
ms.locfileid: "94572485"
---
# <a name="generic-segmentation-offload"></a>一般分段卸载

> [!WARNING]
> 本主题中的一些信息与预发布的产品相关，该产品在商业发布之前可能会进行重大修改。 Microsoft 对此处提供的信息不提供任何明示或暗示的保证。
>
> NetAdapterCx 仅在 Windows 10 版本2004中处于预览阶段。
>
> 目前，NetAdapterCx 客户端驱动程序无法通过认证。

一般分段卸载 (GSO) 共同表示 [大量发送卸载 (LSO) ](../network/offloading-the-segmentation-of-large-tcp-packets.md) 和 [UDP 发送卸载 (USO) ](../network/udp-segmentation-offload-uso-.md)。 

客户端驱动程序可以卸载大于网络媒体 (MTU) 的 TCP/UDP 数据包的分段。 驱动程序必须使用 GSO Api 指示此功能 NetAdapterCx。

## <a name="inf-keywords-for-controlling-gso"></a>用于控制 GSO 的 INF 关键字

NetAdapterCx 检查注册表关键字，并在启用活动卸载功能时遵循这些关键字。 驱动程序无需执行任何进一步操作。

[使用注册表值启用和禁用任务卸载](../network/using-registry-values-to-enable-and-disable-task-offloading.md)中指定的 LSO 关键字可用于启用/禁用使用注册表项设置的 LSO 卸载。

[UDP 分段卸载 (USO) ](../network/udp-segmentation-offload-uso-.md)中指定的 USO 关键字可用于启用/禁用使用注册表项设置的 USO 卸载。

## <a name="configuring-gso"></a>配置 GSO

客户端驱动程序首先在网络适配器初始化期间公布其硬件的 GSO 功能。 这可能会在启动网络适配器之前的 [*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调中发生。

若要配置 GSO，客户端驱动程序：

1. 分配 [**NET_ADAPTER_OFFLOAD_GSO_CAPABILITIES**](/windows-hardware/drivers/ddi/netadapteroffload/ns-netadapteroffload-_net_adapter_offload_gso_capabilities) 结构。

1. 调用 [**NET_ADAPTER_OFFLOAD_GSO_CAPABILITIES_INIT**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-net_adapter_offload_gso_capabilities_init) 以初始化结构。

1. 调用 [**NetAdapterOffloadSetGsoCapabilities**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netadapteroffloadsetgsocapabilities) 来向 NetAdapterCx 注册结构。

在调用时 **NET_ADAPTER_OFFLOAD_GSO_CAPABILITIES_INIT** 客户端驱动程序提供指向 [*EVT_NET_ADAPTER_OFFLOAD_SET_GSO*](/windows-hardware/drivers/ddi/netadapteroffload/nc-netadapteroffload-evt_net_adapter_offload_set_gso) 回调的指针。 如果活动卸载功能发生变化，系统稍后会调用此回调。

### <a name="rules-for-indicating-hardware-gso-capabilities"></a>指示硬件 GSO 功能的规则

以下规则适用于 [**NET_ADAPTER_OFFLOAD_GSO_CAPABILITIES**](/windows-hardware/drivers/ddi/netadapteroffload/ns-netadapteroffload-_net_adapter_offload_gso_capabilities) 结构：

1. 驱动程序必须设置 **Layer3Flags** 和 **Layer4Flags** 。

1. 如果 NIC 支持 LSO，则驱动程序必须在 **Layer4Flags** 字段中填充 `NetAdapterOffloadLayer4FlagTcpWithoutOptions` TCP 标志。

1. 如果 NIC 支持 USO，则驱动程序必须在 **Layer4Flags** 字段中填充 `NetAdapterOffloadLayer4FlagUdp` UDP 标志。

1. **MaximumOffloadSize** 和 **MinimumSegmentCount** 是必填字段。

1. **Layer4OffsetLimit** 字段是可选的。 如果 OS 发送的数据包的标头偏移大于指定的限制，则不会要求执行 GSO。

1. 如果支持选项/扩展，则必须支持没有选项/扩展的 IP/TCP 数据包。

此示例演示客户端驱动程序如何设置其硬件卸载功能。

```C++
VOID
MyAdapterSetOffloadCapabilities(
    NETADAPTER NetAdapter
)
{
    // Configure the hardware's GSO offload capabilities
    NET_ADAPTER_OFFLOAD_GSO_CAPABILITIES gsoOffloadCapabilities;

    auto const layer3Flags = NetAdapterOffloadLayer3FlagIPv4NoOptions |
        NetAdapterOffloadLayer3FlagIPv4WithOptions |
        NetAdapterOffloadLayer3FlagIPv6NoExtensions |
        NetAdapterOffloadLayer3FlagIPv6WithExtensions;

    auto const layer4Flags = NetAdapterOffloadLayer4FlagTcpNoOptions |
        NetAdapterOffloadLayer4FlagTcpWithOptions;
        NetAdapterOffloadLayer4FlagUdp;

    NET_ADAPTER_OFFLOAD_GSO_CAPABILITIES_INIT(
        &gsoOffloadCapabilities,
        layer3Flags,
        layer4Flags,
        MY_GSO_OFFLOAD_MAX_SIZE,
        MY_GSO_OFFLOAD_MIN_SEGMENT_COUNT,
        EvtAdapterOffloadSetGso);

    gsoOffloadCapabilities.Layer4OffsetLimit = 127;

    // Set the current GSO offload capabilities and register the callback for future changes in active capabilities
    NetAdapterOffloadSetGsoCapabilities(NetAdapter, &gsoOffloadCapabilities);
}
```

## <a name="updating-hardware-offloads"></a>更新硬件卸载

如果 TCP/IP 堆栈或过量协议驱动程序请求更改网络适配器的活动功能，NetAdapterCx 将调用在适配器初始化期间注册的客户端驱动程序的 [*EVT_NET_ADAPTER_OFFLOAD_SET_GSO*](/windows-hardware/drivers/ddi/netadapteroffload/nc-netadapteroffload-evt_net_adapter_offload_set_gso) 回调。 在此函数中，系统在 NETOFFLOAD 对象中提供更新的功能，客户端驱动程序将查询这些功能以更新其卸载功能。

客户端驱动程序可以调用以下函数来确定启用了哪些卸载：

* [**NetOffloadIsLsoIPv4Enabled**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netoffloadislsoipv4enabled)
* [**NetOffloadIsLsoIPv6Enabled**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netoffloadislsoipv6enabled)
* [**NetOffloadIsUsoIPv4Enabled**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netoffloadisusoipv4enabled)
* [**NetOffloadIsUsoIPv6Enabled**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netoffloadisusoipv6enabled)

下面的示例演示了客户端驱动程序如何更新其 GSO 卸载功能：

```C++
VOID
MyEvtAdapterOffloadSetGso(
    NETADAPTER NetAdapter,
    NETOFFLOAD Offload
)
{
    PMY_NET_ADAPTER_CONTEXT adapterContext = MyGetNetAdapterContext(NetAdapter);

    // Store the updated information in the context
    adapterContext->LSOv4 = NetOffloadIsLsoIPv4Enabled(Offload) ? 
        GsoOffloadEnabled : GsoOffloadDisabled;
    adapterContext->LSOv6 = NetOffloadIsLsoIPv6Enabled(Offload) ?
        GsoOffloadEnabled : GsoOffloadDisabled;
    adapterContext->USOv4 = NetOffloadIsUsoIPv4Enabled(Offload) ? 
        GsoOffloadEnabled : GsoOffloadDisabled;
    adapterContext->USOv6 = NetOffloadIsUsoIPv6Enabled(Offload) ?
        GsoOffloadEnabled : GsoOffloadDisabled;

    // Enable hardware checksum if LSO/USO is enabled
    MyUpdateHardwareChecksum(adapterContext);
}
```
