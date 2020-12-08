---
title: 设备电源管理
description: ACPI 6.3 规范定义一组命名空间对象，以指定设备的设备电源信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c8ce50afb4e3c02512bffbc035e016468cf4212
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789117"
---
# <a name="device-power-management"></a>设备电源管理

[ACPI 6.3 规范](https://uefi.org/specifications)定义一组命名空间对象，以指定设备的设备电源信息。 例如，一组对象可以指定设备在每个受支持的设备电源状态下所需的电源资源。 另一种对象类型可以描述设备从低功耗状态唤醒以响应硬件事件的能力。

## <a name="device-power-management-in-windows"></a>Windows 中的设备电源管理

当系统正在运行 (即，系统处于 ACPI 定义的工作状态 S0) 中，单个设备可在设备电源状态之间进行转换，具体取决于活动，省电。 在传统的 PC 系统中，ACPI 定义的休眠状态 (S1 到 S4) 还用于节省电能，但这些断开连接，高延迟睡眠状态不会在 Windows SoC 平台上使用。 因此，电池寿命很大程度上取决于平台如何实现运行时设备电源管理。

集成到 SoC 的设备可以通过 Windows Power Framework (PoFx) 进行电源管理。 这些集成了框架的设备通过 PoFx 通过 SoC 特定的 power engine 插件进行管理， (microPEP) 了解 SoC 的电源和时钟控制的细节。 有关 PoFx 的详细信息，请参阅 [电源管理框架概述](../kernel/overview-of-the-power-management-framework.md)。

对于未集成到 SoC 的外围设备，Windows 将使用 ACPI 设备电源管理。 对于这些 ACPI 管理的设备，设备驱动程序堆栈中的电源策略所有者通常 (功能或类驱动程序) 进行设备电源状态转换决定，并且 [WINDOWS ACPI 驱动程序](../kernel/acpi-driver.md)Acpi.sys 调用 ASL 控制方法，以应用所需的特定于平台的电源控制。

> [!NOTE]
> 对于基于 SoC 的设备电源管理，和某些设备堆栈可以使用 ACPI 设备电源管理（单独或与 microPEP 结合使用）。

如 ACPI 中的 [设备电源管理](#device-power-management-in-acpi)中所述，Windows 支持在 acpi 5.0 规范中定义的 D3cold 电源管理功能。 通过使用此支持，设备、平台和驱动程序可以选择在运行时空闲期间完全删除设备电源。 此功能可以显著提高电池寿命。 但是，所有受影响的组件都必须支持断电才能成功返回到 D0。 出于此原因，驱动程序 (总线和函数) 以及平台本身必须指明它们是否支持。 有关 D3cold 驱动程序选择加入的详细信息，请参阅在 [驱动程序中支持 D3cold](../kernel/supporting-d3cold-in-a-driver.md)。

## <a name="device-power-management-in-acpi"></a>ACPI 中的设备电源管理

命名空间设备最多支持四个设备电源状态、已编号的 D0 (full-功能，或 "on" ) 到 D3 (no 函数或 "off" ) 。 每个状态都可以具有不同的电源要求，具有较高编号的省/市/自治区更少的省电。 此外，D3 (关闭) 状态具有两个子状态： D3hot 和 D3cold。 D3hot 子状态要求设备在其父总线上仍可访问，以便能够响应特定于总线的软件命令。 此要求以及用于满足此要求的功能在 D3cold 中被删除。 最后，在硬件事件发生的情况下，设备可以从低功耗状态唤醒，还可以在必要时使平台脱离空闲状态。

该平台通过在 \_ 使用平台范围的 OSPM 功能方法请求 "PR3 支持" 功能 (第2位) 的操作系统控制，来指示其对 D3cold 的支持。 有关详细信息，请参阅 [ACPI 5.0 规范](https://uefi.org/specifications)中的 6.2.10.2 "平台范围内的 OSPM 功能" 部分。

电源管理设备使用子对象来描述其操作系统的电源功能。 以下各节介绍了这些功能和对象。

### <a name="power-resources-and-states"></a>电源资源和状态

设备通过列出其所需的一组电源资源来声明其对电源状态的支持。 ACPI 电源资源代表电源设备以及用于驱动设备的时钟信号。 这些资源是在命名空间的根声明的。 每个电源资源都具有一个的 \_ ON 和 \_ OFF 方法，通过该方法可对其进行控制，并使用 \_ STA 方法报告其状态。 有关详细信息，请参阅 [ACPI 5.0 规范](https://uefi.org/specifications)的7.1 节 "声明电源资源对象"。

[WINDOWS ACPI 驱动程序](../kernel/acpi-driver.md)Acpi.sys 监视共享资源的设备之间的电源依赖关系，在这些设备在电源状态之间过渡时，可确保只有设备实际所需的电源资源在任何特定时间都处于开启状态。

#### <a name="power-resource-requirements-_prx"></a>电源资源要求 (\_ PRx) 

\_对于每个受支持的设备电源状态， () 对象的电源资源要求，其中 x = 0、1、2或3。 当设备驱动程序决定过渡到新的电源状态时，Acpi.sys 确保新状态所需的任何电源资源都已打开，并且关闭了任何不再使用的资源。

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
<td>需要 (D0) </td>
<td>_PR0</td>
<td><p>设备的完整功能所需的所有电源和时钟。</p></td>
</tr>
<tr class="even">
<td>D1</td>
<td>_PR1</td>
<td><p>此状态的类定义缩减功能所需的任何电源或时钟。</p></td>
</tr>
<tr class="odd">
<td>D2</td>
<td>_PR2</td>
<td><p>此状态的类定义缩减功能所需的任何电源或时钟。</p></td>
</tr>
<tr class="even">
<td>D3hot (必需) </td>
<td>_PR3</td>
<td><p>仅设备在其总线上显示和响应特定于总线的命令所需的电源或时钟。</p></td>
</tr>
</tbody>
</table>

 > [!NOTE]
 > 如果某个特定平台支持 D3cold 功能，并且设备的设备驱动程序在 D3cold 中，则设备的 \_ PR3 电源资源将（如果它们未被其他设备使用）在转换到 D3cold 后的某个时间关闭。

有关支持 D3cold 的设备的电源资源要求的详细信息，请参阅 [D3cold 的固件要求](firmware-requirements-for-d3cold.md)。

#### <a name="device-power-state-_psx"></a>设备电源状态 (\_ PSx) 

\_对于每个受支持的设备电源状态 Dx，都有一个电源状态方法 PSx，其中 x = 0、1、2或3。 此方法是可选的，但如果存在，则在关闭状态的电源资源之前调用，并在打开状态的电源资源后调用。 \_PSx 用于执行在电源周期前后所需的任何特定于平台的操作。 \_PSx 不得访问分配给函数驱动程序的设备寄存器，访问分配给总线驱动程序的总线标准寄存器，或打开或关闭电源资源，这是为 Acpi.sys 保留的操作。

### <a name="wake-capabilities"></a>唤醒功能

当处于低功耗状态时，电源管理设备可能能够检测事件，并导致平台唤醒来处理这些事件。 若要启用此功能，Windows 需要有关平台和设备功能的信息。

#### <a name="sx-device-wake-state-_sxw"></a>Sx 设备唤醒状态 (\_ SxW) 

在给定平台上，设备状态之间存在特定的映射，它们支持可响应唤醒事件的唤醒功能和系统状态。 ACPI 定义 \_ 用于向操作系统提供此信息的 SxW 对象。 每个受支持的系统电源状态为 Sx，都有一个 SxW 对象。 由于 SoC 平台始终处于 S0 中，因此此处仅有意义的对象是 \_ S0W。 此对象指定平台能够从低功耗空闲状态中唤醒，以响应设备的唤醒信号。 在系统低功耗空闲期间，Windows 使用对象来确定设备的目标 D 状态。 有关 S0W 的详细信息 \_ ，请参阅 \_ [ACPI 5.0 规范](https://uefi.org/specifications)中的 "S0W (S0 设备唤醒状态) " 部分。

对于大多数 SoC 平台，设备处于空闲状态时，会主动管理到 D3 状态，并且在设备处于此状态时，系统能够从低功耗状态中唤醒。 对于此类系统， \_ 如果 S0W 对象还支持 D3cold) ，则返回 3 (或4。 但是，任何 D 状态都可以指定为支持的最低唤醒状态，而某些设备类或总线则使用不同的值。 例如，通过 SDIO 和 USB 连接的设备，状态 D2 会处于此状态。

> [!NOTE]
> 为了便于从 Windows 7 向 Windows 8 或 Windows 8.1 迁移设备驱动程序，您的设备可能也需要提供 \_ S4W。 目前，具有此要求的唯一设备类是网络 ( # A0) 。

#### <a name="wake-capable-interrupts-_crs"></a>CRS)  (支持唤醒的中断 \_

设备的资源说明指示设备能够检测和发出唤醒事件，方法是将中断标记为 "可唤醒" ("ExclusiveAndWake" 或 "SharedAndWake") 。 Windows 和设备驱动程序提供了此类中断的特殊处理，以确保在设备转换为低功耗状态时启用这些中断。 有关详细信息，请参阅 [ACPI 5.0 规范](https://uefi.org/specifications)的 "扩展中断描述符" 一节中的中断和 GpioInt 资源描述符的说明，以及6.4.3.8.1，"GPIO 连接描述符" 一节。

### <a name="wake-enablement"></a>唤醒启用

根据用户方案或系统策略，支持唤醒的设备实际上可能是唤醒功能，也可能不是。 因此，在设备处于空闲状态时，可能会也可能不会启用支持唤醒的中断。 除了启用中断外，Windows 还使用以下机制在设备上启用唤醒。

#### <a name="device-sleep-wake-_dsw"></a>设备睡眠唤醒 (\_ DSW) 

ACPI 将 \_ DSW 对象定义为一种方法，以便操作系统向 ACPI 平台固件通知下一个睡眠或低功耗空闲时间。 此对象是可选的，仅当平台需要提前配置特定于平台的唤醒硬件时才使用。 同时提供了设备的目标 D 状态和系统的目标 S 状态。 D 状态和 S 状态组合将始终符合设备的 SxW 对象提供的信息 \_)  (s。

#### <a name="power-resources-for-wake-_prw"></a>用于唤醒 (PRW 的功率资源 \_) 

在某些情况下，必须打开其他电源资源，才能启用唤醒设备。 在这种情况下，设备可以提供 \_ PRW 对象以列出这些额外的电源资源。 [WINDOWS ACPI 驱动程序](../kernel/acpi-driver.md)Acpi.sys 将按通常的方式管理这些电源资源，确保设备在需要设备时打开这些资源 (即启用了唤醒的设备) ，否则，这些资源将被关闭。

\_PRW 还用于定义传统 (完整 ACPI 硬件) PC 平台的唤醒功能。
