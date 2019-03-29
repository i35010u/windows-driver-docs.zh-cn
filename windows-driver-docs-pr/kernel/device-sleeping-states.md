---
title: 设备低功耗状态
description: 设备低功耗状态
ms.assetid: f594a63f-10ce-439d-abe3-d342555d98f0
keywords:
- 设备电源状态 WDK 内核
- 设备低功耗状态 WDK 电源管理
- 睡眠电源管理 WDK 内核
- Dx 名称 WDK 电源管理
- 睡眠状态的设备 WDK 电源管理
- 最低功率设备状态 WDK 内核
- highest-powered 设备低功耗状态 WDK 内核
- 中间的睡眠状态 WDK 内核
- 低能耗模式 WDK 内核
- 节能模式 WDK 内核
- 连续 power WDK 内核
- 延迟 WDK 电源管理
- 状态转换会延迟 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6bb4590a1fa97a27dc4ea9bb834bc793e31f0b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565250"
---
# <a name="device-low-power-states"></a>设备低功耗状态





设备的电源状态 D1，D2 和 D3 是设备低功耗状态。 从 Windows 8 开始，D3 分为两个子状态[D3hot](#d3hot)并[D3cold](#d3cold)。

D1 和 D2 中间低功耗状态。 设备的许多类未定义这些状态。 所有设备都必须都定义 D3hot。

以下部分介绍 D1 和 D2，D3:

-   [设备电源状态 D1](#d1)
-   [设备电源状态更改为 D2](#d2)
-   [设备电源状态 D3](#d3)

### <a href="" id="d1"></a>设备电源状态 D1

设备电源状态 D1 是 highest-powered 设备低功耗状态。 它具有以下特征：

<a href="" id="power-consumption"></a>*功率消耗*  
消耗是小于在 D0 状态但大于或等于在 D2 状态。 通常情况下，D1 是设备接收到只需能力不足以保留设备的硬件上下文的网关时钟的状态。 通常情况下，支持 D1 总线或设备类的规范介绍更多详细信息中的此状态。

<a href="" id="device-context"></a>*设备上下文*  
一般情况下，设备上下文保留的硬件和驱动程序不需要还原。 通常支持 D1 总线或设备类的规范提供了有关保留此上下文的详细的要求。

<a href="" id="device-driver-behavior"></a>*设备驱动程序行为*  
驱动程序必须保存和还原或重新初始化的硬件丢失任何上下文。 通常情况下，但是，设备会丢失在进入此状态的上下文。

<a href="" id="restore-time"></a>*还原时间*  
一般情况下，若要将设备还原到 D0，D1 中所需的时间应早于来自 D2 还原到 D0。

<a href="" id="wake-up-capability"></a>*唤醒功能*  
D1 中的设备可能能够请求唤醒。 若要提供有关此状态是否可以支持唤醒信号的信息，总线驱动程序将使用[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构，或从 Windows 8 开始[GUID\_D3COLD\_支持\_接口](https://msdn.microsoft.com/library/windows/hardware/hh967714)驱动程序接口。

通常情况下，设备使用 D1 这样做，因为在此状态下恢复不需要还原设备的完整硬件上下文的驱动程序。 为了尽量减少延迟的用户的角度看，D1 中的设备还原到 D0 应该不会导致尽可能少的延迟。 最小化状态转换中的延迟是比降低能耗更重要。

### <a href="" id="d2"></a>设备电源状态更改为 D2

D2 是一种中间设备低功耗状态具有以下特征：

<a href="" id="power-consumption"></a>*功率消耗*  
消耗是小于或等于的中的 D1 状态。

<a href="" id="device-context"></a>*设备上下文*  
一般情况下，大多数设备上下文会丢失的硬件。 通常情况下，此状态可保留用于发出信号唤醒事件上下文的一部分。 通常支持 D2 总线或设备类的规范提供了有关保留此上下文的详细的要求。

<a href="" id="device-driver-behavior"></a>*设备驱动程序行为*  
设备驱动程序必须保存和还原或重新初始化的硬件丢失任何上下文。 典型的设备将进入 D2 时失去大多数上下文。

<a href="" id="restore-time"></a>*还原时间*  
将设备 D2 还原到 D0 采用至少只要设备 D1 中还原到 D0。 有一个大型的帧缓冲区的图形适配器是设备的具有大量的硬件上下文，若要从 D2 转换到 D0 后还原的示例。 对于此类设备 D2 的还原时间可能远大于 D1 的还原时间。

<a href="" id="wake-up-capability"></a>*唤醒功能*  
D2 中的设备可能能够请求唤醒。 若要提供有关此状态是否可以支持唤醒信号的信息，总线驱动程序将使用[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构，或从 Windows 8 开始[GUID\_D3COLD\_支持\_接口](https://msdn.microsoft.com/library/windows/hardware/hh967714)驱动程序接口。

通常情况下，支持 D2 的驱动程序这样做，因为他们的设备不支持从 D3 唤醒。 对于这些设备，D2 状态的功耗降至最低的级别从其设备可以响应唤醒信号恢复中。 D1 状态，这实现以减少识别的用户的延迟，与实现 D2 状态中的目标是节省电量。 因此，D0 来自 D2 的还原时间通常超出了，从 D1 到 D0。 在 D2 状态下，例如，总线上的减少了的电源可能会导致关闭其部分功能，因此，需要额外的时间来重新启动，并将设备还原的设备。

设备的许多类未定义此状态。

### <a href="" id="d3"></a>设备电源状态 D3

D3 是最低功率设备低功耗状态。 所有设备都必须都支持此状态。

从 Windows 8 开始，操作系统将 D3 细分为两个单独且完全不同子状态的状态，D3hot 和 D3cold。 早期版本的 Windows 定义 D3 状态，但不是 D3hot 和 D3cold substates。 但是，所有版本的[PCI 总线电源管理接口规范](http://www.pcisig.com/specifications/conventional/)定义单独 D3hot 和 D3cold 子状态和版本 4 及更高版本的[高级配置和电源接口规范](https://go.microsoft.com/fwlink/p/?linkid=57185)定义 D3hot 和 D3cold substates。

虽然 Windows 8 之前的 Windows 版本没有显式定义 D3 D3hot 和 D3cold 子状态，但这些子状态存在隐式在这些早期版本的 Windows。 设备是隐式的 D3hot 子状态在中，如果设备处于显式 D3 状态，并且计算机处于 S0 系统电源状态。 D3hot，在设备连接到电源源 （尽管该设备可能配置为绘制低当前），并且可以检测到总线上设备的状态。 设备是隐式中的 D3cold 子状态中，如果它是显式 D3 状态，并且计算机处于低功耗 Sx 状态 （S0 以外的状态）。 在此隐式 D3cold 子状态，设备可能会收到最新，滴送但设备和计算机在有效地关闭之前发生唤醒事件时。

从 Windows 8 开始，设备可以进入和离开的 D3cold 子状态，在计算机仍处于 S0 状态时。 若要支持这一新行为，D3hot 和 D3cold 必须显式定义为 D3 的子状态的不同状态。

D3hot 是唯一子状态的 D3 的设备可以直接从 D0 输入。 设备向转换从 D0 D3hot 软件控制下的设备驱动程序。 在 D3hot，可以连接到总线上检测到设备。 设备的 D3hot 子状态时，在总线必须保持 D0 状态。 从 D3hot，设备可以返回到 D0 或输入 D3cold。 只能从 D3hot，可以输入 D3cold。

D3cold 是子状态的 D3 在其中以物理方式将设备连接到该总线但不能检测到总线上设备的状态，（即，直到再次打开设备）。 在 D3cold，一个或两个以下为 true:

-   设备连接到总线是在低功耗状态。
-   设备处于低功耗状态中的设备时，未响应总线驱动程序会尝试在总线上的其状态进行检测。

从 D3hot 转换为 D3cold 时无需设备驱动程序交互。 相反，设备驱动程序指示是否在准备它时进行 D3cold 转换之前启动从 D0 到 D3hot 的转换。 随后，从 D3hot 转换到 D3cold 可能或可能不会发生，具体取决于是否所有条件都正确启用这一转换。

两个此类条件是所有使用相同电源的设备位于 D3hot 和做好 D3cold 转换。 当这些设备的最后一个输入 D3hot 时，父总线驱动程序或 ACPI 筛选器驱动程序将关闭电源的这些设备，也就是采用设备输入 D3cold。

D3cold 中的设备可以将此 substate 仅通过输入 D0。 从 D3cold D3hot 到没有直接转换。

如果计算机处于 S0 状态，设备将进入 D3hot 子状态的设备驱动程序是通常无法事先确定设备的下一步转换将将 D3cold 或 D0。 一个例外情况是当计算机正在准备，以便保留 S0 状态。 在这种情况下下, 一步转换是 D3cold。

以下部分介绍 D3hot 和 D3cold:

-   [D3hot 子状态](#d3hot)
-   [D3cold 子状态](#d3cold)

有关详细信息，请参阅[驱动程序中支持 D3cold](supporting-d3cold-in-a-driver.md)。

### <a href="" id="d3hot"></a>D3hot 子状态

D3hot 具有以下特征：

<a href="" id="power-consumption"></a>*功率消耗*  
Power 主要删除从该设备，但不能从该计算机作为一个整体。 计算机处于 S0 状态，可能会继续在此状态下运行，或它可能正在准备从 S0 转为低功耗 Sx 状态。

<a href="" id="device-context"></a>*设备上下文*  
设备驱动程序是负责还原设备上下文。 该驱动程序必须保持一致，然后还原所有的设备上下文，或必须重新初始化后转换到 D0 状态的设备。

<a href="" id="device-driver-behavior"></a>*设备驱动程序行为*  
设备驱动程序用于还原设备上下文中，通常从最新的工作配置完全负责。

<a href="" id="restore-time"></a>*还原时间*  
总还原时间是最高的任何设备的电源状态，除了 D3cold，但通常不远大于来自 D2 的还原时间。

<a href="" id="wake-up-capability"></a>*唤醒功能*  
中的 D3hot 子状态的设备可能会或可能不能请求唤醒。 若要提供有关此子状态是否可以支持唤醒信号的信息，总线驱动程序将使用[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构，或从 Windows 8 开始[GUID\_D3COLD\_支持\_接口](https://msdn.microsoft.com/library/windows/hardware/hh967714)驱动程序接口。

在 D3hot，只有最少滴送当前是可用的。 驱动程序和硬件必须为没有 power 做好准备。 通常支持 D3hot 总线规范提供了有关可在此状态的电源的详细的要求。 若要将设备恢复为工作状态，设备的驱动程序必须能够还原并重新初始化具体取决于 BIOS 选项可能适用于设备的 ROM 中运行的任何代码而无需设备。

父总线驱动程序不会从任何设备都进入 D3hot，除非父总线删除系统电源作为整个转换为 S0 状态的计算机。

设备的所有类都定义的 D3hot 子状态。

### <a href="" id="d3cold"></a>D3cold 子状态

D3cold 具有以下特征：

<a href="" id="power-consumption"></a>*功率消耗*  
从设备和整个系统可能已完全删除电源。 设备可能能够绘制来源端外，具体取决于其构造当前。

<a href="" id="device-context"></a>*设备上下文*  
设备驱动程序是负责还原设备上下文。 该驱动程序必须保留，然后还原设备上下文或必须重新初始化后转换到 D0 状态的设备。

<a href="" id="device-driver-behavior"></a>*设备驱动程序行为*  
设备驱动程序用于还原设备上下文中，通常从最新的工作配置完全负责。

<a href="" id="restore-time"></a>*还原时间*  
总还原时间是最高的任何设备的电源状态。

<a href="" id="wake-up-capability"></a>*唤醒功能*  
中的 D3cold 子状态，设备可能能够触发唤醒睡眠计算机的唤醒信号。 此功能以报告[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)结构，然后通过使用 Windows 8 中，启动[ *GetIdleWakeInfo*](https://msdn.microsoft.com/library/windows/hardware/hh967712)例程中[GUID\_D3COLD\_支持\_接口](https://msdn.microsoft.com/library/windows/hardware/hh967714)驱动程序接口。 信号中唤醒计算机后，设备驱动程序将启动从 D3cold D0 到的设备的转换。 有关详细信息，请参阅以下备注。

从 Windows 8 开始，在 D3cold 子状态的设备可能能够触发到 S0 系统电源状态的计算机的唤醒信号。 此功能报告的*GetIdleWakeInfo*例程。 **设备\_功能**结构不包含有关此功能的信息。 唤醒信号到达后，设备驱动程序将启动从 D3cold D0 到的设备的转换。 在这种情况下，在计算机处于唤醒状态时收到信号，并仅在设备需要唤醒。

在许多现有的硬件平台，在低功耗 Dx 状态中的设备可以触发唤醒睡眠计算机的唤醒信号。 但是，在同一设备可能不能在 S0 状态中运行的计算机的情况下触发唤醒信号。 因此，此设备的驱动程序不能启动从 D0 到低功耗 Dx 状态的设备的转换时在计算机处于 S0 状态。 否则，设备离开 D0 之后，它将不可用计算机离开 S0 状态之前。 仅当计算机正在准备，以便保留 S0 状态时，此设备应将保留 D0 状态。

如果在低功耗 Dx 状态中的设备可以触发到运行在 S0 状态的计算机的唤醒信号，该设备不需要时在计算机处于 S0 保留在 D0。 如果计算机处于 S0，并且设备处于 D0 但处于空闲状态，该驱动程序可以 arm 设备来触发唤醒信号，并启动从 D0 到此低功耗 Dx 状态的设备的转换。

设备的某些类定义的 D3cold 子状态。

有关详细信息，请参阅[驱动程序中支持 D3cold](supporting-d3cold-in-a-driver.md)。

 

 




