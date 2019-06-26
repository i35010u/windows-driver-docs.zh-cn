---
title: 启动环境中 Windows 10 移动版的电池充电
description: 启动环境中 Windows 10 移动版的电池充电
ms.assetid: 5aa1ef68-6939-4896-aabd-d499ba23f89f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 228cc7c671f0b1fcb88cc95adcade6d7cd240051
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364633"
---
# <a name="battery-charging-in-the-boot-environment-for-windows-10-mobile"></a>启动环境中 Windows 10 移动版的电池充电

对于运行 Windows 10 移动版的设备，从 SoC 供应商接收 Oem BSP 包括 UEFI 电池充电驱动程序专为 SoC 供应商的硬件。 Oem 通常会修改此驱动程序进行自定义，为其硬件。

如果此驱动程序用于 UEFI 电池充电驱动程序提供的 Microsoft，该驱动程序实现处理[UEFI 电池充电协议](uefi-battery-charging-protocol.md)，并与 Microsoft UEFI 电池充电应用程序进行通信通过使用此协议的驱动程序。

或者，Oem 可能会根据需要实现自己 UEFI 电池充电应用程序而不是 Microsoft 应用程序使用。 在此方案中，UEFI 电池充电驱动程序必须实现[UEFI 电池充电协议](uefi-battery-charging-protocol.md)。 Windows 启动管理器将加载 Microsoft UEFI 电池充电应用程序，如果该驱动程序实现此协议。

**请注意**  大部分此主题中的信息适用于使用 UEFI 电池充电由 Microsoft 提供的应用程序的设备。 术语*UEFI 电池充电应用程序*本主题中引用 UEFI 电池充电 mobilestartup.efi 所加载的库。 有关 mobilestartup.efi 详细信息，请参阅[启动和 UEFI](boot-and-uefi.md)。

## <a name="understanding-the-boot-battery-charging-process-provided-by-microsoft"></a>了解启动电池充电由 Microsoft 提供的过程

以下步骤介绍使用 UEFI 电池充电由 Microsoft 提供的应用程序的设备在启动流程计费过程：

1. 设备已开机，通过连接到电源或由用户按下电源按钮。

2. 特定于 SoC 的固件引导加载程序运行，并执行以下操作之一：

    - 如果启动加载器检测到已连接的电源，电池是在设备中设备开始滴送充电电池，并将继续引导到 UEFI 环境到启动管理器。

    - 如果引导加载程序不会检测在电源，电池电量过低，为到 UEFI 环境启动设备关闭。

    - 如果启动加载器检测到已连接的电源，但在设备中没有的电池，设备将继续引导到 UEFI 环境到 UEFI 电池充电应用程序。 当应用程序尝试为电池充电时，UEFI 电池充电驱动程序将返回到应用程序，以指示未检测到电池错误。 应用程序通过显示一条错误 UI 并关闭该设备来处理此错误。 有关详细信息，请参阅[UEFI 电池充电由 Microsoft 提供的应用程序的体系结构](architecture-of-the-uefi-battery-charging-application.md)。

3. 启动管理器运行电池充电应用程序。

    - 如果设备检测到已连接的电源，则设备将进入电池充电模式。 与 UEFI 电池充电驱动程序和 UEFI USBFn 驱动程序给电池充电的电池充电应用程序接口。 有关详细信息，请参阅[UEFI 电池充电协议](uefi-battery-charging-protocol.md)。

    - 如果设备不会检测已连接的电源，电池电量过低，启动到主要 OS 设备会关闭。

4. 根据 OEM 可自定义的注册表值的值，电池充电或者应用程序的设备达到阈值，或等待用户这样做之前，一直按住电源按钮后继续执行启动过程。

下图阐释了这一点与启动电池充电过程涉及的组件。 此关系图有意省略了许多 UEFI 组件将焦点置于电池充电进程;有关 UEFI 引导过程的更全面地了解，请参阅[启动和 UEFI](boot-and-uefi.md)。

![预启动电池充电流](images/oem-preboot-battery-flow.png)

## <a name="charging-states-supported-by-the-microsoft-provided-battery-charging-application"></a>计费支持由 Microsoft 提供的电池充电应用程序状态

当启动电池充电过程达到 UEFI 电池充电应用程序时，设备可以输入多个不同的状态，具体取决于其配置方式。 这些状态称为*阈值充电*并*关闭电源充电*。

### <a name="threshold-charging"></a>收费的阈值

下图显示了默认启动电池充电过程。 在此过程中，设备启动到主要 OS 电池电量达到特定阈值，调用时，就立即*启动到 Main OS 阈值*。 有关此设置和定义为电池充电过程的一部分其他阈值的详细信息，请参阅[电池充电阈值](#battery-charging-thresholds)。

![预启动阈值充电的电池流](images/oem-preboot-battery-flow-threshold-charging.png)

以下步骤演示了此计费过程的相应 UI 流：

1. 如果电池不具有足够的费用，以满足*启动到 Main OS*阈值，为 10 秒以下的电池电量不足用户界面屏幕之间交替的设备。 如果用户在此 10 的第二个间隔内按电源按钮，设备将继续之间交替变化以下的电池电量不足用户界面屏幕额外的 10 秒。

    ![前启动阈值的电池电量不足屏幕](images/oem-battery-charge-ui-empty-red.png)![前启动阈值的电池电量不足屏幕](images/oem-battery-charge-ui-plug-red.png)

2. 如果设备处于空闲状态 10 秒，设备会关闭显示器。

    ![电池电量不足屏幕黑色](images/oem-battery-charge-ui-black.png)

3. 设备到达后*启动到 Main OS*阈值、 设备显示 OEM 启动徽标和前的主操作系统启动。 下面的屏幕截图演示了示例 OEM 启动徽标。

    ![电池电量不足屏幕 oem 徽标](images/oem-battery-charge-ui-oem-logo.png)

### <a name="power-off-charging"></a>打开 / 关闭收费

Windows 10 支持的功能时从用户的角度来看关闭该设备将显示为电池充电。 此功能被称为*关机充电*。 将此文档的未来版本中提供有关如何启用此功能的信息。

> [!IMPORTANT]
> 生成的设备映像时可以仅配置关闭电源收费。 Windows 10 操作系统不提供用户启用或禁用关闭电源收费的。

如果启用了关闭电源充电，则该设备仍然受控制的电池充电应用程序即使*启动到 Main OS*达到阈值。 设备将保持此状态，直到用户按住电源按钮 2 秒或更长时间进行启动主操作系统到设备。

即使关闭电源充电启用时，用户将不始终会通过关闭电源充电路径。 如果设备重启 (例如，由于更新，或者是因为系统语言设置更改) 时它启用，并且连接到电源，设备将跳过关闭电源计费模式，并直接启动到主要 OS 在预启动充电阈值后达到了。 关闭电源计费模式将还是如果用户按下电源按钮以重新启动设备上时跳过并连接到电源。

下图显示了启动电池充电过程，启用后关闭电源收费。

![预启动关闭电源充电的电池的流](images/oem-preboot-battery-flow-power-off-charging.png)

启用时关闭电源充电，则以下步骤演示了相应的 UI 流：

1. 如果电池不具有足够的费用，以满足*启动到 Main OS*阈值，10 秒以下红色电池电量不足用户界面屏幕之间交替的设备。 如果用户在此 10 的第二个间隔内按电源按钮，设备将继续之间交替变化以下的电池电量不足用户界面屏幕额外的 10 秒。

    ![前启动阈值的电池电量不足屏幕](images/oem-battery-charge-ui-empty-red.png)![前启动阈值的电池电量不足屏幕](images/oem-battery-charge-ui-plug-red.png)

2. 如果设备处于空闲状态 10 秒，设备会关闭显示器。

    ![电池电量不足屏幕黑色](images/oem-battery-charge-ui-black.png)

3. 设备到达后*启动到 Main OS*阈值，为 10 秒，而不是直接向主操作系统启动以下的白色电池电量不足用户界面屏幕之间交替的设备。 如果用户按此 10 的第二个间隔内的短 duraction （不超过 2 秒） 的电源按钮，设备将继续之间交替变化以下的电池电量不足用户界面屏幕额外的 10 秒。

    ![电池电量不足屏幕后启动阈值](images/oem-battery-charge-ui-empty-white.png)![电池电量不足屏幕后启动阈值](images/oem-battery-charge-ui-plug-white.png)

4. 如果设备处于空闲状态 10 秒，设备会关闭显示器。

    ![电池电量不足屏幕黑色](images/oem-battery-charge-ui-black.png)

5. 如果用户按下电源按钮，2 秒或更长时间，设备显示 OEM 启动徽标，并启动到主操作系统。 下面的屏幕截图演示了示例 OEM 启动徽标。

    ![电池电量不足屏幕 oem 徽标](images/oem-battery-charge-ui-oem-logo.png)

## <a name="battery-charging-thresholds"></a>电池充电阈值

Microsoft 还定义了多个电池充电阈值，以确保正确电池充电的用户体验。 这些阈值的一些必须实现由 OEM 以确保正确电池充电行为。 下图说明了如何计费的阈值的每个组合在一起 (此关系图不绘制为缩放)。

![预启动电池充电阈值](images/oem-preboot-battery-charging-thresholds.png)

左侧和右侧的关系图显示了当设备正在充电，影响用户体验的所有阈值和关系图的右侧显示都了正在放电设备时，会影响用户体验的所有阈值。 下表描述了每个阈值。

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
<td><p>这是在该设备将从基于硬件的收费基于固件的计费启动的阈值。 它有必要在硬件充电阶段进行收费和保护电池时太低，无法启动到固件中存储设备。</p></td>
<td><p>Oem 必须设置为低于此阈值<em>启动到 UEFI 阈值</em>。 有关如何修改此阈值的详细信息，请与 SoC 供应商联系。</p></td>
</tr>
<tr class="even">
<td><p>启动到 UEFI 阈值</p></td>
<td><p>这是在其设备启动从到基于 UEFI 的收费基于固件的收费 （它由 Microsoft 提供） 的阈值。 它有必要在固件充电阶段给电池充电时太低，无法启动到固件中存储设备。</p></td>
<td><p>Oem 必须设置为高于此阈值<em>固件充电阈值</em>，但是低于<em>启动到 Main OS</em>阈值。 有关如何修改此阈值的详细信息，请与 SoC 供应商联系。</p></td>
</tr>
<tr class="odd">
<td><p>启动到 Main OS 阈值</p></td>
<td><p>这是的阈值的设备启动从主操作系统基于 UEFI 的充电<em>阈值收费模式</em>。 它有必要在 UEFI 充电阶段给电池充电时太低，无法启动进入 Main OS 中保存该设备。</p></td>
<td><p>Oem 必须设置为高于此阈值<em>启动到 UEFI 阈值</em>并<em>主操作系统关闭的情况下阈值</em>。 此阈值定义中的电池的全部容量百分比。 默认情况下，此值设置为 7%。 将此文档的未来版本中提供有关如何设置此阈值的信息。</p></td>
</tr>
<tr class="even">
<td><p>启动到更新 OS/设备重置阈值</p></td>
<td><p>这是在该设备将从基于 UEFI 的收费为更新 OS 启动的阈值或对设备重置模式。 它有必要在 UEFI 充电阶段给电池充电时太低，无法承受的 update 或设备重置过程中保存该设备。</p></td>
<td><p>此阈值设置为<em>启动到 Main OS 阈值</em> + 8%。</p></td>
</tr>
<tr class="odd">
<td><p>完整的电池</p></td>
<td><p>这是在 100%的最大容量时是电池的阈值。 在此阈值，系统托盘中的电池图标显示电池图标。</p></td>
<td><p>Oem 应调整其电池配置文件，以便设备能够始终访问电池满负荷。</p></td>
</tr>
<tr class="even">
<td><p>电池保护程序阈值</p></td>
<td><p>这是在哪个电池保护程序会自动启用如果用户已经将电池保护程序设置的阈值。</p></td>
<td><p>此阈值设置为 20%的电池的大容量时，并且这是无法更改由 OEM。</p></td>
</tr>
<tr class="odd">
<td><p>Main OS 警告阈值</p></td>
<td><p>这是在该设备显示电池电量低通知给用户的阈值。</p></td>
<td><p>此阈值设置为 10%的电池的大容量时，并且这是无法更改由 OEM。</p></td>
</tr>
<tr class="even">
<td><p>主操作系统关闭的情况下阈值</p></td>
<td><p>这是在其软件安全地关闭该设备关闭的阈值。 它是为了防止系统内存损坏所必需的。</p></td>
<td><p>OEM 必须设置为低于此阈值<em>启动到 Main OS 阈值</em>并小于<em>Main OS 警告阈值</em>。 此外，此阈值必须大于或等于 2%。 定义此阈值<strong>DefaultAlert1</strong>的成员<a href="https://docs.microsoft.com/windows/desktop/Power/battery-information-str" data-raw-source="[BATTERY_INFORMATION](https://docs.microsoft.com/windows/desktop/Power/battery-information-str)">BATTERY_INFORMATION</a>结构。 有关如何修改此阈值的详细信息，请与 SoC 供应商联系。</p></td>
</tr>
<tr class="odd">
<td><p>关闭阈值的硬件</p></td>
<td><p>这是在其硬件强制设备电源关闭的阈值。 它是需要防止电池正在放电得过低。</p></td>
<td><p>此阈值设置 SoC 供应商和 OEM 不应更改。</p></td>
</tr>
</tbody>
</table>

## <a name="related-topics"></a>相关主题

[UEFI 电池充电由 Microsoft 提供的应用程序的体系结构](architecture-of-the-uefi-battery-charging-application.md)  
[启动和 UEFI](boot-and-uefi.md)  
