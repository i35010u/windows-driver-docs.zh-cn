---
title: 网络适配器的设备电源状态
description: 网络适配器的设备电源状态
ms.assetid: 969aadc9-e797-4a07-9714-8c2c5a6357da
keywords:
- Nic WDK 网络、 电源状态
- 网络接口卡 WDK 网络、 电源状态
- 设备电源状态 WDK 网络
- 电源状态 WDK 网络
- 电源管理 WDK NDIS 微型端口设备电源状态
- 转换电源状态 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 800da6faa1c0f9a20b9c878613119c7c1e105ff3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381387"
---
# <a name="device-power-states-for-network-adapters"></a>网络适配器的设备电源状态





网络适配器的设备电源状态描述的功率消耗和计算活动的网络适配器的级别。

有四个设备的电源状态：D0、 D1、 D2 和 D3。 D0 是 highest-powered 状态。 D1 和 D2，D3 是处于休眠状态的状态。 D3 细分为 D3hot 和 D3cold。

状态数成反比与功率消耗： 编号较高的状态使用较少的电量。 Power 可能从 D3 状态中的网络适配器中完全删除。

设备状态的详尽描述，请参阅以下主题：

* [设备的电源状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)
* [设备处于工作状态 D0](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-working-state-d0)
* [设备低功耗状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)
* [设备的电源状态所需的支持](https://docs.microsoft.com/windows-hardware/drivers/kernel/required-support-for-device-power-states)

**请注意**  NDIS 进程电源管理 Irp，但 NDIS 驱动程序不这样做。

 

网络适配器的设备电源状态定义，如下所示：

### <a href="" id="d0"></a>设备处于工作状态 D0

此电源状态描述的所有设备[设备正常工作状态 D0](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-working-state-d0)。 网络适配器和微型端口驱动程序：

<a href="" id="power-consumption"></a>功率消耗  
网络适配器是完全供电和交付完整的功能和性能。

<a href="" id="device-context"></a>设备上下文  
硬件设备上下文由网络适配器和/或微型端口驱动程序进行维护。

<a href="" id="miniport-driver-and-network-adapter-behavior"></a>微型端口驱动程序和网络适配器行为  
网络适配器是网络的完全符合附加的要求。 由于低能耗要求微型端口驱动程序和网络适配器的操作不受限制。

<a href="" id="restore-time"></a>还原时间  
不适用。

### <a href="" id="d1"></a>设备电源状态 D1

此电源状态描述的所有设备[设备低功耗状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)。 网络适配器和微型端口驱动程序：

<a href="" id="power-consumption"></a>功率消耗  
此状态是 highest-powered 睡眠状态。 功率消耗最小值 D0 状态和大于或等于在 D2 状态中。

<a href="" id="device-context"></a>设备上下文  
微型端口驱动程序应保留可能会丢失任何硬件的设备上下文。 设备返回到 D0 状态时，微型端口驱动程序应还原此类上下文。

<a href="" id="miniport-driver-and-network-adapter-behavior"></a>微型端口驱动程序和网络适配器行为  
微型端口驱动程序不接收协议驱动程序从传输请求。 NDIS 或者通知绑定的协议驱动程序的网络适配器的转换为休眠状态或 NDIS 协议驱动程序是否是电源管理感知的旧驱动程序，禁用从协议驱动程序的传输请求。 但是，微型端口驱动程序应该能够处理在其中它会接收传输请求，在此低功耗状态时的情况。 在这种情况下，微型端口驱动程序应该传输的所有请求会都失败。

微型端口驱动程序并不表示任何数据包会处于此状态时，可能会收到的网络适配器。

网络适配器不会生成中断。 但是，微型端口驱动程序必须能够处理中断，因为无法在总线上生成共享的中断。

<a href="" id="restore-time"></a>还原时间  
若要还原到 D0 状态的网络适配器的时间是小于所需的网络适配器处于 D2 状态时。

### <a href="" id="d2"></a>设备电源状态更改为 D2

此电源状态描述的所有设备[设备低功耗状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)。 网络适配器和微型端口驱动程序：

<a href="" id="power-consumption"></a>功率消耗  
中间的睡眠状态。 功率消耗最小值在 D1 状态和大于或等于 D3 状态中。

<a href="" id="device-context"></a>设备上下文  
D1 的一样。

<a href="" id="miniport-driver-and-network-adapter-behavior"></a>微型端口驱动程序和网络适配器行为  
D1 的一样。

<a href="" id="restore-time"></a>还原时间  
若要还原到 D0 状态的网络适配器的时间是大于所需的网络适配器处于 D1 状态时和较小的网络适配器处于 D3 状态时所需的值。

### <a href="" id="d3"></a>设备电源状态 D3

此电源状态描述的所有设备[设备低功耗状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)。 网络适配器和微型端口驱动程序：

<a href="" id="power-consumption"></a>功率消耗  
带的电量最少的睡眠状态。 所需的能力可能会为非零值 (D3hot) 也可能是完全为零 (D3cold)。 有关 D3hot 和 D3cold 的详细信息，请参阅[设备低功耗状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)。

<a href="" id="device-context"></a>设备上下文  
D1 的一样。

<a href="" id="miniport-driver-and-network-adapter-behavior"></a>微型端口驱动程序和网络适配器行为  
D1 的一样。

<a href="" id="restore-time"></a>还原时间  
若要还原到 D0 状态的网络适配器的时间大于的所需的网络适配器处于 D2 状态时。

网络适配器可以转换为休眠状态之前，其微型端口驱动程序必须禁用微型端口驱动程序的控制下的所有内容： 中断，必须先禁用、 计时器必须取消等。 总线驱动程序将网络适配器设置为 D3 状态后，微型端口驱动程序无法访问网络适配器硬件。

### <a name="transitions-allowed-between-device-power-states"></a>允许在设备电源状态之间转换

允许在设备电源状态之间的唯一转换为 highest-powered 状态 (D0) 到休眠状态 （D1，D2，D3），或从休眠状态到 highest-powered 状态。 NDIS 永远不会直接从一种睡眠状态到另一个转换命令的网络适配器。

 

 





