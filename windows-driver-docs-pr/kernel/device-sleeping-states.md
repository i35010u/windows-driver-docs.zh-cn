---
title: 设备低功耗状态
description: 设备低功耗状态
keywords:
- 设备电源状态 WDK 内核
- 设备低功耗状态 WDK 电源管理
- 睡眠电源管理 WDK 内核
- Dx 命名 WDK 电源管理
- 睡眠设备 WDK 电源管理
- 最低功率设备状态 WDK 内核
- 性能最高的设备低功耗状态 WDK 内核
- 中间睡眠状态 WDK 内核
- 低功耗模式 WDK 内核
- 省电模式 WDK 内核
- 持续电能 WDK 内核
- 延迟 WDK 电源管理
- 状态转换延迟 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e349d642739d242f5f2108fcf53e091330b940fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837719"
---
# <a name="device-low-power-states"></a>设备低功耗状态





设备电源状态 D1、D2 和 D3 是设备低功率状态。 从 Windows 8 开始，D3 分为两个 substates： [D3hot](#d3hot) 和 [D3cold](#d3cold)。

D1 和 D2 是中级低功耗状态。 许多设备类不定义这些状态。 所有设备都必须定义 D3hot。

以下各节介绍了 D1、D2 和 D3：

-   [设备电源状态 D1](#d1)
-   [设备电源状态 D2](#d2)
-   [设备电源状态 D3](#d3)

### <a name="device-power-state-d1"></a><a href="" id="d1"></a>设备电源状态 D1

设备电源状态 D1 是性能最高的设备低功耗状态。 其具有以下特征：

<a href="" id="power-consumption"></a>功率消耗  
消耗小于 D0 状态，但大于或等于 D2 状态的。 通常，D1 是一种时钟封闭状态，在该状态下，设备将接收足够的功率来保留设备的硬件上下文。 通常，支持 D1 的总线或设备类的规范更详细地介绍了此状态。

<a href="" id="device-context"></a>*设备上下文*  
通常，设备上下文由硬件保留，无需由驱动程序还原。 支持 D1 的总线或设备类的规范通常提供保留此上下文的详细要求。

<a href="" id="device-driver-behavior"></a>*设备驱动程序行为*  
驱动程序必须保存并还原或重新初始化硬件丢失的任何上下文。 但通常情况下，设备进入此状态时将丢失很少的上下文。

<a href="" id="restore-time"></a>*还原时间*  
通常，将设备从 D1 还原到 D0 所需的时间应小于从 D2 还原到 D0。

<a href="" id="wake-up-capability"></a>*唤醒功能*  
D1 中的设备可能能够请求唤醒。 若要提供有关此状态是否可以支持唤醒信号的信息，总线驱动程序使用 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities) 结构，或从 Windows 8 开始，使用 [GUID \_ D3COLD \_ 支持 \_ 接口](https://msdn.microsoft.com/library/windows/hardware/hh967714) 驱动程序接口。

通常，使用 D1 的设备会这样做，因为从此状态恢复不需要驱动程序还原设备的完整硬件上下文。 若要最大程度地减少用户的延迟，请将设备从 D1 还原到 D0，这可能会导致延迟最小。 最大程度地减少状态转换延迟比降低功率消耗更重要。

### <a name="device-power-state-d2"></a><a href="" id="d2"></a>设备电源状态 D2

D2 是一种具有以下特征的中间设备低功耗状态：

<a href="" id="power-consumption"></a>功率消耗  
消耗小于或等于 D1 状态的。

<a href="" id="device-context"></a>*设备上下文*  
通常，大多数设备上下文都丢失了硬件。 通常，此状态将保留用于对唤醒事件发出信号的上下文部分。 支持 D2 的总线或设备类的规范通常提供保留此上下文的详细要求。

<a href="" id="device-driver-behavior"></a>*设备驱动程序行为*  
设备驱动程序必须保存并还原或重新初始化硬件丢失的任何上下文。 典型设备进入 D2 时丢失大多数上下文。

<a href="" id="restore-time"></a>*还原时间*  
如果将设备从 D1 还原到 D0，则将设备从 D2 还原到 D0 至少需要一段时间。 在从 D2 转换到 D0 后，具有大帧缓冲区的图形适配器就是一个设备的示例，该设备具有大量要还原的硬件上下文。 对于此类设备，从 D2 还原时间可能远远大于从 D1 还原时间。

<a href="" id="wake-up-capability"></a>*唤醒功能*  
D2 中的设备可能能够请求唤醒。 若要提供有关此状态是否可以支持唤醒信号的信息，总线驱动程序使用 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities) 结构，或从 Windows 8 开始，使用 [GUID \_ D3COLD \_ 支持 \_ 接口](https://msdn.microsoft.com/library/windows/hardware/hh967714) 驱动程序接口。

通常，支持 D2 的驱动程序会这样做，因为其设备不支持从 D3 唤醒。 对于这些设备，D2 状态的电源消耗降到设备在响应唤醒信号时可以恢复的最低级别。 与 D1 状态不同的是，为了减少用户所能看到的延迟，实现 D2 状态的目标是节省电源。 因此，从 D2 到 D0 的还原时间通常会超出从 D1 到 D0 的时间。 例如，在 D2 状态下，总线上的电量降低可能导致设备关闭其某些功能，因而需要额外的时间来重新启动和还原设备。

许多设备类不定义此状态。

### <a name="device-power-state-d3"></a><a href="" id="d3"></a>设备电源状态 D3

D3 是性能最低的设备电源状态。 所有设备都必须支持此状态。

从 Windows 8 开始，操作系统细分 D3 分为两个不同的 substates、D3hot 和 D3cold。 较早版本的 Windows 定义 D3 状态，但不定义 D3hot 和 D3cold substates。 但是，所有版本的 [PCI 总线电源管理接口规范](https://pcisig.com/specifications/conventional/) 都定义了单独的 D3hot 和 D3cold substates，以及 [高级配置和电源接口规范](https://go.microsoft.com/fwlink/p/?linkid=57185) 的版本4及更高版本定义 D3hot 和 D3cold substates。

虽然 Windows 8 之前的 Windows 版本未明确定义 D3 的 D3hot 和 D3cold substates，但这些 substates 在这些早期版本的 Windows 中是隐式存在的。 如果设备显式处于 D3 状态，并且计算机处于 S0 系统电源状态，则会在 D3hot 子状态中隐式地显示设备。 在 D3hot 中，设备连接到电源 (虽然可能会将设备配置为绘制低电流) ，并且可以检测到总线上的设备状态。 如果设备显式处于 D3 状态，并且计算机处于低功耗 Sx 状态 (除了 S0) 以外的状态，则该设备在 D3cold 子状态中是隐式的。 在此隐式 D3cold 子状态中，设备可能会收到滴，但在发生唤醒事件之前，会有效关闭设备和计算机。

从 Windows 8 开始，设备可以输入并离开 D3cold 子状态，同时计算机仍处于 S0 状态。 若要支持这种新行为，必须将 D3hot 和 D3cold 显式定义为 D3 的不同 substates。

D3hot 是 D3 的唯一子类型，设备可以直接从 D0 进入。 设备驱动程序在软件控制下从 D0 转换为 D3hot。 在 D3hot 中，可以在它连接到的总线上检测到设备。 当设备处于 D3hot 子状态时，总线必须保持 D0 状态。 在 D3hot 中，设备可以返回到 D0 或输入 D3cold。 只能在 D3hot 中输入 D3cold。

D3cold 是 D3 的子状态，其中设备在物理上连接到总线，但无法检测到总线上的设备， (即，直到再次打开设备) 。 在 D3cold 中，以下一项或两项操作成立：

-   设备连接到的总线处于低功耗状态。
-   设备处于低功耗状态，当总线驱动程序尝试在总线上检测到其存在时，设备不会做出响应。

发生 D3hot 到 D3cold 的转换，但没有设备驱动程序交互。 相反，设备驱动程序会在启动从 D0 到 D3hot 的转换之前，指示它是否准备好 D3cold 转换。 接下来，可能会也可能不会发生 D3hot 到 D3cold 的转换，具体取决于是否所有条件都是启用此转换的权限。

两种情况是，使用同一电源的所有设备都在 D3hot 中，并准备好进行 D3cold 转换。 当这些设备的最后一个进入 D3hot 时，父总线驱动程序或 ACPI 筛选器驱动程序会关闭这些设备的电源，这就是说设备进入 D3cold。

位于 D3cold 中的设备只能通过输入 D0 来离开此子类型。 没有从 D3cold 到 D3hot 的直接转换。

如果计算机处于 S0 状态并且设备进入 D3hot 子状态，则设备驱动程序通常无法提前确定设备的下一个转换是 D3cold 还是 D0。 如果计算机正在准备离开 S0 状态，则会出现这种情况。 在这种情况下，下一次转换为 D3cold。

以下部分介绍了 D3hot 和 D3cold：

-   [D3hot 子情况](#d3hot)
-   [D3cold 子情况](#d3cold)

有关详细信息，请参阅 [支持驱动程序中的 D3cold](supporting-d3cold-in-a-driver.md)。

### <a name="d3hot-substate"></a><a href="" id="d3hot"></a>D3hot 子情况

D3hot 具有以下特征：

<a href="" id="power-consumption"></a>功率消耗  
通常从设备中删除电源，而不是从整个计算机中删除。 处于 S0 状态的计算机可能会在此状态下继续运行，或者可能正在准备从 S0 移动到低功耗 Sx 状态。

<a href="" id="device-context"></a>*设备上下文*  
设备驱动程序只负责还原设备上下文。 驱动程序必须保留并还原所有设备上下文，或者必须在转换为 D0 状态时重新初始化设备。

<a href="" id="device-driver-behavior"></a>*设备驱动程序行为*  
设备驱动程序只负责还原设备上下文，通常来自最新的工作配置。

<a href="" id="restore-time"></a>*还原时间*  
总还原时间是任何设备电源状态（D3cold 除外）的最大程度，但通常不会大于从 D2 还原时间。

<a href="" id="wake-up-capability"></a>*唤醒功能*  
D3hot 子状态中的设备可能会也可能不能请求唤醒。 若要提供有关此子情况是否可以支持唤醒信号的信息，总线驱动程序使用 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities) 结构，或从 Windows 8 开始，使用 [GUID \_ D3COLD \_ 支持 \_ 接口](https://msdn.microsoft.com/library/windows/hardware/hh967714) 驱动程序接口。

在 D3hot 中，只有最小滴当前可用。 驱动程序和硬件必须做好准备，找不到电源。 支持 D3hot 的总线规范通常会提供可在此状态下使用的电源的详细要求。 若要将设备恢复到工作状态，设备的驱动程序必须能够还原和重新初始化设备，而无需依赖于 BIOS 来运行选项 ROM 中可用于设备的任何代码。

父总线驱动程序将不会从任何输入 D3hot 的设备的父总线中删除系统电源，除非该计算机作为整体转换为 S0 状态。

设备的所有类都定义 D3hot 子类别。

### <a name="d3cold-substate"></a><a href="" id="d3cold"></a>D3cold 子情况

D3cold 具有以下特征：

<a href="" id="power-consumption"></a>功率消耗  
已完全从设备中删除电源，这可能是从整个系统中删除的。 设备可以根据其构造，从两侧的源绘制当前的。

<a href="" id="device-context"></a>*设备上下文*  
设备驱动程序只负责还原设备上下文。 驱动程序必须保留并还原设备上下文，或者必须在转换为 D0 状态时重新初始化设备。

<a href="" id="device-driver-behavior"></a>*设备驱动程序行为*  
设备驱动程序只负责还原设备上下文，通常来自最新的工作配置。

<a href="" id="restore-time"></a>*还原时间*  
总还原时间是设备电源状态的最大时间。

<a href="" id="wake-up-capability"></a>*唤醒功能*  
在 D3cold 子状态中，设备可能会触发唤醒信号来唤醒睡眠计算机。 此功能在 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构中报告，并从 Windows 8 开始，由 [GUID \_ D3COLD \_ 支持 \_ 接口](https://msdn.microsoft.com/library/windows/hardware/hh967714)驱动程序接口中的 [*GetIdleWakeInfo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-get_idle_wake_info)例程来处理。 在信号唤醒计算机之后，设备驱动程序将启动设备从 D3cold 到 D0 的转换。 有关详细信息，请参阅下面的备注。

从 Windows 8 开始，D3cold 子状态下的设备可能能够触发到处于 S0 系统电源状态的计算机的唤醒信号。 此功能由 *GetIdleWakeInfo* 例程报告。 **设备 \_ 功能** 结构不包含有关此功能的信息。 唤醒信号到达后，设备驱动程序将启动设备从 D3cold 到 D0 的转换。 在这种情况下，计算机在信号到达时处于唤醒状态，并且只有设备需要唤醒。

在许多现有硬件平台中，处于低功耗 Dx 状态的设备可以触发唤醒信号唤醒睡眠计算机。 但是，如果计算机正在 S0 状态下运行，则相同的设备可能无法触发唤醒信号。 因此，当计算机处于 S0 状态时，此设备的驱动程序不能启动设备从 D0 到低功耗 Dx 状态的转换。 否则，在设备保留 D0 后，它将不可用，直至计算机离开 S0 状态。 仅当计算机准备离开 S0 状态时，此设备才会保留 D0 状态。

如果处于低功耗 Dx 状态的设备可以触发到在 S0 状态下运行的计算机的唤醒信号，则当计算机处于 S0 状态时，设备不需要保持 D0。 如果计算机处于 S0 状态，并且设备处于 D0 状态，但处于空闲状态，则驱动程序可以对设备进行 arm 以触发唤醒信号，并启动设备从 D0 到此低功耗 Dx 状态的转换。

某些设备类定义 D3cold 子类别。

有关详细信息，请参阅 [支持驱动程序中的 D3cold](supporting-d3cold-in-a-driver.md)。

 

