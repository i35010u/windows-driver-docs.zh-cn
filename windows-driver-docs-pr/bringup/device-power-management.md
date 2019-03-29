---
title: 设备电源管理
description: ACPI 5.0 规范定义一组命名空间对象来指定设备的设备电源信息。
ms.assetid: F57AD5A0-F459-4A20-BDBE-87C30CF957B3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc8b420f2d84b7c9342bfab10303f761dfc22da3
ms.sourcegitcommit: 3cdabbe0af52459e484e093a9e11da8f5312daf6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2019
ms.locfileid: "58441930"
---
# <a name="device-power-management"></a>设备电源管理

[ACPI 5.0 规范](https://www.uefi.org/specifications)定义一组命名空间对象来指定设备的设备电源信息。 例如，一组对象可以指定设备需要每个受支持的设备电源状态下的能源。 另一种对象类型可以描述从低功耗状态对硬件事件的响应唤醒设备的能力。

## <a name="device-power-management-in-windows"></a>在 Windows 中的设备电源管理

系统运行时 （即，在系统处于 ACPI 定义的工作状态，S0），各个设备可以设备电源状态，具体取决于活动，以节约电源之间进行转换。 在传统 PC 系统中，ACPI 定义进入睡眠状态 (S1 到 S4) 还用来保存功能，但这些已断开连接、 高延迟的睡眠状态不使用 Windows SoC 平台。 因此，电池使用寿命是高度依赖于平台如何实现运行时设备电源管理。

集成到 SoC 的设备可以是通过 Windows 电源框架 (PoFx) 的电源管理。 这些框架集成设备是由知道 SoC 的电源和时钟控件的详细信息通过特定于 SoC 的 power 引擎插件 (microPEP) PoFx 电源管理。 有关 PoFx 详细信息，请参阅[电源管理框架概述](https://msdn.microsoft.com/library/windows/hardware/hh406637)。

对于未集成到 SoC 的外围设备，Windows 使用 ACPI 设备电源管理。 对于这些 ACPI 托管的设备，设备驱动程序堆栈 （通常的函数或类驱动程序） 中的电源策略所有者做出设备电源状态转换决策，并[Windows ACPI 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540493)，Acpi.sys，调用 ASL 控件若要应用所需的特定于平台的功率控制的方法。

> [!NOTE]
> 可以和某些设备堆栈，使用 ACPI 设备电源管理-、 单独或组合使用 microPEP — 在 SoC 设备电源管理的。

如中所述[ACPI 中的设备电源管理](https://docs.microsoft.com/windows-hardware/drivers/bringup/device-power-management#device-power-management-in-acpi)，Windows 支持 ACPI 5.0 规范中定义的 D3cold 电源管理功能。 通过使用这种支持，设备、 平台和驱动程序可以参加于完全在运行时空闲期间删除的设备电源。 此功能可以显著提高的电池使用寿命。 但是，删除 power 必须受所有受影响的组件以便能够成功地返回到 D0。 出于此原因，驱动程序 （总线和函数） 以及平台本身，将必须指示支持它。 有关 D3cold 驱动程序选择加入的详细信息，请参阅[驱动程序中支持 D3cold](https://msdn.microsoft.com/library/windows/hardware/hh967717)。

## <a name="device-power-management-in-acpi"></a>ACPI 中的设备电源管理

Namespace 设备支持最多四个设备的电源状态，编号 D0 （全功能或"启用"） 到 D3 (没有正常工作，或"off")。 每种状态可以有不同的电源要求具有更高的状态编号较低的状态比降低能源消耗。 此外，D3 （关闭） 状态有两种子状态，D3hot 和 D3cold。 D3hot 子状态要求设备保持在其父总线上进行访问，以便它可以响应总线特定的软件的命令。 D3cold 中删除此要求，以及用于满足的能力。 最后，了解设备唤醒本身从低功耗状态由于硬件事件，并且如有必要，还将从空闲状态的平台。

平台通过授予操作系统控制的指示其支持的 D3cold"\_PR3 支持"功能 （位 2） 时使用的平台范围 OSPM 功能方法请求。 详细信息，请参阅部分 6.2.10.2，"平台范围 OSPM 功能"中[ACPI 5.0 规范](https://www.uefi.org/specifications)。

电源管理的设备使用子对象来描述其对操作系统的电源功能。 以下部分介绍这些功能和对象。

### <a name="power-resources-and-states"></a>能源和状态

设备通过列出的一套 power 资源需要才能在该状态下无法声明它对电源状态的支持。 ACPI Power 资源表示电源设备和驱动器它们的时钟信号的电压导轨。 这些资源声明的命名空间的根处。 每个 power 资源已\_ON 和一个\_方法通过其控制它，请关闭和\_STA 方法来报告其状态。 有关详细信息，请参阅 》 的部分 7.1 中，"声明 Power 资源对象"， [ACPI 5.0 规范](https://www.uefi.org/specifications)。

[Windows ACPI 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540493)，Acpi.sys，监视之间共享资源，设备的电源依赖关系，并为这些设备切换电源状态，可确保只有实际需要的 power 资源在任何特定时间启用设备。

#### <a name="power-resource-requirements-prx"></a>支持资源要求 (\_PRx)

没有 Power 资源要求 (\_PRx) 对象，其中 x = 0、 1、 2 或 3，为每个受支持的设备电源状态。 如果设备驱动程序决定过渡到新的电源状态，Acpi.sys 可确保任何所需的新状态的能源开启，并且无法再中使用的任何资源已经关闭。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>支持的设备状态</th>
<th>要使用的资源要求对象</th>
<th>要包括在要求对象中的资源</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>D0 （必需）</td>
<td>_PR0</td>
<td><p>所有电源线和时钟的设备的完整功能所需的。</p></td>
</tr>
<tr class="even">
<td>D1</td>
<td>_PR1</td>
<td><p>任何电源或时钟功能所需的类定义减少-此状态。</p></td>
</tr>
<tr class="odd">
<td>D2</td>
<td>_PR2</td>
<td><p>任何电源或时钟功能所需的类定义减少-此状态。</p></td>
</tr>
<tr class="even">
<td>D3hot （必需）</td>
<td>_PR2</td>
<td><p>相同的资源是受支持 （D2、 D1，还是 D0） 的下一个更高版本状态。</p></td>
</tr>
<tr class="odd">
<td>D3cold</td>
<td>_PR3</td>
<td><p>仅 power 或所需的设备显示在其总线上并响应总线特定命令的时钟。</p></td>
</tr>
</tbody>
</table>

 > [!NOTE]
 > 如果在特定平台支持 D3cold 功能，并且设备的设备驱动程序选择在中 D3cold，设备到\_PR3 power 资源将如果它们未使用任何其他设备，已关闭过渡到 D3hot 后一段时间。

有关支持 D3cold 的设备的 power 资源要求的详细信息，请参阅[D3cold 固件要求](firmware-requirements-for-d3cold.md)。

#### <a name="device-power-state-psx"></a>设备电源状态 (\_PSx)

提供了一个电源状态方法， \_PSx，其中 x = 0、 1、 2 或 3，为每个受支持的设备电源状态 Dx。 此方法是可选的但是，如果存在，它调用电源资源的状态都被关闭之前和之后已打开电源资源的状态。 \_PSx 旨在执行围绕电源周期所需的任何特定于平台的操作。 \_PSx 必须访问分配给功能驱动程序的设备注册、 访问总线标准寄存器的已分配到总线驱动程序，或打开或关闭，这是预留给 Acpi.sys 操作切换 power 资源。

### <a name="wake-capabilities"></a>唤醒功能

电源管理的设备可能能够检测在低功耗状态时的事件，并导致需要半夜起来处理它们的平台。 若要启用此功能，Windows 需要的平台和设备的功能的信息。

#### <a name="sx-device-wake-state-sxw"></a>Sx 设备唤醒状态 (\_SxW)

在给定平台上，没有特定支持唤醒功能的设备状态和可响应唤醒事件的系统状态之间映射。 ACPI 定义\_SxW 对象，将此信息提供给操作系统。 对于每个受支持的系统电源状态，Sx SxW 对象时。 由于始终位于 S0 SoC 平台，现在所关注的唯一对象是\_S0W。 此对象指定平台的功能，可以从以设备的唤醒信号响应低能耗空闲状态唤醒。 该对象由 Windows 用于确定设备的目标 D 状态期间系统低能耗空闲状态。 有关详细信息\_S0W，请参阅部分 7.2.20，"\_S0W （S0 设备唤醒状态）"，在[ACPI 5.0 规范](https://www.uefi.org/specifications)。

对于大多数 SoC 平台，设备主动电源管理到 D3 状态时处于空闲状态，并且系统可以在设备处于此状态时，从低能耗空闲状态唤醒。 对于此类系统， \_S0W 对象返回 3 （或 4，如果它还支持 D3cold）。 但是，可以将任何 D 状态指定为最低提供支持的可唤醒状态，并且某些设备类或总线使用不同的值。 例如，SDIO 和 USB 连接设备使用此状态状态 D2。

> [!NOTE]
> 为了便于从 Windows 7 到 Windows 8 或 Windows 8.1 的设备驱动程序的迁移，你的设备可能需要提供\_S4W 也。 目前，有这样的要求的唯一设备类网络 (Ndis.sys)。

#### <a name="wake-capable-interrupts-crs"></a>支持唤醒的中断 (\_CRS)

设备的资源描述指示设备是否能够检测并通过将标记为"唤醒能够"中断信号发生唤醒事件 （ExclusiveAndWake 或 SharedAndWake）。 Windows 和设备驱动程序提供的此类中断以确保在启用设备转换到低功耗状态时的特殊处理。 详细信息，请参阅部分 6.4.3.6、"扩展中断描述符"和部分 6.4.3.8.1，"GPIO 连接描述符"中的中断和 GpioInt 资源描述符的说明的[ACPI 5.0 规范](https://www.uefi.org/specifications).

### <a name="wake-enablement"></a>唤醒启用

具体取决于用户方案或系统策略，唤醒功能的设备可能会或可能不实际上拥有唤醒。 因此，支持唤醒的中断可能会或可能未在设备处于空闲状态时启用。 除了启用中断，Windows 使用以下机制来启用唤醒设备。

#### <a name="device-sleep-wake-dsw"></a>设备睡眠状态唤醒 (\_DSW)

ACPI 定义\_DSW 对象作为一种方法以通知有关下一步睡眠或低能耗空闲期过后 ACPI 平台固件的操作系统。 此对象是可选的并在平台都需要预先配置特定于平台的唤醒硬件时才使用。 目标设备的 D 状态和系统的目标 S 状态都是提供。 D 状态和 S 状态组合将始终遵守与所提供的设备的信息\_SxW 对象。

#### <a name="power-resources-for-wake-prw"></a>唤醒 power 资源 (\_PRW)

在某些情况下，其他的电源资源必须打开要为唤醒启用的设备。 在这种情况下，设备可以提供\_PRW 对象，若要列出这些其他的电源资源。 [Windows ACPI 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540493)、 Acpi.sys，将根据正常情况下管理这些电源资源，否则确保，它们开启时它们所需的设备 （即，唤醒功能的设备），并且已关闭。

\_PRW 也用于定义唤醒功能的传统 （完整 ACPI 硬件） 的 PC 平台。
