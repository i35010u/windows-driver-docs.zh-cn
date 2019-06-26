---
title: 组件级性能状态管理
description: 电源管理框架 (PoFx) 从 Windows 10 开始，使驱动程序来定义一个或多个集的设备中的单个组件可单独调整性能状态。
ms.assetid: D5341D6D-7C71-43CB-9C70-7E939B32C33F
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9df895638ec56c6c814fe2586e7a55df24bc5a56
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377219"
---
# <a name="component-level-performance-state-management"></a>组件级性能状态管理


电源管理框架 (PoFx) 从 Windows 10 开始，使驱动程序来定义一个或多个集的设备中的单个组件可单独调整性能状态。 驱动程序可以使用性能状态来限制组件的工作负荷，以提供刚好足够的性能来满足工作负荷的当前需求。

## <a name="overview-of-performance-states"></a>性能状态概述


在 Windows 8 和 Windows 8.1，PoFx 空闲状态 （F 状态） 对进行组件级别能源节约电源和时钟 rail 访问控制时，将进入特定的 F 状态。 此模型组件处于空闲状态 (非-F0)，但不优化电源使用情况或根据性能需求进行平衡，该组件处于活动状态时提供的任何机制时节省电能。 即使一个组件中处于活动状态 （F0) 和为请求提供服务，它可能不需要完全性能的设备。 例如，图形卡可能需要仅更新一个闪烁的光标，这可能不需要完整的性能。

变量的性能状态的驱动程序，以限制设备的组件，可提供其当前需求的足够性能，从而解决此问题。 在 Windows 8 和 Windows 8.1 中，如果组件支持性能状态每个驱动程序必须实现一种专有的性能状态选择算法内部的驱动程序，并根据需要通知平台中的扩展插件 (PEP) 一种专有方式。 PEP 是执行特定于特定产品系列的处理器或系统芯片 (SoC) 模块上的电源管理任务的软件组件。 特定于驱动程序的专有性能状态解决方案具有使用 PEP，紧密耦合的缺点，并不能轻松地调试。

从 Windows 10 开始，性能状态管理 PoFx 提供一个 API。 此 API 有两个主要目标：

-   它提供的设备驱动程序，以便 PEP 可能采取适当措施通知 PEP 的性能状态更改的标准方法。
-   它提供了驱动程序而无需自定义插件的每个驱动程序通知的日志记录和分析中 Windows Performance Analyzer (WPA) 的性能状态更改的操作系统的标准方法。

## <a name="introduction-to-the-pofx-api-for-component-level-performance-states"></a>组件级性能状态 PoFX API 简介


PoFx 启用定义以下类型的每个组件的性能状态的设备：

-   离散的单位的频率 （以 Hz 为单位）、 带宽 （以每秒位数为单位） 或不透明的索引号的状态数。
-   在最小和最大值之间的状态的连续分布。

性能状态组织成集，并且在每个组件的基础上注册。 必须单调增加一组内的性能状态。 大多数驱动程序需要定义一组每个组件的性能状态。 例如，驱动程序可能会定义一组要控制的组件的时钟频率的性能状态。 但是，某些驱动程序可能需要定义设置以控制的一个组件的性能状态的多个维度的多个性能状态。 例如，驱动程序可能会定义两个集的性能状态，以控制的时钟频率和总线带宽。

若要注册的 PoFx 性能状态管理的设备组件，驱动程序，请遵循以下常规步骤：

1.  该驱动程序将注册要由 PoFx 管理的设备组件。 有关详细信息，请参阅[组件级别电源管理](component-level-power-management.md)。

2.  该驱动程序通过调用注册为支持性能状态[ **PoFxRegisterComponentPerfStates**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregistercomponentperfstates)。 作为注册调用的一部分，驱动程序可以自行定义给定的组件的性能状态或推迟到平台扩展插件 (PEP) 改为定义它们。

    设备驱动程序或 PEP 必须保存性能状态，包括每个组件的性能状态 （离散或基于范围的） 的类型和值的详细信息和计数的实际性能的性能状态集的数量的知识状态。 如果 PEP 不支持性能状态，驱动程序可能仍注册，以便与 PoFx 性能状态支持和通知的日志记录和分析 Windows Performance Analyzer (WPA) 中的性能状态更改的操作系统。

    在任一情况下，成功完成后[ **PoFxRegisterComponentPerfStates**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregistercomponentperfstates)，该驱动程序有[ **PO\_FX\_组件\_PERF\_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_perf_info)结构，其中包含已注册的性能状态集。

3.  当驱动程序决定一个组件，应更改性能状态时，它将调用[ **PoFxIssueComponentPerfStateChange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechange)或[ **PoFxIssueComponentPerfStateChangeMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)。 PoFx 调用驱动程序提供[ **ComponentPerfStateCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_perf_state_callback)例程性能状态更改完成后。

4.  该驱动程序将得到通知，通过[ **ComponentPerfStateCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_perf_state_callback)例程是否 PEP 成功或拒绝的性能状态更改。 如果 PEP 成功更改，该驱动程序然后执行它需要从其角度来看有关更改的性能状态的任何工作。 如果 PEP 拒绝更改，该驱动程序可以选择不执行任何操作，或重试该请求再次与相同或一个备用的性能状态。

## <a name="related-topics"></a>相关主题
[设备电源管理的参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  



