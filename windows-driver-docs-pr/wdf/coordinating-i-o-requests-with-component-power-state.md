---
title: 对 I/O 请求与组件电源状态进行协调
description: 对 I/O 请求与组件电源状态进行协调
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1c94e718321e6829b371be3896fb0543b5ef250
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829077"
---
# <a name="coordinating-io-requests-with-component-power-state"></a>对 I/O 请求与组件电源状态进行协调


\[仅适用于 KMDF\]

多组件设备的 KMDF 驱动程序必须仅向处于活动状态的组件发送请求。 通常，驱动程序将 i/o 队列分配给组件或组件集。

首先考虑分配给单个组件的队列。 当组件激活时，驱动程序将启动队列，并在组件处于空闲状态时停止队列。 因此，当 KMDF 调用队列的请求处理程序时，设备处于完全打开状态 (D0) 状态，并且所需的组件处于活动状态。 请求处理程序可以安全地访问组件硬件。

相同的概念适用于分配给一组组件的队列。 在这种情况下，当集中的所有组件都处于活动状态时，驱动程序将启动队列。 当任何一个组件处于空闲状态时，驱动程序将停止队列。

本主题介绍多组件设备的 KMDF 驱动程序如何在涉及多个需要不同组件组合的请求类型的情况下实现此类支持。

## <a name="example"></a>示例


对于该驱动程序支持的每个请求类型，确定所需的组件。 例如，假设有三个组件的设备：0、1和2，驱动程序将收到三种类型的请求： A、B 和 C。请求的组件要求如下所示：

| 请求类型 | 所需组件 |
|--------------|-------------------|
| A            | 0、2               |
| B            | 1                 |
| C            | 0、1、2             |

 

在此示例中，有三个不同的组件集，分别用于每个请求类型。
驱动程序为设备提供了一个默认的电源托管 i/o 队列，以及一个与每组组件相对应的其他电源管理队列。 在上面的示例中，驱动程序将创建一个主队列和三个辅助队列，每个都对应于每个组件集。 下图显示了此队列配置：

![多个组件设备的队列实现](images/multicompqueues.png)

驱动程序为每个组件集维护一个位掩码。 位掩码中的每个位代表一个组件的活动/空闲状态。 如果设置了位，则组件处于活动状态。 如果清除该位，该组件将处于空闲状态。

请求到达时，顶级队列的 [请求处理程序](request-handlers.md) 将确定请求需要的组件，并为每个组件调用 [**PoFxActivateComponent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxactivatecomponent) 。 然后，请求处理程序将请求转发到对应于该组件集的辅助 i/o 队列。

当组件变为活动状态时，电源管理框架 (PoFx) 调用驱动程序的 [*ComponentActiveConditionCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback) 例程。 在此回调中，驱动程序会在表示组件的每个位掩码中设置对应于指定组件的位。 如果设置了给定位掩码中的所有位，则相应集中的所有组件都将处于活动状态。 对于完全活动的每个组件集，驱动程序将调用 [**WdfIoQueueStart**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestart) 来启动相应的辅助 i/o 队列。

例如，假设设备上有假设的设备。 假设组件0处于活动状态，而组件1和2处于空闲状态。 当组件2变为活动状态时，PoFx 将调用该组件的 [*ComponentActiveConditionCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_active_condition_callback) 例程。 请求类型 A 和 C 使用组件2，因此驱动程序将为这两种请求类型处理位掩码。 由于请求类型 A 的位掩码中的所有位现在均已设置，因此驱动程序将为请求类型 A 启动队列。但是，并不是所有位都为请求类型 C 设置 (组件1仍处于空闲) 。 驱动程序未启动请求类型 C 的队列。

启动辅助 i/o 队列时，框架会开始传递存储在队列中的请求。 在辅助 i/o 队列的 [请求处理程序](request-handlers.md) 中，驱动程序可以安全地处理请求，因为该组件处于活动状态，并且已对每个请求的组件执行了电源引用。

当驱动程序完成请求处理后，它将为该请求使用的每个组件调用 [**PoFxIdleComponent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxidlecomponent) ，然后完成该请求。 当没有更多的请求使用组件时，power framework 会调用驱动程序的 [*ComponentIdleConditionCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback) 例程。

在此回调中，驱动程序将清除与指定组件相对应的位，其中每个位掩码表示该组件。 如果给定的位掩码指示组件是要过渡到空闲状态的相应集合中的第一个位掩码，则驱动程序将调用 [**WdfIoQueueStop**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop) 来停止相应的辅助 i/o 队列。 通过此操作，驱动程序可确保队列不会调度请求，除非相应集中的所有组件都处于活动状态。

请再次考虑上述示例。 假设所有组件都处于活动状态，因此所有队列均已启动。 当组件1处于空闲状态时，PoFx 将为组件1调用 [*ComponentIdleConditionCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback) 例程。 在此回调中，驱动程序为请求类型 B 和 C 操作了位掩码，因为它们使用组件1。 由于组件1是每个请求类型都处于空闲状态的第一个组件，因此驱动程序将停止请求类型 B 和 C 的队列。

假设此时组件0变为空闲状态。 在 [*ComponentIdleConditionCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_idle_condition_callback) for component 0 中，驱动程序为请求类型 A 和 C 操作位掩码。由于组件0是请求类型 (第2部分仍) 处于活动状态的第一个组件，因此，驱动程序将停止请求类型 A 的队列。但是，对于请求类型 C，组件0不是要进入空闲状态的第一个组件。 对于请求类型 C，驱动程序不会停止队列 () 。

若要使用本示例中所述的方法，驱动程序还必须为其每个辅助队列注册一个 [*EvtIoCanceledOnQueue*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue) 回调函数。 如果请求在辅助队列中被取消，则驱动程序可以使用此回调为每个相应的组件调用 [**PoFxIdleComponent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxidlecomponent) 。 这样做会释放请求处理程序在将请求转发到辅助队列之前调用 [**PoFxActivateComponent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxactivatecomponent) 时所用的 power reference。

 

