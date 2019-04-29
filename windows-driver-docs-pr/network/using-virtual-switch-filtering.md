---
title: 使用虚拟交换机筛选
description: 使用虚拟交换机筛选
ms.assetid: 09325037-F9A4-45C8-97E0-8FCA7D42A120
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c48c44856961ddf2b5cc7ee8abddda0289b13344
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361809"
---
# <a name="using-virtual-switch-filtering"></a>使用虚拟交换机筛选

## <a name="overview-of-virtual-switch-filtering"></a>筛选虚拟交换机概述

Windows 8 和更高版本的 Windows 中支持虚拟交换机筛选。

此 WFP 功能允许 MAC 报头、 IP 标头和上部协议端口的字段，以及虚拟交换机虚拟端口 (VPort) 和虚拟机标识符 (VM ID) 等的特定字段进行筛选。 这些层上的所有数据包通过虚拟交换机的每个数据包基础调用。 从虚拟交换机扩展筛选器访问这些层 — NDIS 轻型筛选器 (LWF) 驱动程序的类型。

标注驱动程序调用[ **FwpsvSwitchEventsSubscribe0** ](https://msdn.microsoft.com/library/windows/hardware/hh439687)函数以注册回调入口点的虚拟交换机层事件。

中指定的回调通知函数的入口点[ **FWPS\_VSWITCH\_事件\_调度\_TABLE0** ](https://msdn.microsoft.com/library/windows/hardware/hh451263)结构. 提供的回调函数包括：

* [*FWPS\_VSWITCH\_FILTER\_ENGINE\_REORDER\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451267)
* [*FWPS\_VSWITCH\_INTERFACE\_EVENT\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451269)
* [*FWPS\_VSWITCH\_LIFETIME\_EVENT\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451271)
* [*FWPS\_VSWITCH\_POLICY\_EVENT\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451272)
* [*FWPS\_VSWITCH\_PORT\_EVENT\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451276)
* [*FWPS\_VSWITCH\_RUNTIME\_STATE\_RESTORE\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451281)
* [*FWPS\_VSWITCH\_RUNTIME\_STATE\_SAVE\_CALLBACK0*](https://msdn.microsoft.com/library/windows/hardware/hh451286)

[ **FWPS\_VSWITCH\_事件\_类型**](https://msdn.microsoft.com/library/windows/hardware/hh451265)枚举定义的值*eventType*虚拟参数切换通知函数。

标注驱动程序必须最终调用[ **FwpsvSwitchEventsUnsubscribe0** ](https://msdn.microsoft.com/library/windows/hardware/hh439691)释放系统资源。

如果标注驱动程序将返回状态\_WFP 通知函数从 PENDING，WFP 将返回状态\_PENDING 到 OID 请求处理程序。 标注驱动程序必须调用[ **FwpsvSwitchNotifyComplete0** ](https://msdn.microsoft.com/library/windows/hardware/hh439695)函数来完成挂起操作。 之后**FwpsvSwitchNotifyComplete0**调用，WFP 调用[ **NdisFOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561833)函数来完成虚拟交换机的 OID。

回调不应添加或删除通知函数的上下文中同步的 WFP 筛选器。 此外，如果该通知功能允许回调返回状态\_PENDING，并标注返回状态\_挂起、 标注不应添加或删除之前完成通知的 WFP 筛选器。

## <a name="wfp-virtual-switch-filter-layer-and-fields"></a>WFP 虚拟交换机筛选层和字段

[运行时筛选层标识符](https://msdn.microsoft.com/library/windows/hardware/ff570731)虚拟交换机筛选包括：

* FWPS\_LAYER\_INGRESS\_VSWITCH\_ETHERNET
* FWPS\_LAYER\_EGRESS\_VSWITCH\_ETHERNET
* FWPS\_层\_入口\_VSWITCH\_传输\_V4
* FWPS\_层\_入口\_VSWITCH\_传输\_V6
* FWPS\_层\_出口\_VSWITCH\_传输\_V4
* FWPS\_层\_出口\_VSWITCH\_传输\_V6

[数据字段标识符](https://msdn.microsoft.com/library/windows/hardware/ff546312)虚拟交换机筛选包括：

* [**FWPS\_FIELDS\_EGRESS\_VSWITCH\_ETHERNET**](https://msdn.microsoft.com/library/windows/hardware/hh439709)
* [**FWPS\_FIELDS\_EGRESS\_VSWITCH\_TRANSPORT\_V4**](https://msdn.microsoft.com/library/windows/hardware/hh439715)
* [**FWPS\_FIELDS\_EGRESS\_VSWITCH\_TRANSPORT\_V6**](https://msdn.microsoft.com/library/windows/hardware/hh439721)
* [**FWPS\_FIELDS\_INGRESS\_VSWITCH\_ETHERNET**](https://msdn.microsoft.com/library/windows/hardware/hh439733)
* [**FWPS\_FIELDS\_INGRESS\_VSWITCH\_TRANSPORT\_V4**](https://msdn.microsoft.com/library/windows/hardware/hh439738)
* [**FWPS\_FIELDS\_INGRESS\_VSWITCH\_TRANSPORT\_V6**](https://msdn.microsoft.com/library/windows/hardware/hh439745)

## <a name="guidance-for-wfp-virtual-switch-callout-writers"></a>WFP 虚拟交换机标注编写器的指南

### <a name="port-0-traffic"></a>端口 0 流量

有关 WFP 虚拟交换机标注流量从端口 0 (默认端口 ID) 是受信任和不会筛选。 这是因为通常情况下，端口 0 流量源自驱动程序堆栈中的其他扩展，因此会被作为特权和受信任的数据路径。 虚拟交换机扩展将尽量少使用端口 0，如发起控制数据包时，它不应筛选并拒绝任何基础扩展的情况下进行。 有关 HYPER-V 可扩展交换机源端口 mofification 详细信息，请参阅[修改数据包的可扩展切换源端口数据](modifying-a-packet-s-extensible-switch-source-port-data.md)。

### <a name="callout-matching-rules"></a>标注匹配规则

在定义用于筛选匹配规则时，虚拟交换机标注不应使用的 MAC 地址为基础进行比较。 在运行时，可以更改 MAC 地址和某些端口可能会生成从多个 MAC 地址的流量。 相反，调出应使用更持久的匹配规则，例如 NIC ID，将不会更改。

### <a name="io-virtualization-iov-and-wfp-coexistence"></a>I/O 虚拟化 （） 技术和 WFP 共存

不能在 IOV 上启用 WFP 切换，则将无法由操作系统尝试启用它。

### <a name="enabling-or-disabling-wfp"></a>启用或禁用 WFP

WFP 虚拟交换机标注为安装程序不应修改 WFP 启用扩展状态;也就是说，它们不应启用或禁用 WFP 本身。



