---
title: NetAdapterCx 硬件卸载
description: NetAdapterCx 卸载
ms.assetid: 85A819E2-6352-4DE9-9689-3DCEB9B0AAD8
keywords:
- WDF 网络适配器类扩展卸载，NetAdapterCx 硬件卸载功能，将卸载 NetAdapterCx，NetAdapter 将卸载
ms.date: 01/18/2019
ms.custom: 19H1
ms.openlocfilehash: ea184c78e2baba23be7dd780446edd535adbdc83
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375353"
---
# <a name="netadaptercx-hardware-offloads"></a>NetAdapterCx 硬件卸载

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

若要提高其性能，Windows TCP/IP 堆栈可以一些将任务卸载到具有适当任务卸载能力的网络接口卡 (NIC)。

## <a name="overview-of-offloads-in-netadaptercx"></a>NetAdapterCx 中卸载的概述

NetAdapterCx 重点介绍易于卸载配置和管理的卸载功能。 客户端驱动程序只需指定其硬件卸载功能的简单配置并注册回调的功能中的更改通知。 

本指南提供了硬件的重要概念的概述将卸载 NetAdapterCx 中。

- 硬件卸载功能在初始化期间播发的网络适配器硬件，并且必须在调用之前播发[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart)。
- 该驱动程序不需要担心检查标准注册表关键字。 NetAdapterCx 检查注册表关键字，并遵循它们时启用活动卸载功能。
- *Active*网络适配器的卸载功能是指那些网络适配器是当前编程，以便执行。 这些是以前所播发的客户端驱动程序的硬件功能的子集。
- TCP/IP 堆栈或过量的协议驱动程序可以请求中的网络适配器活动功能的更改。 客户端驱动程序向 NetAdapterCx active 卸载功能中的更改通知注册回调。
- 如果数据包扩展需要以进行卸载，它会自动注册时的网络适配器会通告硬件卸载功能的支持。

客户端驱动程序播发到 NetAdapterCx 功能将最小集。 其中不包括所有支持的客户端驱动程序的卸载组合的精细功能详细信息。 例如，这可以是是否支持 IPOptions、 IPExtensions 或 TCPOptions，等等。这意味着客户端驱动程序负责执行卸载所有组合的播发的功能。 例如，对 IPv4 意味着 IPOptions 支持的支持、 对 IPv6 意味着 IPExtensions，支持的支持并支持 TCP 暗示支持为 TCPOptions。 

如果硬件不是可用于处理特定组合的它应不声明对该功能的支持或当遇到此类数据包执行软件回退。

NetAdapterCx 和 Windows TCP/IP 堆栈支持以下卸载：

| 卸载名称 | 描述 |
| --- | --- |
| 校验和 | 卸载的计算和 nic 的 IP 和 TCP 校验和验证 |
| 大量发送卸载 (LSO) | 卸载对 IPv4 和 IPv6 的大型 TCP 数据包分段。 |

## <a name="configuring-hardware-offloads"></a>配置硬件卸载

客户端驱动程序在网络适配器初始化期间首次播发其硬件校验和卸载功能。 这可能会发生的上下文中[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)启动时的网络适配器。 若要开始，客户端驱动程序分配功能结构以进行每个受支持的卸载、 初始化它们，并调用适当**NetAdapterOffloadSetXxxCapabilities**注册 NetAdapterCx 的方法。 在调用**NET_ADAPTER_OFFLOAD_XxX_CAPABILITIES_INIT**，驱动程序提供了指向系统如果 active 硬件卸载功能更改会更高版本调用的回调函数的指针。

此示例演示客户端驱动程序可能会如何设置其硬件卸载功能。

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

如果 TCP/IP 堆栈或过量的协议驱动程序请求中的网络适配器活动功能的更改，NetAdapterCx 调用客户端驱动程序*EVT_NET_ADAPTER_OFFLOAD_SET_XxX*回调函数以前注册适配器初始化过程。 在此函数中，则系统将提供在 NETOFFLOAD obbject，客户端驱动程序可以查询和用于更新其卸载功能的更新的功能。

下面的示例演示如何客户端驱动程序可能会更新其校验和卸载功能：

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

下一步类似的示例显示了客户端驱动程序可能会如何更新其 LSO 卸载功能：

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

[**NET_ADAPTER_OFFLOAD_CHECKSUM_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/ns-netadapter-_net_adapter_offload_checksum_capabilities)

[**NET_ADAPTER_OFFLOAD_CHECKSUM_CAPABILITIES_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-net_adapter_offload_checksum_capabilities_init)

[**NetAdapterOffloadSetChecksumCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapteroffloadsetchecksumcapabilities)

[*EvtNetAdapterOffloadSetChecksum*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_offload_set_checksum)

[**NET_ADAPTER_OFFLOAD_LSO_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapteroffload/ns-netadapteroffload-_net_adapter_offload_lso_capabilities)

[**NET_ADAPTER_OFFLOAD_LSO_CAPABILITIES_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapteroffload/nf-netadapteroffload-net_adapter_offload_lso_capabilities_init)

[**NetAdapterOffloadSetLsoCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapteroffload/nf-netadapteroffload-netadapteroffloadsetlsocapabilities)

[*EvtNetAdapterOffloadSetLso*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapteroffload/nc-netadapteroffload-evt_net_adapter_offload_set_lso)
