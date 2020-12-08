---
title: 启动环境中 Windows 10 移动版的电池充电
description: 启动环境中 Windows 10 移动版的电池充电
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b15e4556ea706954426476166a1a3ab790a71ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789163"
---
# <a name="battery-charging-in-the-boot-environment-for-windows-10-mobile"></a>启动环境中 Windows 10 移动版的电池充电

对于运行 Windows 10 移动版的设备，Oem 从 SoC 供应商接收的 BSP 包含为 SoC 供应商的硬件专门设计的 UEFI 充电驱动程序。 通常，Oem 会修改此驱动程序，以便对其硬件进行自定义。

如果此驱动程序设计为与 Microsoft 提供的 UEFI 电池充电驱动程序配合使用，则驱动程序将实现 [uefi 电池充电协议](uefi-battery-charging-protocol.md)，而 Microsoft UEFI 电池充电应用程序使用此协议与驱动程序通信。

另外，Oem 还可以选择实现自己使用的、而不是 Microsoft 应用程序的 UEFI 电池充电应用程序。 在此方案中，UEFI 电池充电驱动程序不得实现 [UEFI 电池充电协议](uefi-battery-charging-protocol.md)。 如果驱动程序实现此协议，Windows 启动管理器将加载 Microsoft UEFI 电池充电应用程序。

**注意**  本主题中的大部分信息适用于使用 Microsoft 提供的 UEFI 电池充电应用程序的设备。 本主题中的 " *uefi 电池充电应用程序* " 一词是指由 mobilestartup 加载的 uefi 电池充电库。 有关 mobilestartup 的详细信息，请参阅 [Boot AND UEFI](boot-and-uefi.md)。

## <a name="understanding-the-boot-battery-charging-process-provided-by-microsoft"></a>了解由 Microsoft 提供的启动电池充电过程

以下步骤描述了在使用 Microsoft 提供的 UEFI 电池充电应用程序的情况下，在启动过程中的充电过程：

1. 通过连接到电源或按用户按下电源按钮打开设备。

2. SoC 特定的固件启动加载程序将运行并执行以下操作之一：

    - 如果启动加载器检测到连接的电源，并且电池在设备中，则该设备会开始滴电池充电，并继续将启动到 UEFI 环境的启动管理器。

    - 如果启动加载程序未检测到电源，并且电池太少而无法启动到 UEFI 环境，则设备将关闭。

    - 如果启动加载程序检测到连接的电源，但设备中没有电池，则该设备继续进入 UEFI 环境到 UEFI 电池充电应用程序。 当应用程序尝试对电池充电时，UEFI 电池充电驱动程序将向应用程序返回一个错误，指示未检测到电池。 应用程序通过显示错误 UI 并关闭设备来处理此错误。 有关详细信息，请参阅 [Microsoft 提供的 UEFI 电池充电应用程序的体系结构](architecture-of-the-uefi-battery-charging-application.md)。

3. 启动管理器运行电池充电应用程序。

    - 如果设备检测到连接的电源，则设备将进入电池充电模式。 使用 UEFI 充电驱动程序和 UEFI USBFn 驱动程序对电池充电应用程序接口来对电池充电。 有关详细信息，请参阅 [UEFI 电池充电协议](uefi-battery-charging-protocol.md)。

    - 如果设备未检测到连接的电源，并且电池太少而无法启动到主操作系统，则设备将关闭。

4. 根据 OEM 可自定义的注册表值的值，电池充电应用程序将在设备达到阈值后继续执行启动过程，或等待用户在执行此操作之前保留电源按钮。

下图说明了启动电池充电过程中涉及的组件。 此关系图有意省略了许多 UEFI 组件，以将精力集中在电池充电过程上;有关 UEFI 引导过程的更全面的视图，请参阅 [boot 和 UEFI](boot-and-uefi.md)。

![预启动电池充电流量](images/oem-preboot-battery-flow.png)

## <a name="charging-states-supported-by-the-microsoft-provided-battery-charging-application"></a>收取 Microsoft 提供的电池充电应用程序支持的状态

当启动电池充电过程到达 UEFI 电池充电应用程序时，设备可以输入几个不同的状态，具体取决于其配置方式。 这些状态称为 *阈值充电* 和 *充电*。

### <a name="threshold-charging"></a>阈值充电

下图显示了默认的启动电池充电进程。 在此过程中，设备将在电池达到特定阈值（称为 *启动到主操作系统阈值*）时立即启动到主操作系统。 有关在充电过程中定义的此阈值和其他阈值的详细信息，请参阅 [电池充电阈值](#battery-charging-thresholds)。

![阈值充电预启动电池流量](images/oem-preboot-battery-flow-threshold-charging.png)

以下步骤演示了这种充电过程的相应 UI 流：

1. 如果电池电量不足，无法满足 *启动到主操作系统* 阈值的要求，则设备将在以下电池电量不足的 UI 屏幕之间交替10秒。 如果用户在10秒的时间间隔内按下 "电源" 按钮，则设备将继续在以下电池电量不足的 UI 屏幕之间切换，增加10秒。

    ![显示电池电量不足的屏幕截图。](images/oem-battery-charge-ui-empty-red.png)
    ![显示电源插头电量不足的屏幕截图。](images/oem-battery-charge-ui-plug-red.png)

2. 如果设备空闲10秒钟，设备将关闭显示器。

    ![显示黑屏的屏幕截图。](images/oem-battery-charge-ui-black.png)

3. 设备进入 *主操作系统* 阈值后，将显示 OEM 启动徽标，并启动到主操作系统。 下面的屏幕快照演示了一个示例 OEM 启动徽标。

    ![屏幕截图，显示电池电量不足 O E M 徽标。](images/oem-battery-charge-ui-oem-logo.png)

### <a name="power-off-charging"></a>断电

Windows 10 支持在设备从用户的角度看来关闭时对电池充电。 此功能称为 " *断电*"。 本文档未来版本中将提供有关如何启用此功能的信息。

> [!IMPORTANT]
> 只能在生成设备映像时配置电源关充电。 Windows 10 操作系统并不为用户提供启用或禁用充电的方式。

如果启用了断电，则即使达到 " *启动到主操作系统* " 阈值，设备仍会受到电池充电应用程序的控制。 设备将保持此状态，直到用户按住电源按钮2秒钟或更长时间才能将设备启动到主操作系统。

即使启用了断电，用户也不会始终经历断电的充电路径。 如果设备重新启动 (例如，由于更新，或者系统语言设置在它处于开启状态并连接到电源时) 更改，则设备将跳过关闭充电模式，并在达到预启动充电阈值后直接启动到主操作系统。 如果用户按住电源按钮重新启动设备并将其连接到电源，则也会跳过电源充电模式。

下图显示了启用电源充电时的启动电池充电进程。

![关机时的预启动电池流量](images/oem-preboot-battery-flow-power-off-charging.png)

以下步骤说明启用了断电功能时相应的 UI 流：

1. 如果电池的电量不足，无法满足 *启动到主操作系统* 阈值的要求，则设备将在10秒内交替使用以下红色电池电量不足 UI 屏幕。 如果用户在10秒的时间间隔内按下 "电源" 按钮，则设备将继续在以下电池电量不足的 UI 屏幕之间切换，增加10秒。

    ![屏幕截图，显示白色电池电量低。](images/oem-battery-charge-ui-empty-red.png)
    ![屏幕截图，显示带有电源插头的白色和红色低电池。](images/oem-battery-charge-ui-plug-red.png)

2. 如果设备空闲10秒钟，设备将关闭显示器。

    ![电池电量不足黑色](images/oem-battery-charge-ui-black.png)

3. 在设备达到 " *启动到主操作系统* " 阈值后，设备将在10秒内交替使用以下电池电量低 UI 屏幕，而不是直接启动到主操作系统。 如果用户按下此10秒间隔内的短 duraction 的电源按钮 (不到2秒) ，则设备将继续在以下电池电量不足的 UI 屏幕之间切换，增加10秒。

    ![显示白色和黑色电量不足 UI 的屏幕截图。](images/oem-battery-charge-ui-empty-white.png)
    ![屏幕截图，显示具有电源插件 UI 的白色和黑色低电池。](images/oem-battery-charge-ui-plug-white.png)

4. 如果设备空闲10秒钟，设备将关闭显示器。

    ![电池电量不足黑色](images/oem-battery-charge-ui-black.png)

5. 如果用户按下 "电源" 按钮2秒或更长时间，则设备将显示 OEM 启动徽标，并启动到主操作系统。 下面的屏幕快照演示了一个示例 OEM 启动徽标。

    ![电池电量不足 oem 徽标](images/oem-battery-charge-ui-oem-logo.png)

## <a name="battery-charging-thresholds"></a>电池充电阈值

Microsoft 定义了几个电池充电阈值，以确保正确的电池充电用户体验。 其中部分阈值必须由 OEM 实现，以确保电池充电行为正确。 下图说明了如何将每个充电阈值组合在一起 (不绘制此关系图来) 缩放。

![预启动电池充电阈值](images/oem-preboot-battery-charging-thresholds.png)

关系图的左侧显示了在设备充电时影响用户体验的所有阈值，关系图的右侧显示了在设备放电时影响用户体验的所有阈值。 下表描述了每个阈值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>阈值</th>
<th>描述</th>
<th>配置指南</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>固件充电阈值</p></td>
<td><p>这是设备从基于硬件的充电启动到基于固件的充电时的阈值。 在硬件充电阶段，有必要将设备放在硬件充电阶段，以便在电池太低无法启动到固件时进行充电和保护。</p></td>
<td><p>Oem 必须将此阈值设置为低于 <em>启动到 UEFI 阈值</em>。 有关如何修改此阈值的详细信息，请联系 SoC 供应商。</p></td>
</tr>
<tr class="even">
<td><p>启动到 UEFI 阈值</p></td>
<td><p>这是设备从基于固件的充电启动到基于 UEFI 的收费 (的阈值，由 Microsoft) 提供。 需要将设备放在固件充电阶段，以便在电池电量过低时对电池充电，使其无法启动到固件。</p></td>
<td><p>Oem 必须将此阈值设置为高于 <em>固件充电阈值</em>，但低于 <em>启动到主操作系统</em> 阈值。 有关如何修改此阈值的详细信息，请联系 SoC 供应商。</p></td>
</tr>
<tr class="odd">
<td><p>启动到主操作系统阈值</p></td>
<td><p>这是在 <em>阈值充电模式下</em>，设备从基于 UEFI 的充电到主操作系统的启动阈值。 需要将设备放在 UEFI 收费阶段，以便在电池电量过低时对电池充电，使其无法启动到主操作系统。</p></td>
<td><p>Oem 必须将此阈值设置为高于 <em>启动到 UEFI 阈值</em> 和 <em>主 OS 关闭阈值</em>。 此阈值以电池的全部容量的百分比来定义。 默认情况下，此值设置为7%。 本文档未来版本中将提供有关如何设置此阈值的信息。</p></td>
</tr>
<tr class="even">
<td><p>启动以更新 OS/设备重置阈值</p></td>
<td><p>这是设备从基于 UEFI 的充电到更新操作系统或设备重置模式启动时的阈值。 需要将设备置于 UEFI 收费阶段，以便在电池电量过低时对电池充电，以维持更新或设备重置过程。</p></td>
<td><p>此阈值设置为 <em>启动到主操作系统阈值</em> + 8%。</p></td>
</tr>
<tr class="odd">
<td><p>电池已满</p></td>
<td><p>这是电池在其全部容量的100% 时的阈值。 在此阈值下，系统托盘中的电池图标显示电池电量装满图标。</p></td>
<td><p>Oem 应校准其电池配置文件，以便该设备始终可以达到电池电量的全部容量。</p></td>
</tr>
<tr class="even">
<td><p>电池保护程序阈值</p></td>
<td><p>如果用户已设置节电功能，则此阈值为自动启用节电功能的阈值。</p></td>
<td><p>此阈值设置为电池全部容量的20%，并且不能由 OEM 更改。</p></td>
</tr>
<tr class="odd">
<td><p>主操作系统警告阈值</p></td>
<td><p>这是设备向用户显示电池电量不足的通知的阈值。</p></td>
<td><p>此阈值设置为电池的全部容量的10%，这不能由 OEM 更改。</p></td>
</tr>
<tr class="even">
<td><p>主 OS 关闭阈值</p></td>
<td><p>这是软件安全关闭设备的阈值。 需要防止系统内存损坏。</p></td>
<td><p>OEM 必须将此阈值设置为低于 <em>启动到主操作系统阈值</em> ，并且低于 <em>主操作系统警告阈值</em>。 此外，此阈值必须大于或等于2%。 此阈值由<a href="/windows/desktop/Power/battery-information-str" data-raw-source="[BATTERY_INFORMATION](/windows/desktop/Power/battery-information-str)">BATTERY_INFORMATION</a>结构的<strong>DefaultAlert1</strong>成员定义。 有关如何修改此阈值的详细信息，请联系 SoC 供应商。</p></td>
</tr>
<tr class="odd">
<td><p>硬件关闭阈值</p></td>
<td><p>这是硬件强制设备关机的阈值。 需要确保电池电量过低。</p></td>
<td><p>此阈值由 SoC 供应商设置，不应由 OEM 更改。</p></td>
</tr>
</tbody>
</table>

## <a name="related-topics"></a>相关主题

[Microsoft 提供的 UEFI 电池充电应用程序的体系结构](architecture-of-the-uefi-battery-charging-application.md)  
[启动和 UEFI](boot-and-uefi.md)
