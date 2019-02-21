---
Description: A USB function driver supports runtime idle detection by implementing USB selective suspend.
title: USB 驱动程序 (WDF) 中的选择性挂起
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be1759f7aee84db8120eb104e491fd3e3fbcd1d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524542"
---
# <a name="selective-suspend-in-usb-drivers-wdf"></a>USB 驱动程序 (WDF) 中的选择性挂起


USB 函数驱动程序支持运行时空闲检测通过实现 USB 选择性挂起。 下面是有关如何实现选择性的驱动程序开发人员挂起基于 Windows® Driver Foundation (WDF) 上的 USB 驱动程序中的内容。

## <a name="about-selective-suspend"></a>有关选择性挂起


选择性挂起是关闭电源和更高版本连接到在计算机仍处于工作状态 (S0) 时恢复空闲的 USB 设备的能力。 能效较高的操作 — 尤其是在移动 Pc 上 — 所有 USB 设备和驱动程序应都支持选择性挂起。 关闭时处于空闲状态，但系统保持在 S0 状态下，设备具有以下重要优势：

-   选择性挂起节省电力。
-   选择性挂起可以帮助减少环境因素，如散热负载和干扰。

如果它处于空闲状态时，你的设备硬件可以关闭电源，驱动程序应支持此功能。 选择性挂起支持在 USB 驱动程序，它基于 Windows® Driver Foundation (WDF) 需要最多几个额外回调之外基本即插即用支持所必需的。

USB 设备每个功能驱动程序应实现积极的电源管理的系统运行时将挂起的空闲状态的设备。 本主题介绍如何实现选择性挂起基于 WDF 驱动程序中。 如果您不熟悉 WDF，请参阅 Windows 驱动程序工具包 (WDK) 和使用 Windows Driver Foundation 开发驱动程序。

USB 设备支持运行时空闲检测通过 USB 选择性挂起。 选择性挂起允许空闲设备而不会影响其他设备连接到相同的中心，要将它们放入挂起状态或-在多功能设备的情况下，而不会影响设备的其他函数。 当已挂起的所有设备或函数时，可以关闭电源整个集线器或多功能设备。

从硬件角度看，选择性挂起是 USB 端口上的物理状态。 如果连接到端口的所有函数都都处于空闲状态，该端口可以输入选择性挂起。

若要符合 USB 规范，所有 USB 设备必须都支持选择性挂起。 USB 总线空闲时，设备必须能关闭电源。 Microsoft 提供的 USB 集线器的驱动程序实现选择性挂起在硬件级别。

USB 函数驱动程序应实现选择性挂起 WDF，这与总线驱动程序进行通信并管理设备的 I/O 控制请求挂起和恢复设备函数通过其个人设备函数。 WDF 启用这两个内核模式和用户模式驱动程序以支持选择性挂起。

详细信息的功能驱动程序的 USB 选择性挂起代码依赖于驱动程序是否在用户模式或内核模式下运行。 请考虑以下准则：

-   使用用户模式驱动程序框架 (UMDF) 来实现尽可能的 USB 驱动程序。 用户模式驱动程序不太可能会损坏系统数据和要简单得比内核模式驱动程序调试。
-   使用内核模式驱动程序框架 (KMDF)，仅当该驱动程序数据流式传输通过同步终结点或需要其他功能或仅在内核模式中可用的资源。

## <a name="power-policy-ownership-io-queues-and-selective-suspend"></a>电源策略所有权、 I/O 队列和选择性挂起


设备堆栈的电源策略所有者 (PPO) 是确定哪些设备应放置在任何给定时间的电源状态的驱动程序。 每个设备堆栈中的只有一个驱动程序可以是 PPO。 功能驱动程序通常是为其设备 PPO。

如果您的 USB 驱动程序支持选择性挂起，并且在其设备堆栈 PPO 上进行分层，驱动程序必须使用电源管理队列。 这适用于 UMDF 和 KMDF 驱动程序。 如果请求到达电源管理队列的设备被挂起时，可以安装整个设备堆栈。

图 1 显示了对通过其 I/O 的队列的 USB 驱动程序的 I/O 请求的流。

![wdf usb 驱动程序的请求流](images/flowrequestswdfusbdriver.png)

在图中，请求到达 USB 驱动程序。 该框架将请求添加到相应的队列。

如果队列不是电源管理，框架提供了对根据队列 （顺序口，或手动） 的配置驱动程序的调度类型驱动程序的请求。 然后，该驱动程序处理的请求。

如果队列是电源管理，且设备未挂起，框架提供了对根据配置的调度类型驱动程序的请求。

但是，如果设备被挂起，框架的操作取决于驱动程序是否为设备堆栈 PPO。 如果该驱动程序，PPO 框架与要在设备接通电源的 USB 父驱动程序通信。 已恢复设备后，框架提供了对该驱动程序的请求。

如果驱动程序不是 PPO，框架会采用任何进一步操作，因为仅 PPO 可以恢复设备。 请求将保留在队列中。 设备堆栈停留如果 PPO 不会接收会导致它以恢复设备的任何请求。

## <a name="in-this-section"></a>本部分内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="selective-suspend-in-umdf-drivers.md" data-raw-source="[Selective suspend in UMDF drivers](selective-suspend-in-umdf-drivers.md)">在 UMDF 驱动程序的选择性挂起</a></p></td>
<td><p>本主题介绍如何 UMDF 函数驱动程序支持 USB 选择性挂起。</p></td>
</tr>
<tr class="even">
<td><p><a href="selective-suspend-in-a-kmdf-function-driver.md" data-raw-source="[Selective suspend in USB KMDF function drivers](selective-suspend-in-a-kmdf-function-driver.md)">USB KMDF 函数驱动程序中的选择性挂起</a></p></td>
<td><p>本主题介绍如何 KMDF 函数驱动程序支持 USB 选择性挂起。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[Windows 驱动程序框架 (WDF)](https://go.microsoft.com/fwlink/p/?linkid=53698)  
[Plug and Play-体系结构和驱动程序支持](https://go.microsoft.com/fwlink/p/?linkid=320985)  
[KMDF 驱动程序中的 PnP 和电源管理](https://go.microsoft.com/fwlink/p/?linkid=320986)  
[WDF 驱动程序时可以使用电源管理的 I/O 队列](https://go.microsoft.com/fwlink/p/?linkid=320987)  
[编写与 WDF 的 USB 驱动程序](https://go.microsoft.com/fwlink/p/?linkid=320988)  
[在 USB 客户端驱动程序中实施电源管理](https://go.microsoft.com/fwlink/p/?linkid=320989)  



