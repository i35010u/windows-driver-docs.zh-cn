---
description: USB 函数驱动程序通过实现 USB 选择性挂起来支持运行时空闲检测。
title: USB 驱动程序 (WDF) 中的选择性挂起
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a57f1e289de7d7299900b7a962ea2c91b0bf928
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969576"
---
# <a name="selective-suspend-in-usb-drivers-wdf"></a>USB 驱动程序 (WDF) 中的选择性挂起


USB 函数驱动程序通过实现 USB 选择性挂起来支持运行时空闲检测。 下面是有关如何在基于 Windows® Driver Foundation (WDF) 的 USB 驱动程序中实现选择性挂起的驱动程序开发人员的内容。

## <a name="about-selective-suspend"></a>关于选择性挂起


选择性挂起是指关闭并稍后恢复空闲 USB 设备的功能，而将该设备连接到的计算机保持工作状态 (S0) 。 对于节能操作（特别是在移动 Pc 上），所有 USB 设备和驱动程序都应支持选择性挂起。 在设备处于空闲状态时对其进行关闭，但系统仍处于 S0 状态，具有以下明显优势：

-   选择性挂起节省了电源。
-   选择性挂起可帮助减少环境因素，如热负载和噪音。

如果设备硬件处于空闲状态，则驱动程序应支持此功能。 在基于 Windows® Driver Foundation (WDF) 的 USB 驱动程序中，选择性挂起支持需要除了基本即插即用支持所需的额外回调。

USB 设备的每个函数驱动程序都应该实现在系统运行时挂起空闲设备的积极电源管理。 本主题介绍如何在基于 WDF 的驱动程序中实现选择性挂起。 如果你不熟悉 WDF，请参阅 Windows 驱动程序工具包 (WDK) 并通过 Windows Driver Foundation 开发驱动程序。

USB 设备通过 USB 选择性挂起支持运行时空闲检测。 选择性挂起允许将空闲设备置于挂起状态，而不会影响连接到同一集线器的其他设备，也不会影响设备中的其他功能。 当所有设备或功能都挂起时，可以关闭整个集线器或多功能设备。

从硬件角度看，选择性挂起是 USB 端口上的物理状态。 当附加到端口的所有函数都处于空闲状态时，端口可以输入选择性挂起。

为了符合 USB 规范，所有 USB 设备都必须支持选择性挂起。 当 USB 总线处于空闲状态时，设备必须能够关闭电源。 Microsoft 提供的 USB 集线器驱动程序在硬件级别实施选择性挂起。

USB 函数驱动程序应通过 WDF 为其单独的设备功能实现选择性挂起，这种情况与总线驱动程序通信，并管理挂起和恢复设备功能的设备 i/o 控制请求。 WDF 允许内核模式和用户模式驱动程序支持选择性挂起。

函数驱动程序的 USB 选择性挂起代码的详细信息取决于驱动程序在用户模式还是内核模式下运行。 请考虑以下准则：

-   尽可能使用用户模式驱动程序框架 (UMDF) 来实现 USB 驱动程序。 用户模式驱动程序损坏系统数据的可能性较低，并且比内核模式驱动程序更容易调试。
-   仅当驱动程序通过同步终结点流式传输数据，或者需要仅在内核模式下可用的其他功能或资源时，才能使用内核模式驱动程序框架 (KMDF) 。

## <a name="power-policy-ownership-io-queues-and-selective-suspend"></a>电源策略所有权、i/o 队列和选择性挂起


设备堆栈的电源策略所有者 (PPO) 是确定设备在任何给定时间应处于哪个电源状态的驱动程序。 每个设备堆栈中只有一个驱动程序可以是 PPO。 函数驱动程序通常是其设备的 PPO。

如果 USB 驱动程序支持选择性挂起并且在其设备堆栈中的 PPO 上方分层，则驱动程序不得使用电源管理的队列。 这适用于 UMDF 和 KMDF 驱动程序。 如果设备挂起时，请求到达电源管理队列，则整个设备堆栈可能会停止。

图1显示了通过其 i/o 队列向 USB 驱动程序发出的 i/o 请求的流。

![对 wdf usb 驱动程序的请求流](images/flowrequestswdfusbdriver.png)

在图中，请求到达 USB 驱动程序。 框架将请求添加到相应的队列。

如果队列不是电源管理的，则框架将根据为队列配置的驱动程序类型 (顺序、并行或手动) 向驱动程序提供请求。 然后，该驱动程序将处理该请求。

如果队列已进行电源管理且设备未挂起，则该框架会根据配置的调度类型向驱动程序呈现请求。

但是，如果设备处于挂起状态，则框架的操作将取决于驱动程序是否为设备堆栈的 PPO。 如果该驱动程序是 PPO，则该框架将与 USB 父驱动程序通信以启动设备。 恢复设备后，框架会向驱动程序提供请求。

如果该驱动程序不是 PPO，则该框架将不采取任何操作，因为只有 PPO 才能恢复该设备。 请求将保留在队列中。 如果 PPO 未收到导致其恢复设备的任何请求，则设备堆栈会停止。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="selective-suspend-in-umdf-drivers.md" data-raw-source="[Selective suspend in UMDF drivers](selective-suspend-in-umdf-drivers.md)">UMDF 驱动程序中的选择性挂起</a></p></td>
<td><p>本主题介绍了 UMDF 函数驱动程序如何支持 USB 选择性挂起。</p></td>
</tr>
<tr class="even">
<td><p><a href="selective-suspend-in-a-kmdf-function-driver.md" data-raw-source="[Selective suspend in USB KMDF function drivers](selective-suspend-in-a-kmdf-function-driver.md)">USB KMDF 功能驱动程序中的选择性挂起</a></p></td>
<td><p>本主题介绍 KMDF function 驱动程序如何支持 USB 选择性挂起。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[Windows 驱动程序框架 (WDF)](https://go.microsoft.com/fwlink/p/?linkid=53698)  
[即插即用-体系结构和驱动程序支持](https://go.microsoft.com/fwlink/p/?linkid=320985)  
[KMDF 驱动程序中的 PnP 和电源管理](https://go.microsoft.com/fwlink/p/?linkid=320986)  
[当 WDF 驱动程序可以使用电源管理的 i/o 队列时](https://go.microsoft.com/fwlink/p/?linkid=320987)  
[用 WDF 编写 USB 驱动程序](https://go.microsoft.com/fwlink/p/?linkid=320988)  
[在 USB 客户端驱动程序中实施电源管理](https://go.microsoft.com/fwlink/p/?linkid=320989)  



