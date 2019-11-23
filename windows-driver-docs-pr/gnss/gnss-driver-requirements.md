---
title: GNSS 驱动程序要求
description: 描述在开发适用于 Windows 10 的 GNSS 驱动程序时要考虑的要求、假设和约束。
ms.assetid: BA117292-4877-4753-8FEB-2DEE6450155D
ms.date: 05/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: b656fdebce7edbf08aab39fc2036958f63dc3ac0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825084"
---
# <a name="gnss-driver-requirements"></a>GNSS 驱动程序要求

描述在开发适用于 Windows 10 的 GNSS 驱动程序时要考虑的要求、假设和约束。

## <a name="general-requirements"></a>常规要求

-   **驱动程序框架：** GNSS 驱动程序应根据此接口定义（而不是原始 WDM 驱动程序或 KMDF 驱动程序），将其作为 UMDF 2.0 驱动程序 a 写入。 不支持 UMDF 1.0 驱动程序。 GNSS 驱动程序接口定义或 Microsoft 高级操作系统（HLOS） GNSS 组件（如 GNSS 适配器）不会在 WDF、KMDF GNSS 驱动程序和 UMDF 2.0 驱动程序之间进行区分，前提是该驱动程序提供了每个所需的功能接口设计。 UMDF 2.0 为实现需要仅在用户模式下提供的功能的功能提供更高的稳定性、简易性和灵活性。 作为一般规则，当平台上有以前的框架时，Ihv 应首选使用 UMDF 2.0 到 KMDF。

    > [!NOTE]
    >所有平台上均提供   UMDF 2.0，因此强烈建议使用以用户模式编写的驱动程序。

-   **多个应用程序会话：** 应用程序会话是来自直接与 GNSS 驱动程序交互的 HLOS 组件的定位会话。 GNSS 驱动程序可以选择以本机方式支持多个应用程序会话，方法是将其状态变量和功能分区为每个应用程序。 这是驱动程序的可选功能，由明确定义的 GNSS 驱动程序功能信息表示。 为了支持此可选行为，GNSS 驱动程序需要跟踪 HLOS 应用程序在**CreateFile**期间获取的文件句柄，并将所有后续 HLOS 操作关联到应用程序会话特定的文件句柄。 GNSS 驱动程序的这一本机支持使 HLOS 组件更灵活，并且限制了向平台的其余部分公开该驱动程序。 支持此功能的 GNSS 驱动程序可能需要逻辑分区并维护每个单独应用程序会话的状态信息。 不支持此功能的 GNSS 驱动程序只需为所有应用程序会话（而不是逻辑应用特定的分区）维护全局状态。 在后一种模式下，GNSS 驱动程序在意多个并行应用程序会话的存在，并处理来自 HLOS 的所有请求，就像它们源自同一应用程序会话一样。

    ![gnss 驱动程序支持多个应用程序会话](images/gnss-architecture-1.png)

    GNSS 驱动程序中支持多个应用程序会话的优势在于，在 HLOS 中启用测试应用程序，以便与 GNSS 适配器同时直接与 GNSS 驱动程序交互。 测试应用程序和 GNSS 适配器是我们被视为不同应用程序的，这些应用程序可以同时请求单个 GNSS 驱动程序不同的会话。 如果不支持多个应用程序会话，则需要通过 OS 位置平台测试 GNSS 驱动程序，否则应停止托管 OS 位置平台的服务，以避免干扰测试应用程序。

-   **修复会话：** 从底层驱动程序（单个拍摄或跟踪）获取定位信息的操作将抽象到修复会话的概念中。 驱动程序需要支持每个支持的会话类型的至少一个修复会话。 会话类型在[**GNSS\_FIXSESSIONTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver/ne-gnssdriver-gnss_fixsessiontype)枚举下定义。

    -   至少，GNSS 驱动程序必须支持单个快照修复会话。

    -   支持基于距离的跟踪修复会话的驱动程序必须同时支持单个快照修复会话和基于距离的跟踪修复会话。

    -   支持基于时间的跟踪修复会话的驱动程序必须同时支持单个快照修复会话和基于时间的跟踪修复会话。

    -   支持基于距离的跟踪修复会话和基于时间的跟踪修复会话的驱动程序必须同时支持单个快照修复会话、基于距离的跟踪修复会话和基于时间的跟踪修复会话。

    ![支持多个同时修复会话的驱动程序](images/gnss-architecture-2.png)

    驱动程序是否支持多个同时修复会话，或者不是由定义完善的驱动程序功能参数表示的。 如果驱动程序未显式支持多个并行修复会话，则在同一修补程序类型的会话已启动且处于活动状态时，它必须使新的修补会话请求失败。 如果不存在多个修补会话支持，则潜能将位于 HLOS 组件上，以确保来自高级别应用程序的多个 GNSS 请求会被复用并映射到 GNSS 驱动程序的单个修复会话请求。

    不需要 GNSS 驱动程序来支持同一类型的多个并行修复会话。 事实上，在 Windows 10 中，HLOS GNSS 适配器不支持使用 GNSS 驱动程序功能来具有相同类型的多个修补会话，因此不鼓励 Ihv 在此期间投入使用此功能。 在将来的版本中，它将被视为允许 GNSS 适配器使用 GNSS 驱动程序直接启动从位置平台的上部获取的每个修复请求，而不是执行会话多路复用。 GNSS 适配器中支持多路复用修补会话可以简化驱动程序实现，因为它不需要处理应用程序的多个相同类型的会话或多路复用，它会减少驱动程序中的内存使用量，它不需要 GNSS 适配器来处理 HLOS 的情况，这种情况下的修复会话比 GNSS 驱动程序所支持的多。 不同层的设备和不同的驱动程序将支持不同数量的并发修补会话，因此，这种情况需要进行处理，从而在 GNSS 适配器中引入了处理所有情况的复杂性。 因此，在 Windows 10 中，GNSS 适配器将只实现每个受支持的类型的单个修补会话，并将忽略该驱动程序的多个修复会话支持，直到我们需要此功能。

    每个修复会话都是有状态的，并且必须遵循此定义明确的顺序：

    1.  启动修补会话

    2.  获取一个或多个修补程序

    3.  根据需要修改修补会话

        > [!NOTE]
        > 在 GNSS 适配器处理相同类型的修复会话的多路复用之前，此方法是必需的，甚至可能会要求稍后再处理超过 GNSS 驱动程序所支持的数目的并发修复会话的情况。

    4.  正在停止修补会话

    修补会话由修补会话 ID 唯一标识。 在修复会话上下文之外，HLOS 不能检索位置信息。 GNSS 驱动程序必须随时允许修改会话参数，以方便 HLOS 组件进行多路复用操作，而无需重新启动修复会话。

    ![修复 gnss 驱动程序和应用程序之间的报表通信](images/gnss-architecture-3.png)

-   **修复类型：** GNSS 驱动程序必须至少支持基本的单步修复。 另外，驱动程序应以本机方式支持高级修补类型（如跟踪）。 如前文所述，支持其他修补程序类型意味着即使驱动程序不支持同一类型的多个修补会话，也必须同时支持至少一个支持的修复类型的修复会话。 HLOS 组件不会将不同的修复类型复合为单一类型。

-   **设备接口和 PnP：** GNSS 驱动程序应使用**WdfDeviceCreateDeviceInterface** API 播发 Microsoft 定义的设备接口，以便 HLOS 接收 GNSS 驱动程序的到达和出发通知。 如果驱动程序是 UMDF 2.0 驱动程序，则在即插即用（PnP）设置中处理 GNSS 驱动程序时，也将需要此操作，也可能是由于用户级别服务崩溃而导致意外的驱动程序卸载。 GNSS 驱动程序应确保仅在下面的硬件能够支持 HLOS IOCTL 调用，而不是在此之前公布设备接口。

-   **设备电源策略：** GNSS 驱动程序应该管理其设备的电源策略，并应对操作系统引发的电源管理事件进行处理。 驱动程序应为*WDF\_PNPPOWER\_事件\_回调进行注册。EvtDeviceD0Entry*回调（系统进入 D0 状态时由 wdf 引发）和*WDF\_PNPPOWER\_事件\_回调。EvtDeviceD0Exit*回调（当系统从 D0 状态退出时由 WDF 引发）。 GNSS 驱动程序应可配置为可选择禁用电源管理。

    需要在不同系统电源状态下的 GNSS 设备中执行的确切电源管理需要根据 GNSS 设备的功能（它是否支持卸载操作或不支持卸载操作）进行调整，无论是否有实际的卸载操作"活动"，以及 "系统" 和 "GNSS" 设备之间的通信是如何完成的。 一般情况下，预期如下：
    -   当没有活动会话或卸载操作时，无论系统电源状态如何，GNSS 设备都将在可能的最小电源模式下工作。
    -   如果卸载了方案，则无论系统电源状态如何，GNSS 设备可能需要以不同的时间间隔检查位置还是接收通知，因此，即使在连接备用期间，GNSS 设备也可能需要处于 D0 状态（这是屏幕关闭睡眠状态），但仍然需要硬件将能耗降到最低。 例如，此模型适用于使用 DMA （直接内存访问）或 UART 上的串行端口来与主机通信的那些设备。 但对于通过 USB 总线连接的 GNSS 设备，这是一项挑战，在这种情况下，设备的 USB 函数在连接备用期间应处于 D2 （挂起）设备电源状态。 通常，通过 USB 连接的 GNSS 设备必须能够进入低功率 D2 （挂起）状态，之后它们没有任何修复会话或卸载的操作，并且 USB 总线接口进入挂起状态。 所有睡眠和唤醒电源转换都必须通过 USB 总线发出信号。 如果 GNSS 设备具有活动或卸载操作的修补会话，则设备必须能够使用带内连接，USB 恢复信号，以从连接待机状态唤醒 SoC 或核心芯片。 SoC 或核心硅必须能够从其最低电源状态中唤醒，以响应带内设备，USB 恢复从 GNSS 设备发出的信号。
    -   在设备进入新式待机或休眠状态时，不支持连接待机的设备将取消所有卸载的操作。 这包括现成卸载、距离跟踪或定期跟踪会话。
    -   当设备进入连接待机状态时，支持连接待机的设备将继续处于活动状态，并且 GNSS 设备应尽可能高效地继续跟踪操作，并且应提供当地域隔离区内触发器条件或跟踪会话更新相关时，通知到 HLOS。 如果设备中没有支持连接待机的卸载操作，则 GNSS 设备应尽可能进入最低电源状态，但仍可以侦听来自 HLOS 的位置会话请求。 在支持 SUPL 的设备中，GNSS 设备和 SUPL stack 还必须能够在连接备用时唤醒 NI 通知。

    有关驱动程序电源管理的一般信息，请参阅[驱动程序的电源管理责任](https://docs.microsoft.com/windows-hardware/drivers/kernel/power-management-responsibilities-for-drivers)。

-   **电源注意事项：** GNSS 驱动程序堆栈必须将电源占用量考虑为主要设计目标，并尽量减少使主处理器尽可能唤醒。 所有高级功能支持（例如不同的修复类型）都必须以节能方式执行，如主应用处理器不需要处于活动状态，并且大多数处理都可以卸载到芯片/低功耗处理器。 作为一般规则，除非 HLOS 中另有说明，否则 GNSS 驱动程序必须始终将能源消耗视为最重要的限制，并且必须设计为执行正常操作，同时降低功率消耗。 GNSS 驱动程序接口显式设计为允许移动设备尽可能频繁地转换为低功耗模式，并向 GNSS 驱动程序提供必要的与电源相关的提示以优化电源使用情况。 对于需要长时间运行的普遍位置监视的跟踪、地理围栏和其他功能，GNSS 驱动程序/引擎必须利用低功耗硬件/处理器。 如果必须使用驱动程序中的强制轮询机制来实现此类功能，或者需要在应用处理器中实现此类功能，则驱动程序不应将其自身声明为能够执行此类操作。 这使 HLOS 可以将此类功能的公开限制到平台的其余部分，或者根据其他平台服务/基元使用这些功能的替代实现。

-   **编程语言：** GNSS 驱动程序接口以 C 语言标头文件的形式提供，不使用任何C++特定的语言基元（例如，结构继承）。 这允许 IHV 在 C 和C++之间进行选择。 GNSS 接口头文件使选择对 Ihv 保持开放。

-   **筛选器驱动程序：** 不能将 GNSS 设备堆栈限制为阻止在堆栈中添加未来的筛选器驱动程序以支持扩展功能。 IHV 提供的 GNSS 驱动程序不得在驱动程序堆栈的顶部或底部包含其自己的筛选器驱动程序。

-   **通知和事件：** 由于 WDF 驱动程序无法将未经请求的通知发送到 HLOS，因此从 HLOS 中始终至少会有一个挂起的 IRP 从驱动程序层接收任何此类未经请求的通知。 这包括系统处于连接待机状态的情况。 对于 GNSS 驱动程序，此类未经请求的通知包括（但不限于）网络启动的请求、AGNSS 支持的协助数据、其他特定于供应商的通知。 HLOS 将确保始终存在挂起的 i/o 请求来处理此类通知。

-   **用户模式 IHV 扩展：** Ihv 可以编写通过 IHV 定义的专用 IOCTLs 与 GNSS 驱动程序交互的附件用户模式组件。 如果 GNSS 驱动程序处于内核模式，这是特别需要的，在这种情况下，它无法访问以用户模式独占方式（例如 Wi-fi 扫描、连接管理器 Api 等）的功能。 请注意，在 Windows 10 中使用 UMDF 2.0，UMDF GNSS 驱动程序不需要单独的用户模式组件，但 IHV 仍可能实现单独的用户模式组件。 这些用户模式组件被视为 GNSS 驱动程序的单纯扩展，并将被视为由 IHV 提供的 BSP 丢弃。 Microsoft 提供的 HLOS 组件在意了此类组件的准确实现细节以及 IHV 用户模式/内核模式组件之间的交互机制。 如果 GNSS 驱动程序是使用用户模式 IHV 扩展作为 UMDF 2.0 驱动程序写入的，则不建议这样做，因为此模型可能需要更多的内存使用量。

    用户模式 IHV 扩展必须符合以下规则：
    -   Public GNSS driver IOCTLs 的语义和行为必须不受用户模式 IHV 扩展的影响，并且与 GNSS 驱动程序交互。
    -   用户模式扩展必须符合 Windows 10 平台规定的安全性、功能和其他平台基础知识和策略。
    -   用户模式扩展只能执行 Microsoft 批准的授权活动，而无需在运行时使用操作系统平台强制/验证此类授权。

    > [!NOTE]
    > Microsoft 仍可强制实施此类组件的安全策略和控制生存期。 此处的关键在于 IHV 用户模式组件不应在平台上计数来强制执行此类策略，因为扩展组件被视为受信任的操作系统组件。

    Ihv 不会添加任意功能，也不会使用未经授权的 OS 服务/安全资源。

## <a name="minimum-support-requirements"></a>最低支持要求

对于 Windows 平台，可以使用大量的 GNSS 设备来满足不同的设备层（低成本、高端、不同设备类型等）的需求。 若要启用此类丰富的生态系统并增加可包含 GNSS 芯片的平板电脑、笔记本电脑和其他设备类型的数量，Microsoft 不需要所有 GNSS 设备支持[GNSS 驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/gnssdriver)中所述的完整功能集。 下表提供了不同设备类型所需的最小功能的高级视图，以及可选的或推荐的功能。

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
<th>所有平台的要求</th>
<th>手机的特定要求</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>准确报告 GNSS_DEVICE_CAPABILITIES</p></td>
<td><p>强制</p></td>
<td></td>
<td><p>最小功能要求。</p></td>
</tr>
<tr class="even">
<td><p>对 MultipleFixSessions 的支持</p></td>
<td><p>可选</p></td>
<td></td>
<td><p>不受 GNSS 适配器支持。</p></td>
</tr>
<tr class="odd">
<td><p>对 MultipleAppSessions 的支持</p></td>
<td><p>推荐</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>GNSS 协助支持（特定于 IHV）</p></td>
<td><p>推荐</p></td>
<td><p>强制</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>通过 Microsoft 获取 GNSS 援助支持（使用 Agss_inject IOCTLs）</p></td>
<td><p>推荐</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>支持完整 GNSS_FixData 结构</p></td>
<td><p>强制</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>单次拍摄会话</p></td>
<td><p>强制</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>基于时间的跟踪会话本机支持</p></td>
<td><p>可选</p></td>
<td></td>
<td><p>如果支持，则必须包含修改会话参数的支持。</p></td>
</tr>
<tr class="odd">
<td><p>基于距离的跟踪会话本机支持</p></td>
<td><p>可选</p></td>
<td></td>
<td><p>如果支持，则必须包含修改会话参数的支持。</p></td>
</tr>
<tr class="even">
<td><p>上一个已知良好的会话</p></td>
<td><p>可选</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>地理围栏本机支持</p></td>
<td><p>可选</p></td>
<td><p>推荐</p></td>
<td><p>仅要求和支持循环现成。</p></td>
</tr>
<tr class="even">
<td><p>提供 ChipsetInfo</p></td>
<td><p>强制</p></td>
<td></td>
<td><p>使用 GNSS_ChipsetInfo。</p></td>
</tr>
<tr class="odd">
<td><p>报告错误</p></td>
<td><p>推荐</p></td>
<td></td>
<td><p>使用 GNSS_ErrorInfo</p></td>
</tr>
<tr class="even">
<td><p>通过 NMEA 报告</p></td>
<td><p>可选</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>生产测试支持（载波波或自检）</p></td>
<td><p>可选</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>与 MBB 的集成的控制平面位置</p></td>
<td><p>只有移动运营商要求时才是必需的</p></td>
<td><p>强制</p></td>
<td><p>通常，移动运营商需要语音支持的设备。 手机几乎始终需要。</p></td>
</tr>
<tr class="odd">
<td><p>SUPL 1。0</p></td>
<td><p>只有移动运营商要求时才是必需的</p></td>
<td></td>
<td><p>一般替换为 SUPL 2.0。</p>
<p>包括实现完整的客户端会议移动运营商要求，通过 DDI 进行配置，通过 DDI 将 NI 事件报告给操作系统，并与 MBB 集成。</p></td>
</tr>
<tr class="even">
<td><p>SUPL 2。x</p></td>
<td><p>只有移动运营商要求时才是必需的</p></td>
<td><p>强制</p></td>
<td><p>通常，移动运营商需要语音支持的设备。 手机几乎始终需要。</p>
<p>包括实现完整的客户端会议移动运营商要求，通过 DDI 进行配置，通过 DDI 将 NI 事件报告给操作系统，并与 MBB 集成。</p></td>
</tr>
<tr class="odd">
<td><p>UPL</p></td>
<td><p>只有移动运营商要求时才是必需的</p></td>
<td></td>
<td><p>如果移动运营商要求，则只需要在中国的 CDMA 设备上提供支持。</p>
<p>包括：实现完整客户端会议移动运营商要求，通过 DDI 进行配置，通过 DDI 将 NI 事件报告给操作系统，并与 MBB 集成。</p></td>
</tr>
<tr class="even">
<td><p>GNSS_SetLocationServiceEnabled 驱动程序命令</p></td>
<td><p>强制</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>GNSS_SetLocationNIRequestAllowed 驱动程序命令</p></td>
<td><p>仅当移动运营商支持和需要 SUPL 时才是必需的</p></td>
<td></td>
<td><p>无已知的移动运营商不再需要此操作。</p></td>
</tr>
<tr class="even">
<td><p>GNSS_ForceSatelliteSystem 驱动程序命令</p></td>
<td><p>推荐</p></td>
<td></td>
<td><p>适用于测试目的。 某些移动运营商或 Oem 可能需要此进行测试。</p></td>
</tr>
<tr class="odd">
<td><p>GNSS_ForceOperationMode 驱动程序命令</p></td>
<td><p>仅当支持 SUPL 时才是必需的</p></td>
<td></td>
<td><p>某些移动运营商可能需要用于测试目的。</p></td>
</tr>
<tr class="even">
<td><p>GNSS_ResetEngine 驱动程序命令</p></td>
<td><p>强制</p></td>
<td></td>
<td><p>用于测试目的。</p></td>
</tr>
<tr class="odd">
<td><p>GNSS_ClearAgnssData 驱动程序命令</p></td>
<td><p>强制</p></td>
<td></td>
<td><p>用于测试目的。</p></td>
</tr>
<tr class="even">
<td><p>GNSS_SetNMEALogging 驱动程序命令</p></td>
<td><p>可选</p></td>
<td></td>
<td><p>只有移动运营商或 Oem 需要此方法才能实现测试目的。</p></td>
</tr>
<tr class="odd">
<td><p>GNSS_SetSuplVersion 驱动程序命令</p></td>
<td><p>仅当支持 SUPL 时才是必需的</p></td>
<td></td>
<td><p>对于 SUPL 是必需的。</p></td>
</tr>
<tr class="even">
<td><p>GNSS_SetUplServerAccessInterval 驱动程序命令</p></td>
<td><p>仅当移动运营商支持和需要 SUPL 时才是必需的</p></td>
<td></td>
<td><p>仅在移动运营商需要时使用。</p></td>
</tr>
<tr class="odd">
<td><p>GNSS_SetNiTimeoutInterval 驱动程序命令</p></td>
<td><p>仅当移动运营商支持和需要 SUPL 时才是必需的</p></td>
<td></td>
<td><p>仅在移动运营商需要时使用。</p></td>
</tr>
<tr class="even">
<td><p>GNSS_ResetGeofencesTracking 驱动程序命令</p></td>
<td><p>仅当支持地理围栏时才是必需的</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>GNSS_CustomCommand 驱动程序命令</p></td>
<td><p>可选</p></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>










