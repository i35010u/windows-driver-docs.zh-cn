---
title: 设备电源状态
description: 设备电源状态
ms.assetid: 2229f34c-9b88-4e3e-802e-f7be2c7ef168
keywords:
- 设备电源状态 WDK 内核
- 电源状态 WDK 内核
- 状态 WDK 电源管理
- Dx 命名 WDK 电源管理
- 低功耗模式 WDK 内核
- 省电模式 WDK 内核
- 持续电能 WDK 内核
- 延迟 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05b5a144811285afc91cc99844c7daa738fb6926
ms.sourcegitcommit: 2bf68f6c08c02ddcfccaf5fa485ff1ca92a08749
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "69985804"
---
# <a name="device-power-states"></a>设备电源状态


## <a href="" id="ddk-device-power-states-kg"></a>


设备电源状态描述计算机中设备的电源状态, 与计算机中的其他设备无关。 设备电源状态分别为 D0、D1、D2 和 D3。 D0 是完全打开状态, D1、D2 和 D3 均为低功耗状态。 状态号码与功率消耗成反比: 更高编号的状态使用更少的电量。 从 Windows 8 开始, D3 状态分为两个 substates: D3hot 和 D3cold。

设备电源状态的特征如下:

-   功率消耗:设备使用的功率是多少？

-   设备上下文:设备在此状态下将保持多少操作上下文？

-   设备驱动程序行为:设备的驱动程序必须执行哪些操作才能将设备还原到完全操作状态？

-   还原时间:将设备还原到完全操作状态需要多长时间？ 大多数类型的设备都具有适度的还原时间, 这在不同的设备类中很少。 只有几种类型的设备 (例如 Gpu) 具有非常大的硬件上下文, 这些上下文的恢复时间要长得多。

-   唤醒功能:设备请求是否可以从这种状态唤醒？ 通常情况下, 如果设备可以请求从给定电源状态唤醒 (例如 D2), 则它还可以从任何更高的状态 (D1) 请求唤醒。

电源状态的确切定义是设备特定的。 并非所有设备都定义所有状态;许多设备仅定义 D0 和 D3 状态。 请参阅设备类电源管理参考规范, 查明为特定设备定义了哪些设备电源状态以及每种状态的操作要求。 ( [ACPI/电源管理](https://go.microsoft.com/fwlink/p/?linkid=57185)网站上提供了参考规范。)

设备的电源状态需要与[系统电源状态](system-power-states.md)不匹配。 例如, 即使系统处于[系统工作状态 (S0)](system-working-state-s0.md), 某些设备也可能处于关闭 (D3) 状态。

设备的电源状态似乎与设备的父总线的电源状态无关。 例如, 当 USB 设备的父主机控制器处于 D3 状态时, 该设备可能在 D2 (选择性挂起) 状态。 这两个状态似乎是不一致的, 因为 Dx 状态的定义在 USB 和 USB 主机控制器连接到的总线 (通常是 PCI 或 PCI Express) 上是不同的。

请注意, 某些设备在单个设备电源状态下能够使用几种不同的低功率模式。 如果设备的驱动程序可以将设备从一种模式自动切换到另一种模式, 而无需更改设备电源状态, 则此类设备可以使用这些模式。 但一般情况下, 如果模式之间没有用户明显的差异, 则设备只应使用最低的电源模式。 如果低功耗模式 (如低速模式) 会对性能造成负面影响, 或者对非设备驱动程序以外的软件透明, 则硬件不应自动使用。 有关详细信息, 请参阅设备类电源管理参考规范。

驱动程序或电源管理器可以请求设备电源状态转换, 并且所有驱动程序必须准备好处理请求此类转换的 Irp。 有关详细信息，请参阅下列主题：

[发送 IRP\_MN\_\_QUERY\_power 或 IRP\_MN\_为设备电源状态设置电源](sending-irp-mn-query-power-or-irp-mn-set-power-for-device-power-states.md)

[处理 IRP\_MN\_查询\_电源的设备电源状态](handling-irp-mn-query-power-for-device-power-states.md)

[处理 IRP\_MN\_设置\_设备电源状态的电源](handling-irp-mn-set-power-for-device-power-states.md)

## <a href="" id="power-state-diagram"></a>


与系统一样, 设备可以从工作状态 (D0) 转换为任何低功耗状态 (D1、D2 或 D3), 也可以从任何低功耗状态转换到工作状态。 下图是一个状态图, 它显示了有效的设备电源状态转换。

![阐释有效设备电源状态转换的关系图](images/dxpostates.png)

此图显示了 D3 在 D3hot 和 D3cold 中的细分。 D3hot 和 D3cold 是从 Windows 8 开始定义的。 所有设备都需要支持 D0 状态和 D3hot 子状态。 关系图中显示的其他状态是可选的。

在上图中, 从 D3hot 到 D3cold 的转换是设备低功耗状态之间唯一直接转换。 低功耗状态之间的所有其他转换都需要到 D0 的中间转换, 这允许设备驱动程序根据需要配置设备硬件, 使其进入下一低电源状态或保持 D0 状态。 但是, 在关闭设备电源时, 设备会退出 D3hot 并进入 D3cold, 这无需设备驱动程序介入。 此驱动程序在设备进入 D3hot 之前, 对设备硬件进行任何必要的配置;准备设备以便从 D3hot 转换为 D3cold 时, 无需进行其他配置。 有关详细信息, 请参阅[支持驱动程序中的 D3cold](supporting-d3cold-in-a-driver.md)。


## <a name="pci-root-port-to-endpoint-d-state-mapping"></a>PCI 根端口到终结点 D-状态映射 
 
在 Windows 10 系统上, 整体平台电源状态取决于 SoC (系统 on 芯片) 集成设备 (包括 PCI 根端口) 的电源状态 (D-状态)。 根据要开发的平台, PCI 根端口的 D 状态要求可能因每个平台电源状态而异。 建议 Oem 参阅 IHV 平台特定的文档以了解平台和设备电源状态要求。  
 
下表列举了 PCI 根端口及其附加终结点的电源状态映射。 为了使根端口进入目标 D 状态, 必须实现下面列出的终结点的 D 状态。 
 
<table>
<thead>
<tr class="header">
<th>根端口目标 D-状态</th>
<th>终结点 D-状态 </th>
</tr>
</thead>
<tbody valign="top">
<tr class="odd">
<td><p>D0</p></td>
<td><p>D0, D0: F1</p></td>
</tr>
<tr class="even">
<td><p>D0: F1</p></td>
<td><p>D3hot</p></td>
</tr>
<tr class="odd">
<td><p>D3hot</p></td>
<td><p>D3cold*</p></td>
</tr>
</tbody>
</table>

\* PCI D3cold 电源状态需要 BIOS 和设备驱动程序支持。 如果缺少支持, PCI 端点将只能实现 D3Hot。 有关详细信息, 请参阅[支持驱动程序中的 D3Cold](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-d3cold-in-a-driver)。
