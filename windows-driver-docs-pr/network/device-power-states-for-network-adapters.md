---
title: 网络适配器的设备电源状态
description: 网络适配器的设备电源状态
keywords:
- Nic WDK 网络，电源状态
- 网络接口卡 WDK 网络，电源状态
- 设备电源状态 WDK 网络
- 电源状态 WDK 网络
- 电源管理 WDK NDIS 微型端口，设备电源状态
- 转换电源状态 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27520d6a079679b192bd9ac523ac1963b523e9e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808651"
---
# <a name="device-power-states-for-network-adapters"></a>网络适配器的设备电源状态





网络适配器的设备电源状态描述网络适配器的功率消耗和计算活动级别。

有四种设备电源状态： D0、D1、D2 和 D3。 D0 是最高的供电状态。 D1、D2 和 D3 为休眠状态。 D3 已细分为 D3hot 和 D3cold。

状态号码与功率消耗成反比：更高编号的状态使用更少的电量。 在 D3 状态中可能会完全从网络适配器中删除电源。

有关设备状态的详细说明，请参阅以下主题：

* [设备电源状态](../kernel/device-power-states.md)
* [设备工作状态 D0](../kernel/device-working-state-d0.md)
* [设备低功耗状态](../kernel/device-sleeping-states.md)
* [设备电源状态所需的支持](../kernel/required-support-for-device-power-states.md)

**注意**  NDIS 处理电源管理 Irp，而 NDIS 驱动程序则不处理。

 

网络适配器的设备电源状态定义如下：

### <a name="device-working-state-d0"></a><a href="" id="d0"></a>设备工作状态 D0

对于 [设备工作状态 D0](../kernel/device-working-state-d0.md)中的所有设备，描述此电源状态。 对于网络适配器和微型端口驱动程序：

<a href="" id="power-consumption"></a>功率消耗  
网络适配器完全驱动并提供完整的功能和性能。

<a href="" id="device-context"></a>设备上下文  
硬件设备上下文由网络适配器或微型端口驱动程序来维护。

<a href="" id="miniport-driver-and-network-adapter-behavior"></a>微型端口驱动程序和网络适配器行为  
网络适配器完全符合连接的网络的要求。 由于低能耗要求，微型端口驱动程序和网络适配器的操作不受限制。

<a href="" id="restore-time"></a>还原时间  
不适用。

### <a name="device-power-state-d1"></a><a href="" id="d1"></a>设备电源状态 D1

对于 [设备 Low-Power 状态](../kernel/device-sleeping-states.md)中的所有设备，都描述了此电源状态。 对于网络适配器和微型端口驱动程序：

<a href="" id="power-consumption"></a>功率消耗  
此状态是最高的休眠状态。 功率消耗小于 D0 状态中大于或等于 D2 状态的。

<a href="" id="device-context"></a>设备上下文  
微型端口驱动程序应保留任何可能丢失的硬件设备上下文。 当设备返回到 D0 状态时，微型端口驱动程序应还原此类上下文。

<a href="" id="miniport-driver-and-network-adapter-behavior"></a>微型端口驱动程序和网络适配器行为  
微型端口驱动程序不会接收来自协议驱动程序的传输请求。 NDIS 将网络适配器转换的绑定协议驱动程序通知到休眠状态，或者，如果协议驱动程序是不能识别电源的旧驱动程序，NDIS 将禁用来自协议驱动程序的传输请求。 但是，微型端口驱动程序应该能够处理在此低功耗状态下接收传输请求的情况。 在这种情况下，微型端口驱动程序应使所有传输请求失败。

微型端口驱动程序不会指示网络适配器在处于此状态时可能会收到的任何数据包。

网络适配器不会生成中断。 但是，微型端口驱动程序必须能够处理中断，因为可以在总线上生成共享中断。

<a href="" id="restore-time"></a>还原时间  
将网络适配器还原到 D0 状态的时间小于网络适配器处于 D2 状态时所需的时间。

### <a name="device-power-state-d2"></a><a href="" id="d2"></a>设备电源状态 D2

对于 [设备 Low-Power 状态](../kernel/device-sleeping-states.md)中的所有设备，都描述了此电源状态。 对于网络适配器和微型端口驱动程序：

<a href="" id="power-consumption"></a>功率消耗  
中间睡眠状态。 功率消耗小于 D1 状态中大于或等于 D3 状态的。

<a href="" id="device-context"></a>设备上下文  
与 D1 相同。

<a href="" id="miniport-driver-and-network-adapter-behavior"></a>微型端口驱动程序和网络适配器行为  
与 D1 相同。

<a href="" id="restore-time"></a>还原时间  
将网络适配器还原到 D0 状态的时间大于在网络适配器处于 D1 状态时所需的时间，并且低于网络适配器处于 D3 状态时所需的时间。

### <a name="device-power-state-d3"></a><a href="" id="d3"></a>设备电源状态 D3

对于 [设备 Low-Power 状态](../kernel/device-sleeping-states.md)中的所有设备，都描述了此电源状态。 对于网络适配器和微型端口驱动程序：

<a href="" id="power-consumption"></a>功率消耗  
电量最少的睡眠状态。 电源量不能为非零值 (D3hot) ，也可以是 (D3cold) 的完全相同的值。 有关 D3hot 和 D3cold 的详细信息，请参阅 [设备 Low-Power 状态](../kernel/device-sleeping-states.md)。

<a href="" id="device-context"></a>设备上下文  
与 D1 相同。

<a href="" id="miniport-driver-and-network-adapter-behavior"></a>微型端口驱动程序和网络适配器行为  
与 D1 相同。

<a href="" id="restore-time"></a>还原时间  
将网络适配器还原到 D0 状态的时间大于在网络适配器处于 D2 状态时所需的时间。

在网络适配器可以转换为睡眠状态之前，其微型端口驱动程序必须禁用微型端口驱动程序的控制下的所有内容：必须禁用中断，必须取消计时器，依此类推。 当总线驱动程序将网络适配器设置为 D3 状态后，微型端口驱动程序无法访问网络适配器硬件。

### <a name="transitions-allowed-between-device-power-states"></a>允许在设备电源状态之间进行转换

在设备电源状态之间唯一允许的转换是从最高功率状态 (D0) 到休眠状态， (D1，D2，D3) ，或从休眠状态到最高功率状态。 NDIS 从不命令网络适配器直接从一个休眠状态转换到另一个睡眠状态。

 

