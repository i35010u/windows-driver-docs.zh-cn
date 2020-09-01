---
title: 组件级电源管理
description: 从 Windows 8 开始，电源管理框架 (PoFx) 使驱动程序能够管理设备中单个组件的电源状态。 组件级电源管理与设备级电源管理并行存在。
ms.assetid: 77866143-FB10-4623-9923-368B23808715
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3f5a1d7c1d7b8dac25c578775d5078676aaa4da4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189829"
---
# <a name="component-level-power-management"></a>组件级电源管理


从 Windows 8 开始，电源管理框架 (PoFx) 使驱动程序能够管理设备中单个组件的电源状态。 组件级电源管理与设备级电源管理并行存在。

## <a name="overview-of-component-level-power-management"></a>组件级电源管理概述


Windows 7 和更早版本的操作系统仅为设备级别电源管理提供支持，使驱动程序能够在设备中支持 D 状态。 高级配置和电源接口 (ACPI) 规范定义 [设备电源状态](device-power-states.md) D0 (完全通过 D3) 完全关闭 (并定义 [系统电源状态](system-power-states.md) S0) 完全按 (到 S5) 完全关闭 (。 这些版本的 Windows 不提供单独管理提供给设备中各个组件的电源的机制。 在这些版本的 Windows 中，某些驱动程序可以实现组件的自定义电源控制，但这些控制通常增加了驱动程序的复杂性，并且仅当组件电源设置在设备内受控时才可行。

从 Windows 8 开始，PoFx 添加了对组件级电源管理的支持。 这使得驱动程序能够支持一定数量的组件电源状态、F0、F1 等，其中 F0 是完全打开状态。 所有组件都支持 F0 状态。 作为设备中组件 (PPO) 的驱动程序的驱动程序负责定义组件可能具有的任何其他低功率 Fx 电源状态。  (通常情况下，设备的函数驱动程序是 PPO。 ) 此驱动程序确定每个组件的低功率 Fx 状态数和每个 Fx 状态的属性数。 此驱动程序定义的 Fx 状态可能因组件而异。

PoFx 提供 (DDI) 的设备驱动程序接口，通过该接口，驱动程序可以提供有关设备中组件的状态和功能信息。 此信息包括每个组件的当前活动级别、组件从一个电源状态更改为另一个电源状态所需的时间，以及从低功耗状态唤醒组件时，设备的客户端可以承受的延迟量。 此外，PoFx 还获得系统范围内组件所属的电源和时钟域的信息。  (特定 power 域中的设备共享通用电源线;特定时钟域中的设备共享常见时钟信号。 ) 

基于此信息，PoFx 可以明智地决定组件何时进入低功耗状态以及进入哪种低功耗状态。 决策过程涉及其他组件和其他设备中的信息，并考虑各种电源和时钟域中设备和组件之间的依赖关系。

## <a name="introduction-to-the-pofx-api-for-component-level-power-management"></a>用于组件级电源管理的 PoFx API 简介


若要注册由 PoFx 管理的设备，驱动程序将调用 [**PoFxRegisterDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregisterdevice) 例程。 该驱动程序将此例程传递到 [**po \_ fx \_ 设备**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_device_v1) 结构，其中其他数据包含 [**po \_ fx \_ 组件**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_v1) 结构的数组。 此数组中的每个元素都描述设备中组件的 Fx 电源状态以及每个 Fx 状态的属性。  (最少，组件不支持组件级电源管理仅实现了 F0 状态。 ) 特定组件中特定 Fx 电源状态的属性的说明，请参阅 [**PO \_ Fx \_ 组件 \_ 空闲 \_ 状态**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_idle_state) 结构，其中包含以下值：

-   转换滞后时间，这是从该 Fx 状态转换到 F0 (完全) 状态所需的时间。
-   驻留要求，这是组件必须在此 Fx 状态中花费的时间，以将转换为值得的状态。
-   额定功率，这是组件在此 Fx 状态中使用的功率。

除了使用其他系统范围的输入和依赖项) ，PoFx 还 (使用此信息，以便明智地决定组件应处于哪个 Fx 电源状态。 PoFx 必须平衡两个竞争性目标。 首先，应将处于空闲状态的组件配置为使用尽可能少的电量。 其次，必须准备好一个组件，使其能够从低功耗 Fx 状态切换到 F0，以便保持始终开机和始终连接的设备的外观。

仅当设备处于 D0 (完全打开) 电源状态时，才能执行组件级电源管理。 如果设备处于 D1 (几乎在) 上，D2 (几乎关闭) 或 D3 电源状态，则设备不可访问。 如果设备处于 D0 状态，则只有驱动程序主动使用的组件需要保持 F0 状态。 空闲组件可能会切换到低功率 Fx 状态，以降低能耗。

当设备处于 D0 电源状态时，驱动程序将遵循简单的协议来启用组件级电源管理。 当驱动程序需要访问组件时，驱动程序将调用 [**PoFxActivateComponent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxactivatecomponent) 例程以请求对组件的访问。 如果此调用发生时组件处于低功耗 Fx 状态，PoFx 将启动到 F0 状态的转换，并在此转换完成时通知驱动程序。 然后，该驱动程序可以访问该组件。 当驱动程序不再需要访问组件时，驱动程序将调用 [**PoFxIdleComponent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxidlecomponent) 例程来通知 PoFx。 为了响应此调用，PoFx 可能会将组件切换为低功率 Fx 状态。

可访问的组件处于 *活动状态*。 不可访问的组件处于 *空闲状态*。 为了跟踪设备中组件的可访问性，PoFx 在每个组件上维护激活引用计数。 **PoFxActivateComponent**调用将指定组件上的计数递增一， **PoFxIdleComponent**调用会将计数递减1。

如果 **PoFxActivateComponent** 调用将计数从零递增到1，则 PoFx 将启动从空闲条件到活动条件的转换，并在此转换完成时通知驱动程序。 如果在组件已经处于活动状态时出现 **PoFxActivateComponent** ，该组件将保持活动状态，驱动程序不会收到通知。

如果 **PoFxIdleComponent** 调用将计数从一个减少到零，则 PoFx 将启动从活动条件到空闲状态的转换，并在此转换完成时通知驱动程序。 如果 **PoFxIdleComponent** 调用递减计数但计数保持非零，则组件将保持活动状态，并且驱动程序不会收到通知。

激活引用计数可方便地处理同一驱动程序中的两个或两个以上的代码路径需要同时访问设备中同一组件的情况。 通过维护此计数，PoFx 使驱动程序的各个部分独立维护对组件的访问，而无需驱动程序集中管理对组件的访问。

组件的活动/空闲条件是驱动程序确定是否可访问组件的唯一可靠方法。 处于 F0 电源状态但处于空闲状态的组件可能会切换为低功率 Fx 状态。

处于活动状态的组件始终处于 F0 状态。 该组件在进入空闲状态之前无法退出 F0。 处于空闲状态的组件可能处于 F0 或低能耗 Fx 状态。 如果当 **PoFxActivateComponent** 调用启动从空闲条件到活动条件的转换时，组件处于低功率 Fx 状态，则 PoFx 必须先将该组件切换到 F0，然后才能进入活动状态。

## <a name="related-topics"></a>相关主题

[设备电源管理参考](device-power-management-reference.md)