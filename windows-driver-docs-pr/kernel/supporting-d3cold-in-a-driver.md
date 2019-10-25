---
title: 在驱动程序中支持 D3cold
description: 从 Windows 8 开始，D3 （关）设备电源状态分为两个不同的 substates，D3hot 和 D3cold。
ms.assetid: D085820E-EDAC-4353-8500-207F77D9CC1F
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e671878716ef77dd37903ef53e7f41ed57c20d2d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836226"
---
# <a name="supporting-d3cold-in-a-driver"></a>在驱动程序中支持 D3cold


从 Windows 8 开始，D3 （关）设备电源状态分为两个不同的 substates，D3hot 和 D3cold。 D3 是最低功率的设备电源状态，D3cold 是 D3 的最低功率子状态。 将空闲设备移动到 D3cold 子状态可降低能耗，并延长移动硬件平台可在电池电量上运行的时间。

在 D3hot 中，设备主要处于关闭状态。 不过，设备不会从其主电源断开连接，并且父总线控制器可以检测总线上的设备是否存在。 在 D3cold 中，将从设备中删除主电源，并且总线控制器无法检测到设备是否存在。 有关详细信息，请参阅 D3hot 和[D3cold 的说明。](device-sleeping-states.md)

在较早版本的 Windows 中，D3 设备电源状态隐式划分为 D3hot 和 D3cold substates，但设备不能进入 D3cold，除非计算机正在准备退出 S0 系统电源状态，并进入一个睡眠状态 S1 到 S4。 在计算机处于 S0 状态时，设备可输入的低功耗 Dx 状态限制为 D1 到 D3hot。

Windows 8 是 Windows 的第一个版本，当计算机处于 S0 状态且未准备进入睡眠状态时，它将支持设备电源状态转换为 D3cold 子状态。 以这种方式支持 D3cold 的设备可以通过以下方式节省电能：

-   设备在 D3cold 中所消耗的电量比在任何其他低功耗 Dx 状态下更少。
-   如果此设备与其他设备共享总线，并且所有这些设备都支持 D3cold，则在总线上的所有设备进入 D3cold 后，总线控制器可以进入低功耗 Dx 状态。
-   如果此设备与其他设备共享电源，并且所有这些设备都支持 D3cold，那么，当最后一个设备进入 D3hot 时，可以删除电源，此时，这些设备都将共同进入 D3cold。

相反，D3cold 中无法空闲的设备可能会阻止其他设备进入 D3cold 或其他低功耗 Dx 状态。

以下主题包含有关设备驱动程序中支持 D3cold 的详细信息。

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
<td><p><a href="enabling-transitions-to-d3cold.md" data-raw-source="[Enabling Transitions to D3cold](enabling-transitions-to-d3cold.md)">启用到 D3cold 的转换</a></p></td>
<td><p>当计算机处于睡眠状态时，所有版本的 Windows 都允许设备处于 D3cold 状态（在一个系统低功耗状态 S1 到 S4 中）。 在计算机退出 S0 之前，函数驱动程序、总线驱动程序和筛选器驱动程序协同工作以将设备移至 D3hot。 当计算机进入低功耗 Sx 状态时，此转换的副作用是将设备从 D3hot 移动到 D3cold。</p></td>
</tr>
<tr class="even">
<td><p><a href="d3cold-capabilities-of-a-device.md" data-raw-source="[D3cold Capabilities of a Device](d3cold-capabilities-of-a-device.md)">设备的 D3cold 功能</a></p></td>
<td><p>在设备的电源策略所有者（PPO）的驱动程序允许设备进入 "D3cold" （当计算机停留在 S0 中时）之前，驱动程序必须验证设备是否响应并在设备进入 D3cold 后继续正常运行。</p></td>
</tr>
<tr class="odd">
<td><p><a href="using-guid-d3cold-support-interface.md" data-raw-source="[Using the GUID_D3COLD_SUPPORT_INTERFACE Driver Interface](using-guid-d3cold-support-interface.md)">使用 GUID_D3COLD_SUPPORT_INTERFACE 驱动程序接口</a></p></td>
<td><p>从 Windows 8 开始，驱动程序可以调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh967714" data-raw-source="[GUID_D3COLD_SUPPORT_INTERFACE](https://msdn.microsoft.com/library/windows/hardware/hh967714)">GUID_D3COLD_SUPPORT_INTERFACE</a>接口中的例程来确定设备的 D3COLD 功能，并允许这些设备使用 D3COLD。 此接口中的两个主要例程是<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_d3cold_support" data-raw-source="[&lt;em&gt;SetD3ColdSupport&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_d3cold_support)"><em>SetD3ColdSupport</em></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-get_idle_wake_info" data-raw-source="[&lt;em&gt;GetIdleWakeInfo&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-get_idle_wake_info)"><em>GetIdleWakeInfo</em></a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="surprise-wake-up.md" data-raw-source="[Surprise Wake-Up](surprise-wake-up.md)">意外唤醒</a></p></td>
<td><p>意外唤醒是到 D0 的意外转换。 设备进入 D3cold 后，如果同一电源轨上另一台设备的驱动程序请求从 D3cold 到 D0 的转换，则可能会出现意外唤醒。 第一台设备的驱动程序必须收到意外唤醒的通知，以防止设备处于未初始化的 D0 状态。</p></td>
</tr>
</tbody>
</table>

 

 

 




