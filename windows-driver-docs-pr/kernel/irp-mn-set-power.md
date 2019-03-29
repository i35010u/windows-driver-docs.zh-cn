---
title: IRP_MN_SET_POWER
description: 此 IRP 通知对系统电源状态更改的驱动程序，或设置设备的设备电源状态。
ms.date: 08/12/2017
ms.assetid: 1294183a-bd0b-4ead-bd64-669d5b3725ce
keywords:
- IRP_MN_SET_POWER Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 220924dd1997ca425f5173b2b90d507560ecf496
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577297"
---
# <a name="irpmnsetpower"></a>IRP\_MN\_SET\_POWER


此 IRP 通知对系统电源状态更改的驱动程序，或设置设备的设备电源状态。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_电源**](irp-mj-power.md)时发送
---------

系统电源管理器或设备电源策略所有者可以将此 IRP 发送。

电源管理器将发送此 IRP 通知对系统电源状态更改的驱动程序。 如果驱动程序已注册其设备的空闲检测，电源管理器将发送此 IRP，若要更改的闲置设备电源状态。

拥有电源策略的驱动程序将发送此 IRP，若要设置其设备的设备电源状态。 驱动程序必须调用[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)发送此 IRP。

电源管理器将此 IRP 发送在 IRQL = 被动\_级别设置执行操作的设备堆栈\_电源\_PAGABLE 在 PDO 中标记。 此类堆栈中的驱动程序可以触摸分页的代码或数据，以完成该请求。

电源管理器可以将 IRP 发送在 IRQL = 调度\_级别如果 DO\_电源\_浪涌标志设置。 此类的驱动程序不能直接或间接访问的任何分页的代码或数据。

## <a name="input-parameters"></a>输入参数


**Parameters.Power.Type**成员指定的电源状态正在设置，或者类型**SystemPowerState**或**DevicePowerState**。

**Parameters.Power.State**成员指定的电源状态本身，按如下所示：

-   如果**Parameters.Power.Type**是**SystemPowerState**，则这是一个枚举器的[**系统\_POWER\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff564565)类型。

-   如果**Parameters.Power.Type**是**DevicePowerState**，则这是一个枚举器的[**设备\_POWER\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff543160)类型。

**Parameters.Power.ShutdownType**成员指定请求转换有关的其他信息。 为此成员可能的值为**电源\_操作**枚举值。 有关详细信息，请参阅[系统电源操作](https://msdn.microsoft.com/library/windows/hardware/ff564553)。

从 Windows Vista 开始**Parameters.Power.SystemPowerStateContext**成员是一个只读部分不透明[**系统\_POWER\_状态\_上下文**](https://msdn.microsoft.com/library/windows/hardware/jj835780)结构，其中包含有关计算机的以前的系统电源状态的信息。 如果**Parameters.Power.Type**是**SystemPowerState**并**Parameters.Power.State**是**PowerSystemWorking**，两个标志位在此结构指示快速启动或唤醒从休眠是否导致计算机进入 S0 （工作） 系统状态。 有关详细信息，请参阅[快速区分从唤醒从休眠状态的启动](https://msdn.microsoft.com/library/windows/hardware/jj835779)。

## <a name="output-parameters"></a>输出参数


**Parameters.Power.SystemContext**保留供系统使用。

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功以指示设备已进入请求的状态。

驱动程序不得失败的请求以设置系统电源状态。

位于上方总线驱动程序的函数和筛选器驱动程序不得失败的请求设置设备电源状态。 如果删除该设备或正被删除，总线驱动程序可能会失败的设备强化请求。

<a name="operation"></a>操作
---------

电源管理器或驱动程序可以请求**IRP\_MN\_设置\_POWER** IRP。 电源管理器将此 IRP 发送出于以下原因之一：

-   若要通知的系统电源状态更改的驱动程序

-   若要更改其电源管理器正在执行空闲检测设备的电源状态

拥有设备的电源策略的驱动程序发送**IRP\_MN\_设置\_POWER**若要更改其设备的电源状态。

在任何给定时间，系统允许此类只有一个 IRP 处于活动状态的每个设备对象。

每个驱动程序必须通过调用传递到下一步低驱动程序的每个 power IRP [ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336) （从 Windows Vista 开始） 或[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654)（Windows Server 2003、 Windows XP 和 Windows 2000）。 **PoCallDriver**界面是类似于**IoCallDriver**，只不过电源管理子系统可能会延迟 IRP，然后再将它传递到下一步的驱动程序。 例如，可能会发生延迟上**PowerDeviceD0**请求如果设备需要涌流，并且因此必须为通电按顺序与另一个此类设备。

驱动程序收到后**IRP\_MN\_设置\_POWER**驱动程序在 Windows Server 2003 上的请求，Windows XP 或 Windows 2000 中，必须调用[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)，如中所述[调用 PoStartNextPowerIrp](https://msdn.microsoft.com/library/windows/hardware/ff540724)。 使用 Windows Vista 开始，调用**PoStartNextPowerIrp**不是必需的并且此类调用会执行任何电源管理操作。

**IRP\_MN\_设置\_的电源可用于系统的电源状态**

仅系统电源管理器可以发送一个系统集 power IRP。

驱动程序不得失败的请求以设置系统电源状态。

只要有可能，电源管理器将发送[ **IRP\_MN\_查询\_POWER** ](irp-mn-query-power.md)发送之前**IRP\_MN\_设置\_电源**请求系统睡眠状态。 但是，在某些情况下 (例如用户按下**关闭电源**按钮或电池过期)，电源管理器可能会发出**IRP\_MN\_设置\_POWER**而无需先进行查询。 电源管理器查询仅为睡眠状态; 的它将永远不会查询之前启动。

**IRP\_MN\_设置\_POWER**请求发送到设备堆栈中的顶部驱动程序的设备。 直到 IRP 达到的总线驱动程序，必须完成 IRP，顶部驱动程序将 IRP 到下一个较低的驱动程序等传递。

筛选器驱动程序通常不需要的系统上执行操作集 power IRP，若要传递比其他。

设备电源策略所有者，但是，设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程之前关闭 IRP 传递。 在中*IoCompletion*例程，它将发送**IRP\_MN\_设置\_POWER**设备电源 IRP 的请求。 有关详细信息，请参阅[处理设备电源策略所有者中系统集 Power IRP](https://msdn.microsoft.com/library/windows/hardware/ff546749)。

系统集 power IRP 告知驱动程序对系统电源状态的更改即将且驱动程序必须做好准备。 但是，驱动程序不应更改其设备的电源状态直到收到**IRP\_MN\_设置\_POWER**有关*设备*电源状态。

处的值**Parameters.Power.ShutdownType**提供了有关挂起的操作的其他信息。 当指定了 IRP **PowerSystemShutdown** (S5) 驱动程序可以确定系统是否正在重置 (**PowerActionShutdownReset**) 或功耗关闭无限期地以稍后重新启动 (**PowerActionShutdownOff**)。 对于大多数设备的驱动程序，不同之处并不重要。 但是，对于某些设备，如视频流的设备，驱动程序可能会关闭电源设备为了重置系统时停止 I/O。

在 Windows 2000 和更高版本的操作系统处的值**ShutdownType**也可以是**PowerActionShutdown**。 在这种情况下，该驱动程序无法判断哪种类型的关闭请求，因此应继续与重置。

**设备的电源状态**

位于上方总线驱动程序的函数和筛选器驱动程序不得失败的请求设置设备电源状态。 如果删除该设备或正被删除，总线驱动程序可能会失败的设备强化请求。

驱动程序必须完成 IRP 之前设置了到请求的状态的设备。

当 IRP 请求转换为较低的电源状态时，驱动程序必须处理 IRP，向设备堆栈，保存该驱动程序将需要将设备还原到工作状态的任何上下文下传输时。 后一个总线驱动程序接收 IRP，驱动程序：

-   保存驱动程序将需要将设备还原到工作状态的任何上下文。

-   将设备设置为所请求的电源状态。

-   调用[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765)通知电源管理器。

-   调用**PoStartNextPowerIrp**启动下一个幂 IRP （Windows Server 2003、 Windows XP 和 Windows 2000 仅）。

-   完成设备电源 IRP。

该驱动程序必须及时地完成此 IRP。 一般情况下，驱动程序应避免典型用户会明显下降发现任何延迟。 例如，驱动程序可能会延迟系统状态更改来刷新缓存的磁盘或网络数据，但不是应使网络连接保持活动状态或磁带格式化。 有关详细信息，请参阅[传递 Power Irp](https://msdn.microsoft.com/library/windows/hardware/ff558785)。

在 Windows 2000 和更高版本的操作系统，如果指定了 IRP **PowerDeviceD1**， **PowerDeviceD2**，或**PowerDeviceD3**，和系统集 power IRP，则活动、 处的值**Parameters.Power.ShutdownType**提供有关系统 IRP 的信息。

休眠路径上的设备的驱动程序应检查此值。 如果请求 IRP **PowerDeviceD3**并**ShutdownType**是**PowerActionHibernate**，这样的驱动程序应保存将设备还原所需的任何上下文，但不是应关闭设备;当计算机断电时，设备将进入 D3 状态。

在 Windows 2000 和更高版本的操作系统，驱动程序不应依赖于处的值**ShutdownType**如果请求的电源状态为**PowerDeviceD0**。

在 Windows 98 上 / 我来说，如果 IRP 请求设备电源状态， **ShutdownType**始终**PowerActionNone**。

确定何时关闭的设备的驱动程序而异的设备类。

确定何时在设备接通电源的驱动程序几乎始终是访问设备寄存器的驱动程序。 该驱动程序必须验证之前访问设备的硬件注册该设备处于 D0 状态。 如果设备不处于 D0 状态，该驱动程序必须调用**PoRequestPowerIrp**以将 IRP 发送到打开设备的电源。 驱动程序不能访问其设备，除非设备处于 D0 状态。

当驱动程序收到设备状态 D0 集 power IRP 时，它会设置*IoCompletion*例程并将 IRP 到下一个较低的驱动程序。

当 IRP 到达总线驱动程序时，该驱动程序应用 （或重置） 到设备时，调用 power **PoStartNextPowerIrp** （Windows Server 2003、 Windows XP 和 Windows 2000 仅），并调用**PoSetPowerState**以通知新的电源状态的设备的电源管理器。

函数和筛选器驱动程序强化 IRP 总线驱动程序之后，处理 IRP 中的其*IoCompletion*例程作为其传输到设备堆栈。 在中*IoCompletion*例程，每个驱动程序还原或重新初始化其设备上下文并执行任何其他所需的启动任务。

有关详细信息，请参阅[处理 IRP\_MN\_设置\_的电源可用于设备的电源状态](https://msdn.microsoft.com/library/windows/hardware/ff546885)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVICE\_POWER\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff543160)

[**IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)

[**IRP\_MN\_查询\_电源**](irp-mn-query-power.md)

[**IRP\_MN\_SET\_POWER**](irp-mn-set-power.md)

[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)

[**PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)

[**PoSetPowerState**](https://msdn.microsoft.com/library/windows/hardware/ff559765)

[**PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734)

[**SYSTEM\_POWER\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff564565)

[**SYSTEM\_POWER\_STATE\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/jj835780)

 

 




