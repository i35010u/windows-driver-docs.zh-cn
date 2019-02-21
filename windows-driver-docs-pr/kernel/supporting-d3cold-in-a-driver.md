---
title: 在驱动程序支持 D3cold
description: 从 Windows 8 开始，设备电源状态 （关闭） D3 被划分为两个不同子状态的状态，D3hot 和 D3cold。
ms.assetid: D085820E-EDAC-4353-8500-207F77D9CC1F
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 71bc176204f94c2be25ba71c0e2b7ecaf8a4e65c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525901"
---
# <a name="supporting-d3cold-in-a-driver"></a>在驱动程序支持 D3cold


从 Windows 8 开始，设备电源状态 （关闭） D3 被划分为两个不同子状态的状态，D3hot 和 D3cold。 D3 是最低功率设备电源状态，并 D3cold 是最低驱动 D3 子状态。 将空闲设备移动到的 D3cold 子状态可以减少能源消耗和扩展移动硬件平台可以在电池电量运行的时间。

在 D3hot，设备通常处于关闭状态。 但是，在设备从其主电源未断开连接，并且父总线控制器可以检测总线上设备的状态。 在 D3cold，从设备中删除主电源和总线控制器无法检测存在该设备。 有关详细信息，请参阅 D3hot 和 D3cold 中的说明[设备低功耗状态](device-sleeping-states.md)。

在早期版本的 Windows，D3 设备电源状态隐式划分为 D3hot 和 D3cold 子状态的状态，但设备不能输入 D3cold，除非计算机正在准备，以便退出 S0 系统电源状态，并输入一个睡眠状态 S1 到 S4。 设备可以输入在计算机保留在 S0 时的低功率 Dx 状态仅限于通过 D3hot D1。

Windows 8 是 Windows，以支持设备电源状态转换到的 D3cold 子状态，当计算机处于 S0 而不准备进入睡眠状态时的第一个版本。 以这种方式支持 D3cold 的设备，从而节省电源中通过以下方式：

-   设备所消耗的电能 D3cold 比在任何其他低功耗 Dx 状态中。
-   如果此设备共享总线与其他设备和所有这些设备支持 D3cold，然后毕竟总线上的设备输入 D3cold，总线控制器可以进入低功耗 Dx 状态。
-   如果此设备与其他设备共享电源，并且所有这些设备支持 D3cold，然后当这些设备的最后一个进入 D3hot，电源可以删除，在这段时间所有这些设备输入 D3cold 更多信息。

相反，不能在 D3cold 空闲的设备可以阻止其他设备输入 D3cold 或其他低功耗 Dx 状态。

以下主题包含有关设备驱动程序中支持 D3cold 详细信息。

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
<td><p><a href="enabling-transitions-to-d3cold.md" data-raw-source="[Enabling Transitions to D3cold](enabling-transitions-to-d3cold.md)">启用将转换为 D3cold</a></p></td>
<td><p>所有版本的 Windows 中都启用设备在计算机处于睡眠状态 （在一个系统低功耗状态 S1 到 S4） 时，要 D3cold。 在计算机退出 S0 之前，功能的驱动程序、 总线驱动程序和筛选器驱动程序协同工作以将设备移到 D3hot。 当计算机进入低功耗 Sx 状态时，此转换具有将设备从 D3hot 移动到 D3cold 的副作用。</p></td>
</tr>
<tr class="even">
<td><p><a href="d3cold-capabilities-of-a-device.md" data-raw-source="[D3cold Capabilities of a Device](d3cold-capabilities-of-a-device.md)">设备的 D3cold 功能</a></p></td>
<td><p>是设备的电源策略所有者 (PPO) 的驱动程序会启用设备输入 D3cold （当该计算机是保留在 S0） 之前，设备将立即响应并继续正常运行，则设备将进入 D3cold 后必须验证该驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="using-guid-d3cold-support-interface.md" data-raw-source="[Using the GUID_D3COLD_SUPPORT_INTERFACE Driver Interface](using-guid-d3cold-support-interface.md)">使用 GUID_D3COLD_SUPPORT_INTERFACE 驱动程序接口</a></p></td>
<td><p>从 Windows 8 开始，驱动程序可以调用例程<a href="https://msdn.microsoft.com/library/windows/hardware/hh967714" data-raw-source="[GUID_D3COLD_SUPPORT_INTERFACE](https://msdn.microsoft.com/library/windows/hardware/hh967714)">GUID_D3COLD_SUPPORT_INTERFACE</a>接口来确定设备的 D3cold 功能并启用这些设备使用 D3cold。 此接口中的两个主例程都<a href="https://msdn.microsoft.com/library/windows/hardware/hh967716" data-raw-source="[&lt;em&gt;SetD3ColdSupport&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh967716)"> <em>SetD3ColdSupport</em> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/hh967712" data-raw-source="[&lt;em&gt;GetIdleWakeInfo&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh967712)"> <em>GetIdleWakeInfo</em></a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="surprise-wake-up.md" data-raw-source="[Surprise Wake-Up](surprise-wake-up.md)">惊讶唤醒</a></p></td>
<td><p>惊讶唤醒是到 D0 的意外的转换。 设备进入 D3cold 后，它可能会惊讶唤醒遇到产生了负面影响在相同的电源线上的另一台设备的驱动程序从 D3cold 到 D0 请求转换时的情况。 第一台设备的驱动程序必须接收通知的惊讶唤醒，以防止设备在未初始化的 D0 状态中保留。</p></td>
</tr>
</tbody>
</table>

 

 

 




