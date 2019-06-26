---
title: 对 I/O 请求与组件电源状态进行协调
description: 对 I/O 请求与组件电源状态进行协调
ms.assetid: CF74B946-BF62-481A-B8AA-DD106DDB94CA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 758124bb7fea4b017a0da143d59f4327b26ad783
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382412"
---
# <a name="coordinating-io-requests-with-component-power-state"></a>对 I/O 请求与组件电源状态进行协调


\[仅适用于 KMDF\]

多个组件设备的 KMDF 驱动程序必须仅将请求发送到处于活动状态的组件。 通常情况下，该驱动程序将 I/O 队列分配给组件或组件的设置。

首先考虑分配给单个组件的队列。 当该组件将变为活动状态并停止队列，组件进入空闲状态时，驱动程序将启动该队列。 在这种情况下，当 KMDF 调用队列时请求处理程序，设备处于其完全开启 (D0) 状态，并且所需的组件处于活动状态。 请求处理程序可以安全地访问组件的硬件。

相同的概念适用于队列分配给一组组件。 在这种情况下，该驱动程序启动该队列中的所有组件集处于活动状态。 组件的任何一个进入空闲状态时，驱动程序将停止队列。

本主题介绍如何用于多个组件设备的 KMDF 驱动程序可能涉及多个请求需要的类型的不同组件组合的情况下实现这种支持。

## <a name="example"></a>示例


对于每个驱动程序支持的请求类型，确定所需的组件。 例如，考虑具有三个组件的设备：0、 1 和 2，为其驱动程序收到的请求的三种类型：A、 B 和 c。请求的组件要求如下所示：

| 请求类型 | 所需组件 |
|--------------|-------------------|
| A            | 0,2               |
| B            | 1                 |
| C            | 0,1,2             |

 

在此示例中，有三个截然不同的组件，分别为每个请求类型。
驱动程序提供一个默认、 电源管理设备的 I/O 队列，以及一个将对应于每个组的组件其他电源管理队列。 在上面的示例中，该驱动程序创建一个主队列和三个辅助队列，一个对应于每个组件集。 在下图显示了此队列配置：

![队列实现多个组件设备](images/multicompqueues.png)

该驱动程序维护每个组件集的位掩码。 位掩码中的每个位表示的一个组件的活动/空闲状态。 如果设置了位，该组件处于活动状态。 如果清除了位，则该组件处于空闲状态。

当请求到达时，[请求处理程序](request-handlers.md)顶级队列决定哪些组件需要请求，并调用[ **PoFxActivateComponent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxactivatecomponent)为每个。 请求处理程序然后将其转发给辅助的 I/O 队列对应于该组件集。

电源管理框架 (PoFx) 组件将变为活动状态，当调用的驱动程序[ *ComponentActiveConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback)例程。 在此回调中，驱动程序设置对应于指定的组件，在每个表示该组件的位掩码中的位。 如果设置了所有给定的位掩码中的位，对应的一组中的组件的所有处于活动状态。 对于当前正在执行完全每个组件集，该驱动程序调用[ **WdfIoQueueStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestart)启动相应的辅助 I/O 队列。

例如，考虑上述假设的设备。 假设该组件 0 处于活动状态，而 1 和 2 的组件都处于空闲状态。 PoFx 组件 2 将变为活动状态，当调用该组件[ *ComponentActiveConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_active_condition_callback)例程。 请求类型 A 和 C 使用组件 2，因此驱动程序操作这些两个请求类型的位屏蔽。 由于现在设置为请求类型 a 的位掩码中的所有位，因此驱动程序启动的队列的请求类型 a。但是，并非所有的位将设置为请求类型 C （组件 1 是仍然空闲）。 该驱动程序不会启动的队列的请求类型 c。

当启动辅助的 I/O 队列时，框架将开始提供存储在队列中的请求。 在中[请求处理程序](request-handlers.md)辅助的 I/O 队列，驱动程序可以安全地处理请求，因为该组件处于活动状态，并且 power 引用已在组件上的每个请求。

当驱动程序完成处理的请求时，它将调用[ **PoFxIdleComponent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxidlecomponent)为每个请求使用的，，然后完成请求的组件。 有没有更多的请求使用的组件，电源框架将调用的驱动程序[ *ComponentIdleConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback)例程。

在此回调中，驱动程序将清除每个表示该组件的位掩码中的指定组件所对应的位。 如果给定的位掩码表示该组件中的相应设置为过渡到空闲条件的第一个，该驱动程序会调用[ **WdfIoQueueStop** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuestop)停止相应的辅助 I/O队列。 通过此操作，该驱动程序可确保该队列不会除非所有相应的组中的组件处于活动状态，否则调度请求。

再次考虑上面的示例。 假设所有组件都处于活动状态，因此启动的所有队列。 当组件 1 变为空闲状态时，调用 PoFx [ *ComponentIdleConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback)例程组件 1。 在此回调中，驱动程序操作请求类型 B 和 C 的位的屏蔽，因为它们使用组件 1。 由于组件 1 变为空闲状态的这两种请求类型的第一个组件，驱动程序将停止的队列的请求类型 B 和 c。

假设，在此情况下，组件 0 进入空闲状态。 在中[ *ComponentIdleConditionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_idle_condition_callback)组件 0，驱动程序操作的请求类型 A 和 c。 位掩码由于组件 0 是第一个组件变为空闲状态的请求类型 A （2 组件仍处于活动状态），驱动程序将停止的队列的请求类型 A.但是，为请求类型 C，组件 0 不是进入空闲状态的第一个组件。 该驱动程序不会停止的队列的请求类型 C （因此之前那样）。

若要使用此示例中所述的技术，该驱动程序还必须注册[ *EvtIoCanceledOnQueue* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)其辅助队列的每个回调函数。 如果要在辅助队列中取消请求，该驱动程序可以使用此回调以调用[ **PoFxIdleComponent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxidlecomponent)每个对应的组件。 执行请求处理程序时调用它采取 power 引用的是版本[ **PoFxActivateComponent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxactivatecomponent)之前将请求转发到辅助队列。

 

 





