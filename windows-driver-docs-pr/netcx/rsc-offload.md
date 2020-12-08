---
title: 接收段合并卸载
description: 接收段合并 (RSC) 卸载使用情况、规则和 NetAdapterCx 中的示例。
keywords:
- WDF 网络适配器类扩展卸载，NetAdapterCx 硬件卸载，NetAdapterCx 卸载，Get-netadapter 卸载，接收段合并卸载，RSC
ms.date: 10/13/2020
ms.custom: Fe
ms.openlocfilehash: cc1abd0e815adb5026ce3e038892db3c04fcb5fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808091"
---
# <a name="receive-segment-coalescing-rsc-offload"></a>接收段合并 (RSC) 卸载

> [!WARNING]
> 本主题中的一些信息与预发布的产品相关，该产品在商业发布之前可能会进行重大修改。 Microsoft 不对此处提供的信息作任何明示或默示的担保。
>
> NetAdapterCx 仅在 Windows 10 版本2004中处于预览阶段。
>
> 目前，NetAdapterCx 客户端驱动程序无法通过认证。

接收数据时，TCP/IP 堆栈中的大多数层都必须单独查看每个段的标头信息。 当收到大量数据时，这会产生大量的系统开销。

[ (RSC) 接收段合并会 ](../network/overview-of-receive-segment-coalescing.md) 将接收到的段序列合并，并在单个合并段中指示 tcp/ip 堆栈，从而减少此开销。 TCP/IP 堆栈中的上层只需查看整个序列的一个标头。
在硬件中支持 RSC 的网络接口卡 (NIC) 可以极大地提高接收路径性能。 它还可以降低主机 CPU 使用率，因为它可以在软件中使用 RSC 来释放协议层。

有关 RSC 的详细信息，请参阅 [接收段合并概述](../network/overview-of-receive-segment-coalescing.md)。

## <a name="inf-keywords-for-controlling-rsc-offload"></a>用于控制 RSC 卸载的 INF 关键字

NetAdapterCx 检查注册表关键字，并在启用活动卸载功能时遵循这些关键字。 驱动程序无需执行任何进一步操作。

在适用于 RSC 的 [标准化 INF 关键字](../network/standardized-inf-keywords-for-rsc.md) 中指定的 rsc 关键字，可用于通过注册表项设置启用/禁用 RSC 卸载。

## <a name="configuring-rsc-offload"></a>配置 RSC 卸载

客户端驱动程序首先在网络适配器初始化期间公布其硬件的 RSC 功能。 这可能会在启动网络适配器之前的 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调中发生。

若要配置 RSC 功能，请执行以下操作：

1. 分配 [**NET_ADAPTER_OFFLOAD_RSC_CAPABILITIES**](/windows-hardware/drivers/ddi/netadapteroffload/ns-netadapteroffload-_net_adapter_offload_rsc_capabilities) 结构。

1. 调用 [**NET_ADAPTER_OFFLOAD_RSC_CAPABILITIES_INIT**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-net_adapter_offload_rsc_capabilities_init) 以初始化结构。

1. 调用 [**NetAdapterOffloadSetRscCapabilities**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netadapteroffloadsetrsccapabilities) 来向 NetAdapterCx 注册结构。
 
在调用时 **NET_ADAPTER_OFFLOAD_RSC_CAPABILITIES_INIT** 客户端驱动程序提供指向 [*EVT_NET_ADAPTER_OFFLOAD_SET_RSC*](/windows-hardware/drivers/ddi/netadapteroffload/nc-netadapteroffload-evt_net_adapter_offload_set_rsc) 回调的指针。 如果活动卸载功能发生变化，系统稍后会调用此回调。

### <a name="rules-for-indicating-hardware-rsc-capabilities"></a>指示硬件 RSC 功能的规则

1. 对于在 NIC 中没有硬件支持的任何类型的通信，客户端驱动程序 **不得执行****软件** RSC。

以下规则适用于 [**NET_ADAPTER_OFFLOAD_RSC_CAPABILITIES**](/windows-hardware/drivers/ddi/netadapteroffload/ns-netadapteroffload-_net_adapter_offload_rsc_capabilities) 结构：

2. `NetAdapterOffloadLayer3FlagIPv4NoOptions` 和 `NetAdapterOffloadLayer3FlagIPv6NoExtensions` 是 **Layer3Flags** 字段唯一有效的值。 这些标志分别指示 IPv4 和 IPv6 支持。

3. `NetAdapterOffloadLayer4FlagTcpNoOptions` 是 **Layer4Flags** 字段唯一有效的值。

4. 如果设置了标志，则必须设置第3层标志 `NetAdapterOffloadLayer4FlagTcpNoOptions` 。

5. **TcpTimestampOption** 字段是可选的。 客户端驱动程序在调用 **NET_ADAPTER_OFFLOAD_RSC_CAPABILITIES_INIT** 之后和调用 **NetAdapterOffloadSetRscCapabilities** 之前，将此字段设置为指示 NIC 是否支持 TCP 时间戳选项。

以下示例演示客户端驱动程序如何设置其 RSC 硬件卸载功能。

```C++
VOID
MyAdapterSetRscOffloadCapabilities(
    NETADAPTER NetAdapter
)
{
    // Configure the hardware's RSC offload capabilities
    NET_ADAPTER_OFFLOAD_RSC_CAPABILITIES rscOffloadCapabilities;
    NET_ADAPTER_OFFLOAD_RSC_CAPABILITIES_INIT(
        &rscOffloadCapabilities,
        NetAdapterOffloadLayer3FlagIPv4NoOptions | NetAdapterOffloadLayer3FlagIPv6NoExtensions,
        NetAdapterOffloadLayer4FlagTcpNoOptions,
        MyEvtAdapterOffloadSetRsc);
    rscOffloadCapabilities.TcpTimestampOption = FALSE;

    // Set the current RSC offload capabilities and register the callback for future changes in active capabilities
    NetAdapterOffloadSetRscCapabilities(NetAdapter, &rscOffloadCapabilities);
}
```

## <a name="updating-rsc-hardware-offloads"></a>更新 RSC 硬件卸载

如果 TCP/IP 堆栈或过量协议驱动程序请求更改网络适配器的活动 RSC 功能，则 NetAdapterCx 将调用在 **NET_ADAPTER_OFFLOAD_RSC_CAPABILITIES** 中注册的客户端驱动程序的 [*EVT_NET_ADAPTER_OFFLOAD_SET_RSC*](/windows-hardware/drivers/ddi/netadapteroffload/nc-netadapteroffload-evt_net_adapter_offload_set_rsc)回调。 在此回调中，系统在 NETOFFLOAD 对象中提供更新的功能，客户端驱动程序可以通过查询这些功能来更新其卸载功能。

客户端驱动程序可以调用以下函数来确定启用了哪些 RSC 卸载：

* [**NetOffloadIsTcpRscIPv4Enabled**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netoffloadistcprscipv4enabled)
* [**NetOffloadIsTcpRscIPv6Enabled**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netoffloadistcprscipv6enabled)
* [**NetOffloadIsRscTcpTimestampOptionEnabled**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netoffloadisrsctcptimestampoptionenabled)


以下示例演示客户端驱动程序可能如何更新其 RSC 卸载功能：
```C++
VOID
MyEvtAdapterOffloadSetRsc(
    NETADAPTER NetAdapter,
    NETOFFLOAD Offload
)
{
    PMY_NET_ADAPTER_CONTEXT adapterContext = NetvAdapterGetContext(NetAdapter);

    // Store the updated information in the context
    adapterContext->IsRscIPv4Enabled = NetOffloadIsTcpRscIPv4Enabled(Offload);
    adapterContext->IsRscIPv6Enabled = NetOffloadIsTcpRscIPv6Enabled(Offload);
    adapterContext->IsRscTcpTimestampOptionEnabled = NetOffloadIsRscTcpTimestampOptionEnabled(Offload);
}
```
