---
title: IRP_MN_QUERY_POWER
description: 此 IRP 查询设备，以确定是否可以更改系统电源状态或设备电源状态。
ms.date: 08/12/2017
ms.assetid: fc4c5364-2160-4525-889a-96785a3c7a07
keywords:
- IRP_MN_QUERY_POWER Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 2f9df260fdf923b619a5c3298724044b0b8ed6dc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381426"
---
# <a name="irpmnquerypower"></a>IRP\_MN\_查询\_电源


此 IRP 查询设备，以确定是否可以更改系统电源状态或设备电源状态。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_电源**](irp-mj-power.md)时发送
---------

电源管理器或设备电源策略所有者发送此 IRP，以确定是否可以更改系统或设备电源状态，通常要进入睡眠状态。 驱动程序必须调用[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)来分配和发送此 IRP。

电源管理器将此 IRP 发送在 IRQL = 被动\_级别设置执行操作的设备堆栈\_电源\_PAGABLE 在 PDO 中标记。

电源管理器可以将 IRP 发送在 IRQL = 调度\_级别如果 DO\_电源\_浪涌标志设置。 此类的驱动程序不能直接或间接访问的任何分页的代码或数据。

## <a name="input-parameters"></a>输入参数


**Parameters.Power.Type**指定的电源状态正在设置，或者类型**SystemPowerState**或**DevicePowerState**。

**Parameters.Power.State**指定的电源状态本身，按如下所示：

-   如果**Parameters.Power.Type**是**SystemPowerState**，则这是一个枚举器的[**系统\_POWER\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff564565)类型。

-   如果**Parameters.Power.Type**是**DevicePowerState**，则这是一个枚举器的[**设备\_POWER\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff543160)类型。

**Parameters.Power.ShutdownType**指定请求转换的其他信息。 可能的值为枚举器的**电源\_操作**类型。

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功以指示该设备，可以输入请求的状态。 驱动程序设置任何相应的故障状态，以指示它不能输入请求的状态。

<a name="operation"></a>操作
---------

参数**IRP\_MN\_查询\_POWER**于相同[ **IRP\_MN\_设置\_电源**](irp-mn-set-power.md). 而不是通知驱动程序的电源状态，但是，不可撤消更改**IRP\_MN\_查询\_POWER**查询系统或设备是否可以输入特定电源状态。

驱动程序不得更改以响应其设备的电源状态**IRP\_MN\_查询\_POWER**请求。

驱动程序收到后**IRP\_MN\_查询\_POWER**驱动程序在 Windows Server 2003 上的请求、 Windows XP 和 Windows 2000，必须调用[ **PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)，如中所述[调用**PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff540724)。 使用 Windows Vista 开始，调用**PoStartNextPowerIrp**不是必需的和此类调用会执行任何电源管理操作。

**IRP\_MN\_查询\_的电源可用于系统电源状态**

电源管理器将发送此 IRP，以确保它可以更改系统电源状态而不会中断工作，例如网络连接断开。

只要有可能，在发送前查询电源管理器**IRP\_MN\_设置\_POWER**请求系统睡眠状态或正常的系统关闭。 但是，在某些关键的情况下 (例如用户按下**关闭电源**按钮或电池过期)，电源管理器可能会发送**IRP\_MN\_设置\_POWER**而无需第一个发送查询 power 请求的请求。 电源管理器查询仅为睡眠状态; 的它将永远不会查询返回到工作状态之前。

当驱动程序收到系统电源查询 IRP 时，这应该会失败 IRP，如果它不能支持的任何有效查询的系统状态的设备状态。 有关详细信息，请参阅[ **DeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff543087)。 否则，该驱动程序应将 IRP 传递给下一个较低的驱动程序。 总线驱动程序完成 IRP。

从 Windows Vista 开始，过渡到系统睡眠状态被视为关键操作。 尽管驱动程序可能会失败，系统查询能耗 IRP，电源管理器可能仍将更改系统电源状态为睡眠状态。 驱动程序收到查询能耗 IRP，驱动程序应始终在系统后准备的系统电源状态的后续更改。

当设备电源策略所有者收到系统电源查询 IRP 时，它应设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程中之前将其向下传递。 在中*IoCompletion*例程，它应发送**IRP\_MN\_查询\_POWER**有效查询的系统状态的设备状态。 有关详细信息，请参阅[处理设备电源策略所有者中系统查询能耗 IRP](https://msdn.microsoft.com/library/windows/hardware/ff546725)。

当指定了 IRP **PowerSystemShutdown** (S5) 处的值**Parameters.Power.ShutdownType**提供关机的原因。 **ShutdownType**指示驱动程序是否正在重置系统 (**PowerActionShutdownReset**) 或功耗关闭无限期地以稍后重新启动 (**PowerActionShutdownOff**). 对于大多数设备的驱动程序，不同之处并不重要。 但是，对于某些设备，如视频流执行 DMA，设备驱动程序可能会选择关闭其设备的电源系统重置时，因此停止任何正在运行的 I/O。

Microsoft Windows 2000 和更高版本的系统，处的值上**ShutdownType**也可以是**PowerActionShutdown**。 在这种情况下，该驱动程序无法判断哪种类型的关闭请求，因此应继续与重置。

如果驱动程序失败**IRP\_MN\_查询\_POWER**电源管理器通常通过发出响应系统电源状态，请求**IRP\_MN\_设置\_电源**IRP。 通常情况下，此 IRP 将重申的当前系统状态。 但是，就可以驱动程序可能会收到**IRP\_MN\_设置\_POWER**查询状态或另一种中间状态。 驱动程序应准备好处理这些情况。

**IRP\_MN\_查询\_的电源可用于设备电源状态**

设备电源策略所有者向其堆栈到系统的响应中发送此 IRP **IRP\_MN\_查询\_POWER**请求。

如果驱动程序可以将其设备放在请求的设备状态，则将设置**IoStatus.Status**于状态\_成功并将传递到下一步 IRP 降低驱动程序，并直到 IRP 达到总线驱动程序等等。 如果堆栈中的任何驱动程序时不能 IRP，表示立即该驱动程序应通过调用完成 IRP **IoCompleteRequest**并返回故障状态。 失败 IRP 的驱动程序未通过它进一步在堆栈的下层。

通过返回状态\_成功后，该驱动程序可保证它不会启动的任何操作都将更改其设置请求的电源状态的能力。 该驱动程序应队列需要此类操作，直到它完成将设备返回到可接受的电源状态集 power IRP 任何 Irp。

在 Windows 2000 和更高版本系统，当指定 IRP **PowerDeviceD1**， **PowerDeviceD2**，或**PowerDeviceD3**，在值**Parameters.Power.ShutdownType**提供当前系统电源 IRP，有关的信息，如果系统电源 IRP 处于活动状态。 在此情况下，在值**ShutdownType**指示当前请求的系统电源状态，或**PowerActionNone**如果系统请求不是未完成。 在 Windows 98 上 / 我来说，此字段始终包含**PowerActionNone** IRP 当请求设备电源状态。

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


[**IRP\_MN\_查询\_电源**](irp-mn-query-power.md)

[**IRP\_MN\_SET\_POWER**](irp-mn-set-power.md)

[**PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734)

[**PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)

 

 




