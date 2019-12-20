---
title: NetAdapterCx 硬件卸载
description: NetAdapterCx 卸载
ms.assetid: 85A819E2-6352-4DE9-9689-3DCEB9B0AAD8
keywords:
- WDF 网络适配器类扩展卸载，NetAdapterCx 硬件卸载，NetAdapterCx 卸载，Get-netadapter 卸载
ms.date: 01/18/2019
ms.custom: 19H1
ms.openlocfilehash: 4d54e71ea5ab04b9525d7443faa5affa003b0769
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209055"
---
# <a name="netadaptercx-hardware-offloads"></a>NetAdapterCx 硬件卸载

为了提高性能，Windows TCP/IP 堆栈可以将一些任务卸载到具有适当任务卸载功能的网络接口卡（NIC）。

## <a name="overview-of-offloads-in-netadaptercx"></a>NetAdapterCx 的卸载概述

NetAdapterCx 重点介绍减轻卸载功能的配置和管理。 客户端驱动程序只需为其硬件卸载功能指定简单的配置，并注册回调即可通知功能发生的更改。 

本指南概述了 NetAdapterCx 中硬件卸载的主要概念。

- 硬件卸载功能是在初始化期间由网络适配器硬件公布的，并且必须在调用[**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)之前播发。
- 驱动程序无需担心检查标准注册表关键字。 NetAdapterCx 检查注册表关键字，并在启用活动卸载功能时遵循这些关键字。
- 网络适配器的*活动*卸载功能是当前用来对网络适配器进行编程以执行的功能。 这些是之前的客户端驱动程序公布的硬件功能的子集。
- TCP/IP 堆栈或过量协议驱动程序可以请求网络适配器的活动功能更改。 客户端驱动程序向 NetAdapterCx 注册回调，以便在活动卸载功能发生更改时收到通知。
- 如果某个卸载需要数据包扩展，则该扩展将在网络适配器为硬件卸载公布支持时自动注册。

客户端驱动程序将最小的一组功能播发到 NetAdapterCx。 这不包括客户端驱动程序支持的所有卸载组合的粒度功能详细信息。 例如，这可以是支持 IPOptions、IPExtensions 或 TCPOptions，等等。这意味着客户端驱动程序负责对播发功能的所有组合执行卸载。 例如，对 IPv4 的支持表示支持 IPOptions，对 IPv6 的支持表示支持 IPExtensions，而对 TCP 的支持意味着支持 TCPOptions。 

如果硬件无法处理特定的组合，则它不应声明对该功能的支持或在遇到此类数据包时执行软件回退。

NetAdapterCx 和 Windows TCP/IP 堆栈支持以下卸载：

| 卸载名称 | 描述 |
| --- | --- |
| 校验和 | 将 IP 和 TCP 校验和的计算和验证卸载到 NIC。 |
| 大量发送卸载（LSO） | 为 IPv4 和 IPv6 卸载大 TCP 数据包的分段。 |

## <a name="configuring-hardware-offloads"></a>配置硬件卸载

客户端驱动程序首先在网络适配器初始化期间公布其硬件的校验和卸载功能。 启动网络适配器时，可能会出现在[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)的上下文中。 若要开始，客户端驱动程序将为每个受支持的卸载分配功能结构，对其进行初始化，并调用适当的**NetAdapterOffloadSetXxxCapabilities**方法将其注册到 NetAdapterCx。 在对**NET_ADAPTER_OFFLOAD_XxX_CAPABILITIES_INIT**的调用过程中，驱动程序将提供一个指向回调函数的指针，系统稍后会在活动硬件卸载功能发生更改时调用该函数。

此示例演示客户端驱动程序如何设置其硬件卸载功能。

```C++
VOID
MyAdapterSetOffloadCapabilities(
    NETADAPTER NetAdapter
)
{
    // Configure the hardware's checksum offload capabilities
    NET_ADAPTER_OFFLOAD_CHECKSUM_CAPABILITIES checksumOffloadCapabilities;
    NET_ADAPTER_OFFLOAD_CHECKSUM_CAPABILITIES_INIT(&checksumOffloadCapabilities,
                                                   TRUE,    // IPv4
                                                   TRUE,    // TCP
                                                   TRUE,    // UDP
                                                   MyEvtAdapterOffloadSetChecksum);

    // Set the current checksum offload capabilities and register the callback for future changes in active capabilities
    NetAdapterOffloadSetChecksumCapabilities(NetAdapter,
                                             &checksumOffloadCapabilities);

    // Configure the hardware's LSO offload capabilities
    NET_ADAPTER_OFFLOAD_LSO_CAPABILITIES lsoOffloadCapabilities;
    NET_ADAPTER_OFFLOAD_LSO_CAPABILITIES_INIT(&lsoOffloadCapabilities,
                                              TRUE,         // IPv4
                                              TRUE,         // IPv6
                                              MY_LSO_OFFLOAD_SIZE_MAX,
                                              MY_LSO_OFFLOAD_MIN_SEGMENT_COUNT,
                                              MyEvtAdapterOffloadSetLso);

    // Set the current LSO offload capabilities and register the callback for future changes in active capabilities
    NetAdapterOffloadSetLsoCapabilities(NetAdapter,
                                        &lsoOffloadCapabilities);   
}
```

## <a name="updating-hardware-offloads"></a>更新硬件卸载

如果 TCP/IP 堆栈或过量协议驱动程序请求网络适配器的活动功能的更改，则 NetAdapterCx 将调用客户端驱动程序的*EVT_NET_ADAPTER_OFFLOAD_SET_XxX*回调函数，该函数之前在适配器初始化期间注册的。 在此函数中，系统在 NETOFFLOAD obbject 中提供更新的功能，客户端驱动程序可以查询该功能并使用它来更新其卸载功能。

下面的示例演示客户端驱动程序可能如何更新其校验和卸载功能：

```C++
VOID
MyEvtAdapterOffloadSetChecksum(
    NETADAPTER  NetAdapter,
    NETOFFLOAD  Offload
)
{
    PMY_NET_ADAPTER_CONTEXT adapterContext = MyGetNetAdapterContext(NetAdapter);

    // Store the updated information in the context
    adapterContext->HardwareIpChecksum = NetOffloadIsChecksumIPv4Enabled(Offload);
    adapterContext->HardwareTcpChecksum = NetOffloadIsChecksumTcpEnabled(Offload);
    adapterContext->HardwareUdpChecksum = NetOffloadIsChecksumUdpEnabled(Offload);

    // Update the new hardware checksum offload capabilities
    MyUpdateHardwareChecksum(adapterContext);
}
```

下一个类似示例显示了客户端驱动程序可能如何更新其 LSO 卸载功能：

```C++
VOID
MyEvtAdapterOffloadSetLso(
    NETADAPTER NetAdapter,
    NETOFFLOAD Offload
)
{
    PMY_NET_ADAPTER_CONTEXT adapterContext = MyGetNetAdapterContext(NetAdapter);

    // Store the updated information in the context
    adapterContext->LSOv4 = NetOffloadIsLsoIPv4Enabled(Offload) ? 
        LsoOffloadEnabled : LsoOffloadDisabled;
    adapterContext->LSOv6 = NetOffloadIsLsoIPv6Enabled(Offload) ?
        LsoOffloadEnabled : LsoOffloadDisabled;

    // Enable hardware checksum if LSO is enabled
    MyUpdateHardwareChecksum(adapterContext);
}
```

## <a name="related-links"></a>相关链接

[数据包描述符和扩展](packet-descriptors-and-extensions.md)

[**NET_ADAPTER_OFFLOAD_CHECKSUM_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/ns-netadapter-_net_adapter_offload_checksum_capabilities)

[**NET_ADAPTER_OFFLOAD_CHECKSUM_CAPABILITIES_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-net_adapter_offload_checksum_capabilities_init)

[**NetAdapterOffloadSetChecksumCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapteroffloadsetchecksumcapabilities)

[*EvtNetAdapterOffloadSetChecksum*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_offload_set_checksum)

[**NET_ADAPTER_OFFLOAD_LSO_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapteroffload/ns-netadapteroffload-_net_adapter_offload_lso_capabilities)

[**NET_ADAPTER_OFFLOAD_LSO_CAPABILITIES_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-net_adapter_offload_lso_capabilities_init)

[**NetAdapterOffloadSetLsoCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netadapteroffloadsetlsocapabilities)

[*EvtNetAdapterOffloadSetLso*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapteroffload/nc-netadapteroffload-evt_net_adapter_offload_set_lso)
