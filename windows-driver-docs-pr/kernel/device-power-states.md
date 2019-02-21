---
title: 设备的电源状态
description: 设备的电源状态
ms.assetid: 2229f34c-9b88-4e3e-802e-f7be2c7ef168
keywords:
- 设备电源状态 WDK 内核
- 电源状态 WDK 内核
- 指出 WDK 电源管理
- Dx 名称 WDK 电源管理
- 低能耗模式 WDK 内核
- 节能模式 WDK 内核
- 连续 power WDK 内核
- 延迟 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15e0e40294b306f873788c21fa18856eb075d201
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554172"
---
# <a name="device-power-states"></a>设备的电源状态


## <a href="" id="ddk-device-power-states-kg"></a>


设备电源状态描述中的计算机，独立于计算机中的其他设备的设备的电源状态。 D0、 D1、 D2 和 D3 是名为设备的电源状态。 D0 是完全处于的状态，并 D1 和 D2，D3 是低功耗状态。 状态数成反比与功率消耗： 更高版本带编号的状态使用较少的电量。 从 Windows 8 开始，D3 状态被划分为两个子状态的状态，D3hot 和 D3cold。

设备的电源状态的特征体现在以下属性：

-   功率消耗：设备使用多少能源？

-   设备上下文：其操作上下文的多少设备保留在此状态？

-   设备驱动程序行为：设备的驱动程序为必须做什么将设备还原为完全可操作的状态？

-   还原时间：若要将设备还原为完全正常运行状态需要多长时间？ 大多数类型的设备具有不同少适度恢复时间从一台设备类到下一步。 仅几种类型的设备，Gpu，如有需要相当长的时间还原的非常大的硬件上下文。

-   唤醒功能：可以设备请求唤醒从这种状态？ 一般情况下，如果设备可以从给定的电源状态 (例如，D2) 请求唤醒，它还可以请求唤醒从任意 higher-powered 状态 (D1)。

电源状态的确切定义是特定于设备。 并非所有设备都定义所有的状态;多个设备定义只 D0 和 D3 状态。 请参阅指定的设备类电源管理参考，了解哪些设备的电源状态定义为特定设备和每个状态操作的要求是什么。 (引用规范目前[ACPI / 电源管理](https://go.microsoft.com/fwlink/p/?linkid=57185)网站。)

设备的电源状态不需要与匹配[系统电源状态](system-power-states.md)。 例如，某些设备可以是在关闭 (D3) 状态中即使系统处于[系统的工作状态 (S0)](system-working-state-s0.md)。

设备的电源状态可能似乎是无关的设备的父总线电源状态。 例如，USB 设备可能是在 D2 (选择性挂起) 时其父主机控制器处于 D3 状态的状态。 这两个状态显示为不一致，只是因为 Dx 状态的定义是 USB 和 USB 主控制器连接到总线 （通常是 PCI 或 PCI Express） 不同。

请注意，某些设备中的单个设备电源状态的多个不同的低能耗模式的支持。 如果其驱动程序可以自动切换到另一种模式的设备，而无需更改设备电源状态，此类设备可以使用这些模式。 作为一般规则，但是，如果没有在模式之间没有明显区别设备应使用仅是最低的电源模式。 如果低能耗模式，一种较慢的模式，如产生负面影响性能，或者不是透明的软件，只将设备驱动程序，硬件应该不会自动使用它。 请参阅设备类电源管理引用技术指标，有关详细信息。

驱动程序或电源管理器可以请求设备电源状态转换，而所有驱动程序必须准备好处理 Irp 请求这样的变革。 有关详情，请参阅以下主题：

[发送 IRP\_MN\_查询\_电源或 IRP\_MN\_设置\_的电源可用于设备的电源状态](sending-irp-mn-query-power-or-irp-mn-set-power-for-device-power-states.md)

[处理 IRP\_MN\_查询\_的电源可用于设备的电源状态](handling-irp-mn-query-power-for-device-power-states.md)

[处理 IRP\_MN\_设置\_的电源可用于设备的电源状态](handling-irp-mn-set-power-for-device-power-states.md)

## <a href="" id="power-state-diagram"></a>


与系统类似，设备可以转换从工作状态 (D0) 到任意低功耗状态 （D1、 D2 或 D3） 和任意低功耗状态到工作状态。 下图是显示电源状态转换的有效的设备的状态关系图。

![说明有效的设备电源状态转换的关系图](images/dxpostates.png)

此图显示了为 D3hot 和 D3cold D3 的细分。 从 Windows 8 开始定义 D3hot 和 D3cold。 支持 D0 状态和 D3hot 子状态所需的所有设备。 在关系图中所示的其他状态是可选的。

在前面的图形中，从 D3hot 过渡到 D3cold 是设备低功耗状态间的唯一直接转换。 低功耗状态之间的所有其他转换需要在中间转化为 D0，根据需要，可以进入下一步的低功耗状态或处于 D0 允许配置设备硬件的设备驱动程序。 但是，在设备退出 D3hot 和设备的电源处于关闭状态，这要求没有干预的设备驱动程序时，将进入 D3cold。 此驱动程序执行任何必要的配置的设备硬件设备进入 D3hot; 之前准备好转换设备 D3hot 到 D3cold 不需要任何其他配置。 有关详细信息，请参阅[驱动程序中支持 D3cold](supporting-d3cold-in-a-driver.md)。

 

 




