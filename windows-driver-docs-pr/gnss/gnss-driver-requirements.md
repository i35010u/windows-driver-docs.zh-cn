---
title: GNSS 驱动程序要求
description: 介绍适用于 Windows 10 开发 GNSS 驱动程序时要考虑的要求，假设和约束。
ms.assetid: BA117292-4877-4753-8FEB-2DEE6450155D
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: a9f37a4a1e9794c10703e0ca12bf8660e56d8092
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363667"
---
# <a name="gnss-driver-requirements"></a>GNSS 驱动程序要求

介绍适用于 Windows 10 开发 GNSS 驱动程序时要考虑的要求，假设和约束。

## <a name="general-requirements"></a>常规要求

-   **驱动程序框架：** GNSS 驱动程序应被编写为 UMDF 2.0 驱动程序基于此接口定义，而不是原始的 WDM 驱动程序或 KMDF 驱动程序。 UMDF 1.0 驱动程序不支持任何一个。 GNSS 驱动程序接口定义或 Microsoft 高级别操作系统 (HLOS) GNSS 组件，如 GNSS 适配器执行操作之间进行区分 WDF，KMDF GNSS 驱动程序和 UMDF 2.0 驱动程序，只要该驱动程序提供了每个此所需的功能界面设计。 UMDF 2.0 提供了更高版本的稳定性、 简易性和灵活性来实现功能需要仅在用户模式中提供的功能。 作为一般规则，Ihv 更愿意使用 UMDF 2.0 KMDF 以前 framework 平台上不可用。

    > [!NOTE]
    >  UMDF 2.0 是在所有平台上和 Ihv 强烈建议使用驱动程序在用户模式下编写。

-   **多个应用程序会话：** 应用程序会话是从直接与 GNSS 驱动程序进行交互的 HLOS 组件即将定位会话。 GNSS 驱动程序可以选择以本机方式支持多个应用程序会话通过划分其状态变量和每个应用程序的基础功能。 这是一项可选功能的驱动程序，并指示专门通过明确定义 GNSS 驱动程序功能的信息。 为了支持这一可选行为，GNSS 驱动程序所需跟踪的 HLOS 应用程序期间获取的文件句柄**CreateFile**，并将关联到特定于应用程序会话的所有后续 HLOS 操作文件句柄。 这从 GNSS 驱动程序的本机支持允许 HLOS 组件更加灵活和更少限制性有关公开到平台的其余部分的驱动程序的信息。 支持此功能的 GNSS 驱动程序可能需要以逻辑方式进行分区和维护每个单独的应用程序会话的状态信息。 不支持此功能的 GNSS 驱动程序只需维护而不是逻辑特定于应用程序分区的所有应用程序会话的全局状态。 在此后一种模式下，GNSS 驱动程序并不在意的多个并行应用程序会话状态，并将所有请求从 HLOS 视为来自同一应用程序会话。

    ![gnss 驱动程序支持的多个应用程序会话](images/gnss-architecture-1.png)

    GNSS 驱动程序的多个应用程序会话中的支持已启用测试中的应用程序 HLOS GNSS 适配器时直接与 GNSS 驱动程序交互的优势。 测试应用程序和 GNSS 适配器是我们被视为不同的应用程序可以请求到单个 GNSS 驱动程序不同的会话同时。 如果不支持多个应用程序会话，然后 GNSS 驱动程序需要为测试与通过 OS 位置平台，或应否则停止托管 OS 位置平台的服务以避免干扰测试应用程序。

-   **解决会话：** 获取定位信息从基础驱动程序 （一个镜头或跟踪） 的行为已抽象化为修复会话概念。 驱动程序必须支持至少一个修补程序会话的支持每个会话类型。 会话类型定义下[ **GNSS\_FIXSESSIONTYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ne-gnssdriver-gnss_fixsessiontype)枚举。

    -   至少，GNSS 驱动程序必须支持单个单次触发的修复会话。

    -   支持距离的驱动程序基于单个单次触发的修复会话和一个距离基于跟踪修复会话，会话必须同时支持跟踪修复。

    -   驱动程序的支持时间基于单个单次触发的修复会话和时间基于跟踪修复会话，会话必须同时支持跟踪修复。

    -   支持基于距离跟踪的驱动程序修复次单次触发的修复会话、 距离基于跟踪修复会话和基于时间跟踪修复会话，会话必须同时支持的会话和基于时间跟踪修复。

    ![驱动程序支持的多个同时进行修复，会话](images/gnss-architecture-2.png)

    该驱动程序是否支持多个同时修复会话，或不通过定义完善的驱动程序功能参数来表示。 如果驱动程序不显式支持多个并行的修补程序会话，它必须失败了新的修补程序会话请求，如果相同的修复类型的会话已启动并处于活动状态。 如果不存在多个修复会话支持，则潜能，HLOS 组件以确保来自高级应用程序的多个 GNSS 请求进行多路复用，并映射到对 GNSS 驱动程序的单一修复会话请求。

    GNSS 驱动程序不需要支持相同类型的多个并行修复会话。 实际上在 Windows 10 中 HLOS GNSS 适配器不支持利用 GNSS 驱动程序功能使用相同类型的多个修补程序会话，因此不建议 Ihv 投资上目前此功能。 在将来版本将被视为可启用 GNSS 适配器可直接使用 GNSS 驱动程序为每个修补程序请求获取从位置平台的上层，而不是以多路复用本身在会话启动会话。 支持的修补程序会话 GNSS 适配器中的多路复用简化了驱动程序实现，因为它不需要它来处理多个会话的应用程序的相同类型或实现的多路复用，它减少了在驱动程序中的内存使用情况和它不需要 GNSS 适配器以处理启动会话大于 GNSS 驱动程序支持的功能的修补程序的大量 HLOS 的情况。 不同层的设备和不同的驱动程序将支持不同数目的并发修复会话，因此这种情况下需要进行处理，引入新的 GNSS 适配器来处理所有用例中的复杂性。 因此，在 Windows 10 中 GNSS 适配器将仅实现单个修复每个受支持的类型的会话和直到我们需要此功能将忽略由驱动程序的多个修复会话支持。

    每个修补程序会话是有状态，必须遵循此明确定义的顺序：

    1.  启动修复会话

    2.  获取一个或多个修补程序

    3.  如果需要，修改修复会话

        > [!NOTE]
        > 这是必需的至少直到 GNSS 适配器处理多路复用的相同类型的修补程序会话，并甚至可能需要更高版本上以处理更多同时进行的修复方法的情况会话活动比 GNSS 驱动程序支持的数目。

    4.  停止修补程序的会话

    修复会话进行唯一标识一个修补程序会话 id。 可通过修复会话的上下文之外 HLOS 不检索任何位置信息。 GNSS 驱动程序必须动态，从而简化通过 HLOS 组件，而无需重新启动修复会话进行多路复用操作允许修改会话参数。

    ![修复报表 gnss 驱动程序和应用程序之间的通信](images/gnss-architecture-3.png)

-   **修复类型：** GNSS 驱动程序必须在修复基本的单个快照的最小支持。 此外，驱动程序本机应支持高级修补程序的类型 （如跟踪）。 如前面所述，提供对其他修补程序类型支持意味着，即使该驱动程序不支持相同类型的多个修补程序会话，它必须支持同时支持的修补程序类型的至少一个修补程序会话。 HLOS 组件不会不合并到单个类型不同的修复类型。

-   **设备接口和 PnP:** GNSS 驱动程序应将 Microsoft 定义的设备接口使用播发**WdfDeviceCreateDeviceInterface** API，以便可以获取 HLOS 到达和出发 GNSS 驱动程序有关的通知。 这将需要处理插 (PnP) 设置中的 GNSS 驱动程序，并且还在其中意外驱动程序卸载的情况下会造成因用户级别的服务故障的驱动程序 UMDF 2.0 驱动程序。 GNSS 驱动程序应确保播发设备接口时，才启动基础硬件是否能够支持 HLOS IOCTL 调用而不在此之前。

-   **设备电源策略：** GNSS 驱动程序应管理其设备的电源策略，并应处理由操作系统发出的电源管理事件。 该驱动程序应注册*WDF\_PNPPOWER\_事件\_回调。EvtDeviceD0Entry*回调 （时系统将进入 D0 状态，则引发的 WDF） 和*WDF\_PNPPOWER\_事件\_回调。EvtDeviceD0Exit*回调 （引起 WDF 系统从 D0 状态在退出时）。 GNSS 驱动程序应该是可配置的 （可选） 禁用电源管理。

    需要在不同的系统电源中的 GNSS 设备中完成的确切的电源管理状态需要改写根据 GNSS 设备的功能 (不支持卸载操作)、 是否有实际的卸载的操作活动状态，并且完成系统和 GNSS 设备之间的通信方式。 一般情况下人们的期望如下所示：
    -   GNSS 设备时不有任何活动会话将最低可能的电源模式中工作，或卸载操作，而不考虑系统电源状态。
    -   如果卸载的情况下，再次而不考虑系统电源状态，GNSS 设备可能需要检查的位置不同的时间间隔或接收通知并因此 GNSS 设备可能需要在连接待机时也处于 D0 状态 (这是屏幕关闭睡眠状态），但仍需要减少到最低的功率消耗硬件。 此模型适用于使用上 UART DMA （直接内存访问） 或串行端口，与主机进行通信，例如那些设备。 但对于这些 GNSS 已连接设备通过 USB 总线，在这种情况下最有可能设备的 USB 函数应该在 D2 将成为了难题 （挂起） 期间连接待机设备电源状态。 一般情况下必须能够进入低功耗 D2 GNSS 设备通过 USB 连接 （挂起） 状态后已没有修补程序的会话，或者卸载的操作正在进行和 USB 总线接口进入挂起状态。 所有的睡眠和唤醒电源转换必须通过 USB 总线发出信号。 如果 GNSS 设备已修复会话活动或卸载操作，设备必须能够使用带内，USB 恢复信号唤醒从连接待机 SoC 或核芯片。 SoC 或核心硅必须能够以从响应中带 USB 恢复从 GNSS 设备信号其最低电源状态中唤醒。
    -   不支持连接的待机的设备将具有所有设备时出现现代待机或休眠状态时已取消的卸载的操作。 这包括卸载地域隔离区、 跟踪、 距离或定期跟踪会话。
    -   支持连接的待机的设备将继续时在设备进入连接待机和 GNSS 设备应以尽可能高效地继续跟踪操作和预期需要提供能够所有活动的卸载的操作本例中为通知发送到在 HLOS 地域隔离区触发器条件或更新是相关的跟踪会话。 如果没有支持连接待机的设备中卸载的操作，GNSS 设备应该转到最低的电源状态可能，但仍将能够从 HLOS 侦听位置会话请求。 在支持 SUPL 的设备，它必须还能 GNSS 设备和 SUPL 堆栈 NI 通知中连接待机状态唤醒。

    驱动程序的电源管理的常规信息可在[驱动程序的电源管理责任](https://docs.microsoft.com/windows-hardware/drivers/kernel/power-management-responsibilities-for-drivers)。

-   **电源问题需要考虑：** GNSS 驱动程序堆栈必须考虑能源占用量作为主要设计目标，并最大程度减少保留主处理器唤醒状态最大程度地。 所有高级功能支持 （例如不同的修复类型） 必须执行如比主应用程序的处理器不需要处于活动状态超过所需的节能的方式和大多数处理可以卸载到芯片组/低功耗处理器。 作为一般规则，除非另有说明从 HLOS，GNSS 驱动程序必须始终视为功率消耗的最重要的约束，并必须设计为执行具有最少的能源占用量的正常操作。 GNSS 驱动程序接口被专门允许移动设备经常更新，过渡到低能耗模式并提供对 GNSS 驱动程序，以优化电源使用情况的需要与电源相关提示。 有关跟踪、 地理围栏和所需长时间运行普遍位置监视的其他功能，GNSS 驱动程序/引擎必须充分利用低能耗硬件/处理器。 如果此类功能驱动程序中使用暴力破解轮询机制来实现，或者它需要在应用程序处理器中实现，该驱动程序不应声明本身为此类操作的支持。 这将允许 HLOS 限制公开此类功能对平台的其余部分，或使用这些功能基于其他平台服务/基元的备用实现。

-   **编程语言：** GNSS 驱动程序接口传递为不使用任何的 C 语言头文件C++特定语言基元 （例如，结构继承）。 这允许 IHV C 之间进行选择和C++。 GNSS 接口标头文件会使选择面临 Ihv。

-   **筛选器驱动程序：** GNSS 设备堆栈必须不受约束不会被添加未来的筛选器驱动程序堆栈以支持扩展的功能中的此类的方式。 IHV 提供 GNSS 驱动程序不能包含其自己筛选器驱动程序，在顶部或底部的驱动程序堆栈。

-   **通知和事件：** 由于 WDF 驱动程序不能将未经请求的通知发送到 HLOS，始终将至少一个挂起的 IRP 从充当从驱动程序层接收未经请求的任何此类通知 HLOS 启动。 这包括系统处于连接待机这种情况。 对于 GNSS 驱动程序，此类未经请求的通知包括 （但不限于） 网络发起的请求、 AGNSS 支持的协助数据、 其他特定于供应商的通知。 HLOS 将确保挂起的 I/O 请求都会出现在处理此类通知。

-   **用户模式下 IHV 扩展：** Ihv 可以编写通过 IHV 定义专用 Ioctl 与 GNSS 驱动程序进行交互的附件的用户模式组件。 特别是当时需要此 GNSS 驱动程序是在内核模式下，在这种情况下不能为用户模式 （例如，Wi-fi 扫描、 连接管理器 Api 和等等） 中以独占方式提供的功能的访问。 请注意，使用 Windows 10 中 UMDF 2.0，UMDF GNSS 驱动程序不需要单独的用户模式组件，虽然 IHV 仍可实现单独的用户模式组件。 这些用户模式组件将被视为是仅仅对 GNSS 驱动程序扩展，并将被视为 IHV 传递 BSP 放置的一部分。 Microsoft 提供 HLOS 组件是此类组件和 IHV 用户模式/内核模式组件之间的交互机制的确切实现细节不在意。 如果不建议使用用户模式下 IHV 扩展 UMDF 2.0 驱动程序，因为此模型可能会被写入 GNSS 驱动程序需要更多的内存使用情况。

    用户模式下 IHV 扩展必须符合以下规则：
    -   不受影响并没有被用户模式下 IHV 扩展和及其与 GNSS 驱动程序的交互，必须保持的语义和公共 GNSS 驱动程序 Ioctl 的行为。
    -   用户模式下扩展必须符合安全性、 功能和其他平台基础知识及 Windows 10 平台所规定的策略。
    -   用户模式下扩展必须执行仅授权的活动而无需强制执行/验证在运行时这种授权的操作系统平台由 Microsoft 批准。

    > [!NOTE]
    > Microsoft 仍可以强制实施安全策略和控件生存期的此类组件。 此处的关键点是不应统计 IHV 用户模式组件在平台上以强制实施此类策略作为扩展组件被视为受信任的操作系统组件。

    Ihv 将不添加任意功能或使用未经授权的操作系统服务 / 保护资源。

## <a name="minimum-support-requirements"></a>最低支持要求

将有多种可用于 Windows 平台以满足需求的不同层的设备 （低成本，高结束、 不同的设备类型等） 的 GNSS 设备。 若要启用此类丰富生态系统和增加的平板电脑、 便携式计算机和其他设备类型可以包含较低的成本的 GNSS 芯片的数，Microsoft 不需要所有 GNSS 设备，以支持完整的中所述的功能集[GNSS 驱动程序引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver)。 下表提供了不同的设备类型和哪些功能是可选的还是建议所需的最少功能的高级别视图。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所有平台的的要求</th>
<th>适用于手机特定的要求</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>准确地报告 GNSS_DEVICE_CAPABILITIES</p></td>
<td><p>强制</p></td>
<td></td>
<td><p>最小功能要求。</p></td>
</tr>
<tr class="even">
<td><p>对 MultipleFixSessions 的支持</p></td>
<td><p>可选</p></td>
<td></td>
<td><p>不支持由 GNSS 适配器。</p></td>
</tr>
<tr class="odd">
<td><p>对 MultipleAppSessions 的支持</p></td>
<td><p>建议</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>GNSS 协助支持 （IHV 特定于）</p></td>
<td><p>推荐</p></td>
<td><p>强制</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>获取通过 Microsoft （使用 Agss_inject Ioctl） GNSS 协助支持</p></td>
<td><p>建议</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>对完整 GNSS_FixData 结构的支持</p></td>
<td><p>强制</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>单个单次触发的会话</p></td>
<td><p>强制</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>基于时间的跟踪会话的本机支持</p></td>
<td><p>可选</p></td>
<td></td>
<td><p>如果支持，它必须包括支持，以修改会话参数。</p></td>
</tr>
<tr class="odd">
<td><p>基于距离的跟踪会话的本机支持</p></td>
<td><p>可选</p></td>
<td></td>
<td><p>如果支持，它必须包括支持，以修改会话参数。</p></td>
</tr>
<tr class="even">
<td><p>最后一个很好的已知的会话</p></td>
<td><p>可选</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>地理围栏的本机支持</p></td>
<td><p>可选</p></td>
<td><p>建议</p></td>
<td><p>仅循环地域隔离区所需和支持。</p></td>
</tr>
<tr class="even">
<td><p>Providing ChipsetInfo</p></td>
<td><p>强制</p></td>
<td></td>
<td><p>使用 GNSS_ChipsetInfo。</p></td>
</tr>
<tr class="odd">
<td><p>报告错误</p></td>
<td><p>建议</p></td>
<td></td>
<td><p>使用 GNSS_ErrorInfo</p></td>
</tr>
<tr class="even">
<td><p>通过 NMEA 的报表</p></td>
<td><p>可选</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>生产测试支持 （载波或自行测试）</p></td>
<td><p>可选</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>管理平面位置与 MBB 集成</p></td>
<td><p>仅当所需的移动运营商，则为强制</p></td>
<td><p>强制</p></td>
<td><p>通常情况下所需的语音支持的设备中的移动运营商。 几乎总是需要适用于手机。</p></td>
</tr>
<tr class="odd">
<td><p>SUPL 1.0</p></td>
<td><p>仅当所需的移动运营商，则为强制</p></td>
<td></td>
<td><p>一般情况下，替换为的 SUPL 2.0。</p>
<p>包含实现满足移动运营商要求，通过 DDI，配置完整的客户端向 MBB 使用 DDI 和集成通过操作系统报告的 NI 事件。</p></td>
</tr>
<tr class="even">
<td><p>SUPL 2.x</p></td>
<td><p>仅当所需的移动运营商，则为强制</p></td>
<td><p>强制</p></td>
<td><p>通常情况下所需的语音支持的设备中的移动运营商。 几乎总是需要适用于手机。</p>
<p>包含实现满足移动运营商要求，通过 DDI，配置完整的客户端向 MBB 使用 DDI 和集成通过操作系统报告的 NI 事件。</p></td>
</tr>
<tr class="odd">
<td><p>UPL</p></td>
<td><p>仅当所需的移动运营商，则为强制</p></td>
<td></td>
<td><p>只需根据需要移动运营商在中国，传送这些 CDMA 设备支持。</p>
<p>包括： 满足移动运营商要求，通过 DDI，配置完整的客户端实现向 MBB 使用 DDI 和集成通过操作系统报告的 NI 事件。</p></td>
</tr>
<tr class="even">
<td><p>GNSS_SetLocationServiceEnabled 的驱动程序命令</p></td>
<td><p>强制</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>GNSS_SetLocationNIRequestAllowed 的驱动程序命令</p></td>
<td><p>仅当 SUPL 支持和所需的移动运营商，则为强制</p></td>
<td></td>
<td><p>没有已知移动运营商不再需要它。</p></td>
</tr>
<tr class="even">
<td><p>GNSS_ForceSatelliteSystem 的驱动程序命令</p></td>
<td><p>建议</p></td>
<td></td>
<td><p>适用于测试目的。 某些移动运营商或 Oem 可能会需要此进行测试。</p></td>
</tr>
<tr class="odd">
<td><p>GNSS_ForceOperationMode 的驱动程序命令</p></td>
<td><p>仅当 SUPL 支持，则为强制</p></td>
<td></td>
<td><p>某些移动运营商可能需要出于测试目的。</p></td>
</tr>
<tr class="even">
<td><p>GNSS_ResetEngine 的驱动程序命令</p></td>
<td><p>强制</p></td>
<td></td>
<td><p>出于测试目的。</p></td>
</tr>
<tr class="odd">
<td><p>GNSS_ClearAgnssData 的驱动程序命令</p></td>
<td><p>强制</p></td>
<td></td>
<td><p>出于测试目的。</p></td>
</tr>
<tr class="even">
<td><p>GNSS_SetNMEALogging 的驱动程序命令</p></td>
<td><p>可选</p></td>
<td></td>
<td><p>仅当所需的移动运营商或 Oem 需求这出于测试目的。</p></td>
</tr>
<tr class="odd">
<td><p>GNSS_SetSuplVersion 的驱动程序命令</p></td>
<td><p>仅当 SUPL 支持，则为强制</p></td>
<td></td>
<td><p>对于 SUPL 必需。</p></td>
</tr>
<tr class="even">
<td><p>GNSS_SetUplServerAccessInterval driver command</p></td>
<td><p>仅当 SUPL 支持和所需的移动运营商，则为强制</p></td>
<td></td>
<td><p>仅当所需的移动运营商。</p></td>
</tr>
<tr class="odd">
<td><p>GNSS_SetNiTimeoutInterval 的驱动程序命令</p></td>
<td><p>仅当 SUPL 支持和所需的移动运营商，则为强制</p></td>
<td></td>
<td><p>仅当所需的移动运营商。</p></td>
</tr>
<tr class="even">
<td><p>GNSS_ResetGeofencesTracking 的驱动程序命令</p></td>
<td><p>仅当支持地理围栏的必需</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>GNSS_CustomCommand 的驱动程序命令</p></td>
<td><p>可选</p></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>










