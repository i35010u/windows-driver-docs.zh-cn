---
title: 使用虚拟交换机筛选
description: 使用虚拟交换机筛选
ms.assetid: 09325037-F9A4-45C8-97E0-8FCA7D42A120
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 004c518b5e664ada3c6c6bc952dfaf35c1060d82
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212723"
---
# <a name="using-virtual-switch-filtering"></a>使用虚拟交换机筛选

## <a name="overview-of-virtual-switch-filtering"></a>虚拟交换机筛选概述

Windows 8 和更高版本的 Windows 支持虚拟交换机筛选。

此 WFP 功能允许在 MAC 标头、IP 标头和高级协议端口以及虚拟交换机特定字段（例如虚拟端口 (VPort) 和虚拟机标识符 (VM ID) ）中进行筛选。 对于遍历虚拟交换机的所有数据包，将根据每个数据包调用这些层。 可以从虚拟交换机扩展筛选器（一种类型的 NDIS 轻型筛选器 (LWF) 驱动程序）访问这些层。

标注驱动程序调用 [**FwpsvSwitchEventsSubscribe0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitcheventssubscribe0) 函数来注册虚拟交换机层事件的回调入口点。

回调通知函数的入口点是在 [**FWPS \_ VSWITCH \_ 事件 \_ 调度 \_ TABLE0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_vswitch_event_dispatch_table0_) 结构中指定的。 可用的回调函数包括：

* [*FWPS \_ VSWITCH \_ 筛选器 \_ 引擎 \_ 重新排序 \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_filter_engine_reorder_callback0)
* [*FWPS \_ VSWITCH \_ INTERFACE \_ EVENT \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_interface_event_callback0)
* [*FWPS \_ VSWITCH \_ 生存期 \_ 事件 \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_lifetime_event_callback0)
* [*FWPS \_ VSWITCH \_ 策略 \_ 事件 \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_policy_event_callback0)
* [*FWPS \_ VSWITCH \_ PORT \_ 事件 \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_port_event_callback0)
* [*FWPS \_ VSWITCH \_ 运行时 \_ 状态 \_ 还原 \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_runtime_state_restore_callback0)
* [*FWPS \_ VSWITCH \_ 运行时 \_ 状态 \_ SAVE \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_runtime_state_save_callback0)

[**FWPS \_ VSWITCH \_ 事件 \_ 类型**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_vswitch_event_type_)枚举定义虚拟交换机通知函数的*事件*类型参数的值。

标注驱动程序最终必须调用 [**FwpsvSwitchEventsUnsubscribe0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitcheventsunsubscribe0) 以释放系统资源。

如果注解驱动程序 \_ 从 WFP 通知函数返回 "挂起" 状态，则 wfp 会将 \_ 挂起的状态返回到 OID 请求处理程序。 标注驱动程序必须调用 [**FwpsvSwitchNotifyComplete0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitchnotifycomplete0) 函数来完成挂起的操作。 **FwpsvSwitchNotifyComplete0**调用后，WFP 会调用[**NdisFOidRequestComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequestcomplete)函数来完成虚拟交换机的 OID。

回调不应在通知函数的上下文中同步添加或删除 WFP 筛选器。 此外，如果通知函数允许回调返回状态 \_ "挂起"，并且标注返回状态 " \_ 挂起"，则在完成通知之前，标注不应添加或删除 WFP 筛选器。

## <a name="wfp-virtual-switch-filter-layer-and-fields"></a>WFP 虚拟交换机筛选层和字段

虚拟交换机筛选的[运行时筛选层标识符](./run-time-filtering-layer-identifiers.md)包括：

* FWPS \_ 层 \_ 入口 \_ VSWITCH \_ 以太网
* FWPS \_ 层 \_ 传出 \_ VSWITCH \_ 以太网
* FWPS \_ 层 \_ 入口 \_ VSWITCH \_ 传输 \_ V4
* FWPS \_ 层 \_ 入口 \_ VSWITCH \_ 传输 \_ V6
* FWPS \_ 层 \_ 传出 \_ VSWITCH \_ 传输 \_ V4
* FWPS \_ 层 \_ 传出 \_ VSWITCH \_ 传输 \_ V6

用于虚拟交换机筛选的[数据字段标识符](./data-field-identifiers.md)包括：

* [**FWPS \_ 字段 \_ 出口 \_ VSWITCH \_ 以太网**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_ethernet_)
* [**FWPS \_ 字段 \_ 出口 \_ VSWITCH \_ 传输 \_ V4**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_transport_v4_)
* [**FWPS \_ 字段 \_ 出口 \_ VSWITCH \_ 传输 \_ V6**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_transport_v6_)
* [**FWPS \_ 字段 \_ 入口 \_ VSWITCH \_ 以太网**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_ethernet_)
* [**FWPS \_ 字段 \_ 入口 \_ VSWITCH \_ 传输 \_ V4**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_transport_v4_)
* [**FWPS \_ 字段 \_ 入口 \_ VSWITCH \_ 传输 \_ V6**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_transport_v6_)

## <a name="guidance-for-wfp-virtual-switch-callout-writers"></a>WFP 虚拟交换机标注编写器指南

### <a name="port-0-traffic"></a>端口0流量

对于 WFP 虚拟交换机标注，来自端口0的流量 (默认端口 ID) 受信任，不应进行筛选。 这是因为，通常情况下，通过端口0的流量源自驱动程序堆栈中的其他扩展，因此，数据路径会将其视为特权和可信。 如果发出控制数据包，虚拟交换机扩展将会慎用端口0，因为它不应被任何基础扩展筛选和拒绝。 有关 Hyper-v 可扩展交换机源端口 mofification 的详细信息，请参阅 [修改数据包的可扩展交换机源端口数据](modifying-a-packet-s-extensible-switch-source-port-data.md)。

### <a name="callout-matching-rules"></a>标注匹配规则

为筛选定义匹配规则时，虚拟交换机标注不应将 MAC 地址用作比较的基础。 MAC 地址可能会在运行时更改，某些端口可能会从多个 MAC 地址生成流量。 相反，标注应使用更持久的匹配规则（如 NIC ID），这种规则将不会更改。

### <a name="io-virtualization-iov-and-wfp-coexistence"></a>I/o 虚拟化 () 和 WFP 共存

不能在连接交换机上启用 WFP，如果尝试启用它，则它会被操作系统阻塞。

### <a name="enabling-or-disabling-wfp"></a>启用或禁用 WFP

WFP 虚拟交换机标注的安装程序不应修改启用了 WFP 扩展的状态;也就是说，它们不应启用或禁用 WFP 本身。