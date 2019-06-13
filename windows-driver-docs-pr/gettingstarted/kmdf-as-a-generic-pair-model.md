---
title: 作为通用驱动程序对模型的 KMDF
description: 在本主题中，我们介绍内核模式驱动程序框架可以作为通用驱动程序对模型来查看的这一思想。
ms.assetid: C05E3017-0F1A-49D7-8EAD-0DC44351A39A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fb7c4c0d0c87db0ae03d092239b6ed0182098eb
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63371287"
---
# <a name="kmdf-as-a-generic-driver-pair-model"></a>作为通用驱动程序对模型的 KMDF


在本主题中，我们介绍内核模式驱动程序框架可以作为通用驱动程序对模型来查看的这一思想。 在阅读本主题之前，应了解[微型驱动程序和驱动程序对](minidrivers-and-driver-pairs.md)中介绍的思想。

在过去的数年里，Microsoft 已创建多个使用此范例的技术特定的驱动程序模型：

-   驱动程序分为两部分：一部分进行通用处理，另一部分进行特定设备特有的处理。
-   通用部分（称为“框架”）由 Microsoft 编写。
-   特定部分（称为“KMDF 驱动程序”）可由 Microsoft 或独立硬件供应商编写。

![作为通用驱动程序对的 KMDF 图示](images/kmdfdriverpair.png)

驱动程序对的“框架”部分执行通用于各种驱动程序的常规任务。 例如，“框架”可以处理 I/O 请求队列、线程同步以及很大一部分的电源管理任务。

“框架”拥有 KMDF 驱动程序的调度表，因此当某人将 I/O 请求数据包 (IRP) 发送到（KMDF 驱动程序，框架）对时，IRP 会转到“框架”。 如果“框架”可以自行处理 IRP，则不会涉及到 KMDF 驱动程序。 如果“框架”自身无法处理 IRP，则它会通过调用 KMDF 驱动程序实现的事件处理程序来获取帮助。 下面是可以由 KMDF 驱动程序实现的事件处理程序的一些示例。

-   EvtDevicePrepareHardware
-   EvtIoRead
-   EvtIoDeviceControl
-   EvtInterruptIsr
-   EvtInterruptDpc
-   EvtDevicePnpStateChange

例如，USB 2.0 主控制器驱动程序有一个名为 usbehci.sys 的特定部分和一个名为 usbport.sys 的通用部分。 Usbehci.sys（称为 USB 2.0 微型端口驱动程序）的代码特定于 USB 2.0 主控制器。 Usbport.sys（称为 USB 端口驱动程序）的通用代码适用于 USB 2.0 和 USB 1.0。 驱动程序对（usbehci.sys，usbport.sys）合并形成用于 USB 2.0 主控制器的单个 WDM 驱动程序。

在不同的设备技术中，（特定，通用）驱动程序对有不同的名称。 大部分设备特定的驱动程序都有前缀“微型”  。 常规驱动程序通常称为“端口”或“类驱动程序”。 下面是（特定，通用）对的一些示例：

-   （屏幕微型端口驱动程序，屏幕端口驱动程序）
-   （USB 微型端口驱动程序，USB 端口驱动程序）
-   （电池微型类驱动程序，电池类驱动程序）
-   （HID 微型驱动程序，HID 类驱动程序）
-   （存储微型端口驱动程序，存储端口驱动程序）

随着开发了越来越多的驱动程序对模型，跟踪编写驱动程序的所有不同方式就变得很困难。 每个模型都有其自己的接口用于在设备特定驱动程序与通用驱动程序之间进行通信。 为一个设备技术（例如，音频）开发驱动程序所需的知识主体可以与为其他设备技术（例如，存储）开发驱动程序所需的知识主体完全不同。

随着时间的推移，开发者已意识到最好将单个统一模型用于内核模式驱动程序对。 内核模式驱动程序框架 (KMDF)（首先在 Windows Vista 中提供）满足该需要。 基于 KMDF 的驱动程序使用的范例类似于多个技术特定驱动程序对模型。

-   驱动程序分为两部分：一部分进行通用处理，另一部分进行特定设备特有的处理。
-   通用部分（由 Microsoft 编写）称为框架。
-   特定部分（由 Microsoft 或独立的硬件供应商编写）称为 KMDF 驱动程序。

USB 3.0 主控制器驱动程序为基于 KMDF 的驱动程序示例。 在此示例中，驱动程序对中的两个驱动程序都由 Microsoft 编写。 通用驱动程序为“框架”，设备特定的驱动程序为 USB 3.0 主控制器驱动程序。 此图说明了用于 USB 3.0 主控制器的设备节点和设备堆栈。

![USB 3 主控制器的设备堆栈图](images/kmdfaspair01.png)

在该图中，Usbxhci.sys 为 USB 3.0 主控制器驱动程序。 它使用 Wdf01000.sys（即“框架”）进行配对。 （usbxhci.sys，wdf01000.sys）对形成单个 WDM 驱动程序，该驱动程序用作 USB 3.0 主控制器的函数驱动程序。 注意，驱动程序对占用了设备堆栈中的一层并且用单个设备对象表示。 表示（usbxhci.sys，wdf01000.sys）对的单个设备对象为用于 USB 3.0 主控制器的功能设备对象 (FDO)。

在（KMDF 驱动程序，框架）对中，框架处理各种内核模式驱动程序共同的任务。 例如，框架可以处理 I/O 请求排队、线程同步、大部分即插即用任务以及大部分电源管理任务。 KMDF 驱动程序处理需要与特定设备交互的任务。 KMDF 驱动程序通过注册“框架”根据需要调用的事件处理程序来参与处理请求。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[微型驱动程序和驱动程序对](minidrivers-and-driver-pairs.md)

[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

 

 






