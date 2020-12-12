---
title: 校验和卸载
description: NetAdapterCx 中的校验和卸载使用情况、规则和示例
keywords:
- WDF 网络适配器类扩展卸载，NetAdapterCx 硬件卸载，NetAdapterCx 卸载，Get-netadapter 卸载，校验和卸载
ms.date: 08/10/2020
ms.custom: Fe
ms.openlocfilehash: 81893d4324e36be7576d5eaba1b8b0ba032f39ff
ms.sourcegitcommit: 6d31ef1a1d9adedcded793a2f86cbe2bb467684a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97349634"
---
# <a name="checksum-offload"></a>校验和卸载

> [!WARNING]
> 本主题中的一些信息与预发布的产品相关，该产品在商业发布之前可能会进行重大修改。 Microsoft 不对此处提供的信息作任何明示或默示的担保。
>
> NetAdapterCx 仅在 Windows 10 版本2004中处于预览阶段。
>
> 目前，NetAdapterCx 客户端驱动程序无法通过认证。

NetAdapterCx 支持在运行时卸载 TCP/IP 校验和任务。

在 TCP/IP 传输将 [**NET_PACKET**](/windows-hardware/drivers/ddi/packet/ns-packet-_net_packet) 结构传递到客户端驱动程序之前，它会指定与 [**NET_PACKET_CHECKSUM**](/windows-hardware/drivers/ddi/checksumtypes/ns-checksumtypes-_net_packet_checksum) 数据包扩展中的 NET_PACKET 相关联的校验和信息。

在卸载 TCP/udp 数据包的校验和计算之前，TCP/IP 传输会计算 tcp/UDP pseudoheader 的补码总和，如 [卸载校验和任务](../network/offloading-checksum-tasks.md)中所述。

当启用 (GSO) 的 [通用分段卸载](gso-offload.md) 不会阻止客户端驱动程序在 GSO 功能生成的数据包中计算和插入校验和时，关闭校验和卸载。 若要完全禁用校验和卸载，还必须禁用 GSO。

## <a name="inf-keywords-for-controlling-checksum-offload"></a>用于控制校验和卸载的 INF 关键字

NetAdapterCx 检查注册表关键字，并在启用活动卸载功能时遵循这些关键字。 驱动程序无需执行任何进一步操作。

[使用注册表值启用和禁用任务卸载](../network/using-registry-values-to-enable-and-disable-task-offloading.md)中指定的校验和关键字可用于启用/禁用注册表项设置的校验和卸载。 不支持分组的关键字。

关键字值必须为 [REG_SZ](/windows/win32/sysinfo/registry-value-types)类型。

## <a name="configuring-checksum-offload"></a>配置校验和卸载

客户端驱动程序首先在网络适配器初始化期间公布其硬件的校验和卸载功能。 这可能会在启动网络适配器之前的 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调中发生。

若要配置传输 (Tx) 校验和卸载，客户端驱动程序：

1. 分配 [**NET_ADAPTER_OFFLOAD_TX_CHECKSUM_CAPABILITIES**](/windows-hardware/drivers/ddi/netadapteroffload/ns-netadapteroffload-_net_adapter_offload_tx_checksum_capabilities) 结构。

1. 调用 [**NET_ADAPTER_OFFLOAD_TX_CHECKSUM_CAPABILITIES_INIT**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-net_adapter_offload_tx_checksum_capabilities_init) 以初始化结构。

1. 调用 [**NetAdapterOffloadSetTxChecksumCapabilities**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netadapteroffloadsettxchecksumcapabilities) 来向 NetAdapterCx 注册结构。
 
在调用时 **NET_ADAPTER_OFFLOAD_TX_CHECKSUM_CAPABILITIES_INIT** 客户端驱动程序提供指向 [*EVT_NET_ADAPTER_OFFLOAD_SET_TX_CHECKSUM*](/windows-hardware/drivers/ddi/netadapteroffload/nc-netadapteroffload-evt_net_adapter_offload_set_tx_checksum) 回调的指针。 如果活动卸载功能发生变化，系统稍后会调用此回调。

若要配置接收 (Rx) 校验和卸载，客户端驱动程序：

1. 分配 [**NET_ADAPTER_OFFLOAD_RX_CHECKSUM_CAPABILITIES**](/windows-hardware/drivers/ddi/netadapteroffload/ns-netadapteroffload-_net_adapter_offload_rx_checksum_capabilities) 结构。

1. 调用 [**NET_ADAPTER_OFFLOAD_RX_CHECKSUM_CAPABILITIES_INIT**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-net_adapter_offload_rx_checksum_capabilities_init) 以初始化结构。

1. 调用 [**NetAdapterOffloadSetRxChecksumCapabilities**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netadapteroffloadsetrxchecksumcapabilities) 来向 NetAdapterCx 注册结构。

在调用时 **NET_ADAPTER_OFFLOAD_RX_CHECKSUM_CAPABILITIES_INIT** 客户端驱动程序提供指向 [*EVT_NET_ADAPTER_OFFLOAD_SET_RX_CHECKSUM*](/windows-hardware/drivers/ddi/netadapteroffload/nc-netadapteroffload-evt_net_adapter_offload_set_rx_checksum) 回调的指针。 如果活动卸载功能发生变化，系统稍后会调用此回调。

### <a name="rules-for-indicating-hardware-transmit-checksum-capabilities"></a>指示硬件传输校验和功能的规则

1. 必须设置 [**NET_ADAPTER_OFFLOAD_TX_CHECKSUM_CAPABILITIES**](/windows-hardware/drivers/ddi/netadapteroffload/ns-netadapteroffload-_net_adapter_offload_tx_checksum_capabilities) 结构中的 Layer3Flags。 设置 Layer4Flags 是可选的。 设置 Layer3Flags 和 Layer4Flags 表示 NIC 能够执行校验和卸载的数据包。

1. **NET_ADAPTER_OFFLOAD_TX_CHECKSUM_CAPABILITIES** 中的 Layer3HeaderOffsetLimit 和 Layer4HeaderOffsetLimit 是可选的。 如果 OS 发送的数据包的标头偏移量超过指定的限制，则不会请求 NIC 计算该层的校验和。

1. 如果支持选项/扩展，则必须支持没有选项/扩展的 IP/TCP 数据包。

### <a name="rules-for-indicating-hardware-receive-checksum-capabilities"></a>指示硬件接收校验和功能的规则

NetAdapterCx 不要求驱动程序公布硬件接收校验和功能。 如果启用校验和卸载，NIC 应该对它可以处理的所有数据包执行校验和卸载。 如果 NIC 无法在数据包上执行校验和卸载，NetAdapterCx 将在软件中卸载它。

此示例演示客户端驱动程序如何设置其硬件校验和卸载功能：

```C++
VOID
MyAdapterSetOffloadCapabilities(
    NETADAPTER NetAdapter
)
{
    // Configure the hardware's Tx checksum offload capabilities
    NET_ADAPTER_OFFLOAD_TX_CHECKSUM_CAPABILITIES txChecksumOffloadCapabilities;

    auto const layer3Flags = NetAdapterOffloadLayer3FlagIPv4NoOptions |
        NetAdapterOffloadLayer3FlagIPv4WithOptions |
        NetAdapterOffloadLayer3FlagIPv6NoExtensions |
        NetAdapterOffloadLayer3FlagIPv6WithExtensions;

    auto const layer4Flags = NetAdapterOffloadLayer4FlagTcpNoOptions |
        NetAdapterOffloadLayer4FlagTcpWithOptions |
        NetAdapterOffloadLayer4FlagUdp;

    NET_ADAPTER_OFFLOAD_TX_CHECKSUM_CAPABILITIES_INIT(
        &txChecksumOffloadCapabilities,
        layer3Flags,
        EvtAdapterOffloadSetTxChecksum);

    txChecksumOffloadCapabilities.Layer4Flags = layer4Flags;

    txChecksumOffloadCapabilities.Layer4HeaderOffsetLimit = 127;

    // Set the current Tx checksum offload capabilities and register the callback for future changes in active capabilities
    NetAdapterOffloadSetTxChecksumCapabilities(NetAdapter,
        &txChecksumOffloadCapabilities);

    // Configure the hardware's Rx checksum offload capabilities
    NET_ADAPTER_OFFLOAD_RX_CHECKSUM_CAPABILITIES rxChecksumOffloadCapabilities;

    NET_ADAPTER_OFFLOAD_RX_CHECKSUM_CAPABILITIES_INIT(
        &rxChecksumOffloadCapabilities,
        EvtAdapterOffloadSetRxChecksum);

    // Set the current Rx checksum offload capabilities and register the callback for future changes in active capabilities
    NetAdapterOffloadSetRxChecksumCapabilities(NetAdapter,
        &rxChecksumOffloadCapabilities);
}
```

## <a name="updating-hardware-offloads"></a>更新硬件卸载

如果 TCP/IP 堆栈或过量协议驱动程序请求更改网络适配器的活动功能，NetAdapterCx 将调用客户端驱动程序的 [*EVT_NET_ADAPTER_OFFLOAD_SET_TX_CHECKSUM*](/windows-hardware/drivers/ddi/netadapteroffload/nc-netadapteroffload-evt_net_adapter_offload_set_tx_checksum) 或在适配器初始化期间注册的 [*EVT_NET_ADAPTER_OFFLOAD_SET_RX_CHECKSUM*](/windows-hardware/drivers/ddi/netadapteroffload/nc-netadapteroffload-evt_net_adapter_offload_set_rx_checksum) 回调。 在这些函数中，系统在 NETOFFLOAD 对象中提供更新的功能，客户端驱动程序将查询这些功能以更新其卸载功能。

客户端驱动程序可以调用以下函数来确定启用了哪些校验和卸载：

* [**NetOffloadIsTxChecksumIPv4Enabled**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netoffloadistxchecksumipv4enabled)
* [**NetOffloadIsTxChecksumTcpEnabled**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netoffloadistxchecksumtcpenabled)
* [**NetOffloadIsTxChecksumUdpEnabled**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netoffloadistxchecksumudpenabled)
* [**NetOffloadIsRxChecksumIPv4Enabled**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netoffloadisrxchecksumipv4enabled)
* [**NetOffloadIsRxChecksumTcpEnabled**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netoffloadisrxchecksumtcpenabled)
* [**NetOffloadIsRxChecksumUdpEnabled**](/windows-hardware/drivers/ddi/netadapteroffload/nf-netadapteroffload-netoffloadisrxchecksumudpenabled)

下面的示例演示客户端驱动程序可能如何更新其 Tx/Rx 校验和卸载功能：

```C++
VOID
MyEvtAdapterOffloadSetTxChecksum(
    NETADAPTER  NetAdapter,
    NETOFFLOAD  Offload
)
{
    PMY_NET_ADAPTER_CONTEXT adapterContext = MyGetNetAdapterContext(NetAdapter);

    // Store the updated information in the context
    adapterContext->TxHardwareIpChecksum = NetOffloadIsTxChecksumIPv4Enabled(Offload);
    adapterContext->TxHardwareTcpChecksum = NetOffloadIsTxChecksumTcpEnabled(Offload);
    adapterContext->TxHardwareUdpChecksum = NetOffloadIsTxChecksumUdpEnabled(Offload);

    // Update the new hardware Tx checksum offload capabilities
    MyUpdateHardwareChecksum(adapterContext);
}

VOID
MyEvtAdapterOffloadSetRxChecksum(
    NETADAPTER  NetAdapter,
    NETOFFLOAD  Offload
)
{
    PMY_NET_ADAPTER_CONTEXT adapterContext = MyGetNetAdapterContext(NetAdapter);

    // Store the updated information in the context
    adapterContext->RxHardwareIpChecksum = NetOffloadIsRxChecksumIPv4Enabled(Offload);
    adapterContext->RxHardwareTcpChecksum = NetOffloadIsRxChecksumTcpEnabled(Offload);
    adapterContext->RxHardwareUdpChecksum = NetOffloadIsRxChecksumUdpEnabled(Offload);

    // Update the new hardware Rx checksum offload capabilities
    MyUpdateHardwareChecksum(adapterContext);
}
```

## <a name="transmit-checksum-processing"></a>传输校验和处理

通常，客户端驱动程序对传输路径执行以下校验和处理：

1. 客户端驱动程序使用数据包索引调用 [**NetExtensionGetPacketChecksum**](/windows-hardware/drivers/ddi/checksum/nf-checksum-netextensiongetpacketchecksum) 函数，以获取 [**NET_PACKET_CHECKSUM**](/windows-hardware/drivers/ddi/checksumtypes/ns-checksumtypes-_net_packet_checksum) 结构。

2. 客户端驱动程序测试 NET_PACKET_CHECKSUM 结构中特定于层的标志。

    * 如果标志为 `NetPacketTxChecksumActionPassthrough` ，则 NIC 不应在该层中执行校验和操作。

    * 如果标志为 `NetPacketTxChecksumActionRequired` ，则客户端驱动程序应使用 [**NET_PACKET_LAYOUT**](/windows-hardware/drivers/ddi/packet/ns-packet-_net_packet_layout) 结构确定该特定数据包在该层上所使用的协议，并向 NIC 指出应为数据包计算的校验和。

3. 客户端驱动程序将数据包传递到 NIC，这将为数据包计算相应的校验和。

## <a name="receive-checksum-processing"></a>接收校验和处理

在为用于执行校验和任务的接收数据包指示 [**NET_PACKET**](/windows-hardware/drivers/ddi/packet/ns-packet-_net_packet) 结构之前，客户端驱动程序将验证校验和，并在 [**NET_PACKET_CHECKSUM**](/windows-hardware/drivers/ddi/checksumtypes/ns-checksumtypes-_net_packet_checksum) 结构中设置相应的标志。

标志可以是以下各项之一：

| 标志 | 描述 |
| --- | --- |
| `NetPacketRxChecksumEvaluationNotChecked` | NIC 无法验证数据包的校验和 |
| `NetPacketRxChecksumEvaluationValid` | 数据包的校验和有效 |
| `NetPacketRxChecksumEvaluationInvalid` | 数据包的校验和无效 |
