---
title: 组件级性能状态管理
description: 从 Windows 10 开始，电源管理框架 (PoFx) 使驱动程序能够为设备中的单个组件定义一组或多组单独的可调整性能状态。
ms.assetid: D5341D6D-7C71-43CB-9C70-7E939B32C33F
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fd6a625ac4967b33c711e59493ba15a4918960b1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189831"
---
# <a name="component-level-performance-state-management"></a>组件级性能状态管理


从 Windows 10 开始，电源管理框架 (PoFx) 使驱动程序能够为设备中的单个组件定义一组或多组单独的可调整性能状态。 驱动程序可以使用性能状态来限制组件的工作负荷，以提供刚好足够的性能来满足工作负荷的当前需求。

## <a name="overview-of-performance-states"></a>性能状态概述


在 Windows 8 和 Windows 8.1 中，PoFx 提供空闲状态， () F 状态，在输入特定 F 时，通过电源和时钟导轨来实现组件级节能。 当组件处于空闲状态时，此模型可节省电能 (非 F0) ，但不会提供任何机制来优化电源使用或在组件处于活动状态时对其进行平衡。 即使组件处于活动状态 (F0) 并为请求提供服务，它也可能不需要设备的完整性能。 例如，图形卡可能只需要更新闪烁的光标，这可能不需要完全性能。

可变性能状态通过允许驱动程序限制设备的组件来为当前需要提供足够的性能，来解决此问题。 在 Windows 8 和 Windows 8.1 中，如果某个组件支持性能状态，则每个驱动程序都必须实现该驱动程序内部的专有性能状态选择算法，并且如果需要，还可以通过专有方式向平台扩展插件 (PEP) 通知。 PEP 是一个软件组件，用于执行特定于芯片 (SoC) 模块上特定产品系列的电源管理任务。 特定于驱动程序的专有性能状态解决方案具有与 PEP 紧密耦合的缺点，无法轻松进行调试。

从 Windows 10 开始，PoFx 提供了一个 API 来实现性能状态管理。 此 API 有两个主要目标：

-   它为设备驱动程序提供了一种标准方法，通知 PEP 有关性能状态更改的信息，以便 PEP 采取适当的措施。
-   它为驱动程序提供了一种标准方法，通知操作系统 Windows 性能分析器中的日志记录和分析的性能状态更改 (WPA) ，无需每个驱动程序都有自定义插件。

## <a name="introduction-to-the-pofx-api-for-component-level-performance-states"></a>组件级性能状态的 PoFX API 简介


PoFx 使设备可以为每个组件定义以下类型的性能状态：

-   以赫兹) 度量 (单位的离散数量，以赫兹度量 (，以每秒位数) 度量，或不透明索引号。
-   最小值和最大值之间的连续状态分布。

性能状态按集组织，并以每个组件为基础进行注册。 集内的性能状态必须以单调增长。 大多数驱动程序都应该为每个组件定义一组性能状态。 例如，驱动程序可能定义一组性能状态以控制组件的时钟频率。 但是，某些驱动程序可能需要定义多个性能状态集来控制组件的多个性能状态。 例如，驱动程序可能会定义两个性能状态集来控制时钟频率和总线带宽。

若要通过 PoFx 注册性能状态管理的设备组件，驱动程序应遵循以下常规步骤：

1.  驱动程序将注册由 PoFx 管理的设备组件。 有关详细信息，请参阅 [组件级电源管理](component-level-power-management.md)。

2.  驱动程序通过调用 [**PoFxRegisterComponentPerfStates**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregistercomponentperfstates)来注册对性能状态的支持。 作为注册调用的一部分，驱动程序可以自行定义某个给定组件的性能状态，也可以将其推迟到平台扩展插件 (PEP) 改为定义它们。

    设备驱动程序或 PEP 必须保留性能状态的知识，包括每个组件的性能状态集的数量、 (离散或基于范围的) 的性能状态的类型，以及实际性能状态的值和计数的详细信息。 如果 PEP 不支持性能状态，则驱动程序仍可以注册性能状态支持和 PoFx，并在 Windows 性能分析器 (WPA) 中通知操作系统的性能状态更改。

    不管哪种情况，在 [**PoFxRegisterComponentPerfStates**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregistercomponentperfstates)成功完成后，驱动程序都有一个包含已注册性能状态集的 [**PO \_ FX \_ 组件 \_ PERF \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_perf_info) 结构。

3.  当驱动程序决定组件应更改性能状态时，它将调用 [**PoFxIssueComponentPerfStateChange**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechange) 或 [**PoFxIssueComponentPerfStateChangeMultiple**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)。 当性能状态更改完成时，PoFx 将调用驱动程序提供的 [**ComponentPerfStateCallback**](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_perf_state_callback) 例程。

4.  [**ComponentPerfStateCallback**](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_perf_state_callback)例程通知此驱动程序是否成功或拒绝了性能状态更改。 如果 PEP 成功进行了更改，则驱动程序将执行从其角度更改性能状态所需的任何工作。 如果 PEP 拒绝了更改，驱动程序可能会选择不执行任何操作，或者使用相同或备用性能状态再次重试请求。

## <a name="related-topics"></a>相关主题
[设备电源管理参考](/windows-hardware/drivers/ddi/index)