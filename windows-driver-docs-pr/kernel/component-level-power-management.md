---
title: 组件级电源管理
description: 从开始 Windows 8 中，电源管理框架 (PoFx) 允许驱动程序来管理设备中的各个组件的电源状态。 组件级电源管理存在与设备级电源管理并行。
ms.assetid: 77866143-FB10-4623-9923-368B23808715
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 82dbc4d022ec8372b5d218406ce22ca948c7245d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377215"
---
# <a name="component-level-power-management"></a>组件级电源管理


从开始 Windows 8 中，电源管理框架 (PoFx) 允许驱动程序来管理设备中的各个组件的电源状态。 组件级电源管理存在与设备级电源管理并行。

## <a name="overview-of-component-level-power-management"></a>组件级电源管理概述


Windows 7 及更早版本的操作系统仅为设备级电源管理，从而使支持 D 状态中设备的驱动程序提供支持。 高级配置和电源接口 (ACPI) 规范定义了[设备的电源状态](device-power-states.md)D0 （完全启用） 通过 D3 （完全关闭），并定义[系统电源状态](system-power-states.md)S0 （完全启用） 到 S5 （完全关闭）。 这些版本的 Windows 不提供机制来独立地管理设备中的各个组件的电源。 在这些版本的 Windows 中，某些驱动程序可以实现自定义电源控制的组件，但这些控件通常将复杂性添加到驱动程序，并可能是设备控制组件电源设置，才可行。

从 Windows 8 开始，PoFx 添加了对组件级别电源管理支持。 这使驱动程序以支持一定数量的组件的电源状态、 F0，F1，等，其中 F0 是完全开启状态。 所有组件都支持 F0 状态。 设备中的组件的电源策略所有者 (PPO) 的驱动程序负责定义的任何其他、 低 Fx 电源状态可能具有一个组件。 （通常情况下，设备功能驱动程序是 PPO。）此驱动程序确定的每个分量的低功率 Fx 状态数和每个 Fx 状态的属性。 此驱动程序定义的 Fx 状态可能在同一设备中不同组件之间。

PoFx 提供设备驱动程序接口 (DDI) 驱动程序可以通过它提供有关设备中的组件的状态和功能的信息。 此信息包括每个组件的当前活动级别更改到另一个电源状态和组件从低功耗状态中唤醒时，设备的客户端可以容忍的滞后时间量由组件所需的时间. 此外，PoFx 获取有关该组件所属的强大功能和时钟域的系统级信息。 （特定电源域中的设备共享公共电源导轨; 特定时钟域中的设备共享常见的时钟信号。）

根据此信息，PoFx 使时组件应进入低功耗状态和要输入哪些低功耗状态做出明智的决策。 决策过程涉及到从其他组件和其他设备的信息，并将考虑设备和各种电源和时钟域中的组件之间的依赖关系。

## <a name="introduction-to-the-pofx-api-for-component-level-power-management"></a>用于组件级电源管理简介 PoFX API


若要注册设备以便由 PoFx，驱动程序调用[ **PoFxRegisterDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregisterdevice)例程。 驱动程序通过此例程[ **PO\_FX\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_device_v1)结构，其中，在其他数据之间包含的数组[ **PO\_FX\_组件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_v1)结构。 此数组中的每个元素说明设备中的组件的 Fx 电源状态和每个 Fx 状态的属性。 （最小值，不支持组件级别电源管理的组件实现仅 F0 状态。）某个特定组件中的特定 Fx 电源状态的属性的说明通过[ **PO\_FX\_组件\_空闲\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_idle_state)结构，其中包含以下值：

-   过渡延迟，这是在此状态下 Fx 对 F0 （完全启用） 状态进行转换所需的时间。
-   驻留需求，即一个组件必须在这种 Fx 状态以使转换到状态值得花费的时间。
-   名义上电源，就是力量，以供此 Fx 状态中的组件。

PoFx 使用此信息 （以及其他系统范围内输入和依赖项） 做出明智决策的 Fx 电源状态组件应采用在任何特定的时间。 PoFx 必须平衡两个相互竞争的目标。 首先，处于空闲状态的组件应配置为作为尽可能少的功率消耗。 第二，必须准备一个组件将从切换低功耗 Fx 状态到 F0 足够快的速度来维护始终处于打开和始终连接的设备的外观。

仅当设备处于 D0 （完全启用） 电源状态时，可以执行组件级别电源管理。 当设备 D1 （几乎启用）、 D2 （几乎关闭） 或 D3 电源状态中，该设备不可访问。 D0 状态设备时，主动使用该驱动程序的组件都需要以维持在 F0 状态。 空闲组件可能可以切换到低功耗 Fx 状态，以降低功率消耗。

当设备处于 D0 电源状态时，该驱动程序都遵循简单协议以启用组件级别电源管理。 当驱动程序需要访问一个组件时，该驱动程序调用[ **PoFxActivateComponent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxactivatecomponent)例程组件请求访问。 此调用发生时，组件是在低功耗 Fx 状态中，PoFx 启动到 F0 状态的转换，这一转换完成时通知该驱动程序。 该驱动程序可以访问该组件。 当驱动程序不再需要时访问组件时，该驱动程序调用[ **PoFxIdleComponent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxidlecomponent)例程，以通知 PoFx。 此调用的响应，PoFx 到低功耗 Fx 状态可能可以切换该组件。

可访问的组件处于*活动条件*。 无法访问的组件处于*空闲条件*。 若要跟踪的设备中的组件可访问性，PoFx 维护每个组件上的激活引用计数。 一个**PoFxActivateComponent**调用递增 1，在指定组件的计数和一个**PoFxIdleComponent**逐个调用递减计数。

如果**PoFxActivateComponent**调用增加在 0 到 1 计数，PoFx 启动空闲条件从转换到活动的条件，并在这种转换完成时通知驱动程序。 如果**PoFxActivateComponent**组件已处于活动状态、 组件处于活动状态的条件和驱动程序收到任何通知时发生。

如果**PoFxIdleComponent**调用递减计数从 1 到零，PoFx 启动活动条件从转换到空闲的条件，而这一转换完成时通知该驱动程序。 如果**PoFxIdleComponent**调用递减计数，但计数保持非零值、 组件处于活动状态的条件和驱动程序收到任何通知。

激活引用计数方便地处理相同的驱动程序中的两个或多个代码路径可能需要同时访问同一组件中设备的情况。 通过维护此计数，PoFx 使驱动程序独立维护而不需要的驱动程序进行集中管理组件的访问权访问该组件的各个部分。

组件的活动/空闲条件是用于确定组件是否可访问的驱动程序的唯一可靠方法。 正处于 F0 电源状态，但处于空闲状态的组件可能要切换到低功耗 Fx 状态。

在 F0 状态始终是处于活动状态的组件。 该组件不能离开 F0，直到进入空闲状态的条件。 处于空闲状态的组件可能是 F0 中或低功耗 Fx 状态中。 如果组件是低功耗 Fx 中运行时**PoFxActivateComponent**调用启动的空闲条件从转换到活动的条件、 PoFx 必须首先组件之前切换到 F0 组件可以输入活动条件。

## <a name="related-topics"></a>相关主题

[设备电源管理的参考](device-power-management-reference.md)  
