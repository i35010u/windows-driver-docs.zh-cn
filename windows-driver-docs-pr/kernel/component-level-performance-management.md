---
title: 组件级性能状态管理
description: 从 Windows 10 开始，电源管理框架（PoFx）允许驱动程序为设备中的单个组件定义一组或多组单独的可调整性能状态。
ms.assetid: D5341D6D-7C71-43CB-9C70-7E939B32C33F
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 01b7a194aee6e8c97cfd4462dc5ddaa762b3b42a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837066"
---
# <a name="component-level-performance-state-management"></a>组件级性能状态管理


从 Windows 10 开始，电源管理框架（PoFx）允许驱动程序为设备中的单个组件定义一组或多组单独的可调整性能状态。 驱动程序可以使用性能状态来限制组件的工作负荷，以提供刚好足够的性能来满足工作负荷的当前需求。

## <a name="overview-of-performance-states"></a>性能状态概述


在 Windows 8 和 Windows 8.1 中，PoFx 提供空闲状态（F 状态），通过在输入特定 F 状态时使用电源和时钟导轨来实现组件级节能。 此模型可节省组件处于空闲状态时的功能（非 F0），但不提供任何在组件处于活动状态时用于优化电源使用或平衡其性能的机制。 即使组件处于活动状态（在 F0 中）并为请求提供服务，它也可能不需要设备的完整性能。 例如，图形卡可能只需要更新闪烁的光标，这可能不需要完全性能。

可变性能状态通过允许驱动程序限制设备的组件来为当前需要提供足够的性能，来解决此问题。 在 Windows 8 和 Windows 8.1 中，如果组件支持性能状态，则每个驱动程序都必须实现驱动程序内部的专有性能状态选择算法，并且如果需要，还应在专有方式. PEP 是一个软件组件，用于执行特定于芯片（SoC）模块上特定产品系列的电源管理任务。 特定于驱动程序的专有性能状态解决方案具有与 PEP 紧密耦合的缺点，无法轻松进行调试。

从 Windows 10 开始，PoFx 提供了一个 API 来实现性能状态管理。 此 API 有两个主要目标：

-   它为设备驱动程序提供了一种标准方法，通知 PEP 有关性能状态更改的信息，以便 PEP 采取适当的措施。
-   它为驱动程序提供了一种标准方法，用于在 Windows 性能分析器（WPA）中通知操作系统的日志记录和分析性能状态变化，无需每个驱动程序都有自定义插件。

## <a name="introduction-to-the-pofx-api-for-component-level-performance-states"></a>组件级性能状态的 PoFX API 简介


PoFx 使设备可以为每个组件定义以下类型的性能状态：

-   以频率（以 Hz 为单位）、带宽（以每秒位数为单位）或不透明索引号单位表示的离散状态数。
-   最小值和最大值之间的连续状态分布。

性能状态按集组织，并以每个组件为基础进行注册。 集内的性能状态必须以单调增长。 大多数驱动程序都应该为每个组件定义一组性能状态。 例如，驱动程序可能定义一组性能状态以控制组件的时钟频率。 但是，某些驱动程序可能需要定义多个性能状态集来控制组件的多个性能状态。 例如，驱动程序可能会定义两个性能状态集来控制时钟频率和总线带宽。

若要通过 PoFx 注册性能状态管理的设备组件，驱动程序应遵循以下常规步骤：

1.  驱动程序将注册由 PoFx 管理的设备组件。 有关详细信息，请参阅[组件级电源管理](component-level-power-management.md)。

2.  驱动程序通过调用[**PoFxRegisterComponentPerfStates**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregistercomponentperfstates)来注册对性能状态的支持。 作为注册调用的一部分，驱动程序可以自行定义给定组件的性能状态，也可以将其推迟到平台扩展插件（PEP）来定义它们。

    设备驱动程序或 PEP 必须保留性能状态的知识，包括每个组件的性能状态集的数量、性能状态的类型（离散或基于范围）以及实际性能的值和计数的详细信息自治区. 如果 PEP 不支持性能状态，则驱动程序仍可以注册性能状态支持和 PoFx，并在 Windows 性能分析器（WPA）中通知日志记录和分析的性能状态更改。

    不管哪种情况，在[**PoFxRegisterComponentPerfStates**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregistercomponentperfstates)成功完成后，该驱动程序都有一个[**PO\_FX\_组件\_PERF\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_perf_info)结构，其中包含已注册的性能状态集。

3.  当驱动程序决定组件应更改性能状态时，它将调用[**PoFxIssueComponentPerfStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechange)或[**PoFxIssueComponentPerfStateChangeMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)。 当性能状态更改完成时，PoFx 将调用驱动程序提供的[**ComponentPerfStateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_perf_state_callback)例程。

4.  [**ComponentPerfStateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_perf_state_callback)例程通知此驱动程序是否成功或拒绝了性能状态更改。 如果 PEP 成功进行了更改，则驱动程序将执行从其角度更改性能状态所需的任何工作。 如果 PEP 拒绝了更改，驱动程序可能会选择不执行任何操作，或者使用相同或备用性能状态再次重试请求。

## <a name="related-topics"></a>相关主题
[设备电源管理参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  



