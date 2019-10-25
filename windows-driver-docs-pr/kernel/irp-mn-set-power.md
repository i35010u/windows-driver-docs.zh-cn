---
title: IRP_MN_SET_POWER
description: 此 IRP 通知驱动程序系统电源状态的更改或设置设备的设备电源状态。
ms.date: 08/12/2017
ms.assetid: 1294183a-bd0b-4ead-bd64-669d5b3725ce
keywords:
- IRP_MN_SET_POWER 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 41625176056f0cc384c6f8f065340df89b2f1c3b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838563"
---
# <a name="irp_mn_set_power"></a>IRP\_MN\_集\_电源


此 IRP 通知驱动程序系统电源状态的更改或设置设备的设备电源状态。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_POWER**](irp-mj-power.md)发送时间
---------

系统电源管理器或设备电源策略所有者可以发送此 IRP。

电源管理器发送此 IRP，以通知驱动程序系统电源状态的更改。 如果驱动程序已将其设备注册到空闲检测，则电源管理器会发送此 IRP 来更改空闲设备的电源状态。

拥有电源策略的驱动程序将发送此 IRP，以设置其设备的设备电源状态。 驱动程序必须调用[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)来发送此 IRP。

在 PDO 中设置 DO\_POWER\_PAGABLE 标志的设备堆栈时，电源管理器会将此 IRP 以 IRQL = 被动\_级别发送到设备堆栈。 此类堆栈中的驱动程序可以触及分页的代码或数据来完成请求。

如果设置了 DO\_POWER\_浪涌标志，则电源管理器可以将 IRP 发送到 IRQL = 调度\_级别。 此类驱动程序不能直接或间接访问任何分页的代码或数据。

## <a name="input-parameters"></a>输入参数


**Parameters. Type**成员指定所设置的电源状态的类型（ **SystemPowerState**或**DevicePowerState**）。

**参数. power. state**成员指定电源状态本身，如下所示：

-   如果**SystemPowerState**，则值为[**系统\_Power\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_system_power_state)类型的枚举**器。**

-   如果**参数**为**DevicePowerState**，则值为[**设备\_Power\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_device_power_state)类型的枚举器。

**ShutdownType**成员指定有关所请求转换的其他信息。 此成员的可能值为**POWER\_操作**枚举值。 有关详细信息，请参阅[系统电源操作](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-power-actions)。

从 Windows Vista 开始， **SystemPowerStateContext**成员是只读的、部分不透明的[**系统\_电源\_状态\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_system_power_state_context)结构，其中包含有关上一个系统的信息计算机的电源状态。 如果**SystemPowerState**为**PowerSystemWorking**，**则为**，**则此**结构中的两个标志位指示计算机是否进入了快速启动或从休眠状态唤醒S0 （工作）系统状态。 有关详细信息，请参阅将[快速启动从休眠状态中唤醒](https://docs.microsoft.com/windows-hardware/drivers/kernel/distinguishing-fast-startup-from-wake-from-hibernation)。

下表显示了 IRP_MN_SET_POWER 的内容 **。Parameters。幂{State |ShutdownType}** 和**CurrentSystemState**、 **TargetSystemState**和**EffectiveSystemState**位字段，适用于每个[**系统的电源**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_system_power_state_context)转换。  每一行代表一个**IRP_MN_SET_POWER**。

|过渡|省/市/自治区|关闭类型|当前 SystemState|目标 SystemState|有效的 SystemState|备注|
|--- |--- |--- |--- |--- |--- |--- |
|睡眠 。|S3|睡眠|S0|S3|S3||
|...醒来|S0|睡眠|S3|S0|S0||
|混合睡眠到 。|S4|休眠|S0|S3|S4|睡眠文件（Fast S4）|
|...醒来|S0|睡眠|S3|S0|S0||
|...唤醒/PwrLost|S0|睡眠|S4|S0|S0||
|休眠到 。|S4|休眠|S0|S4|S4|||
|...醒来|S0|睡眠|S4|S0|S0||
|混合关闭到 。|S4|休眠|S0|S5|S4|应用已关闭，用户已注销，如同关机（Hiber Boot）|
|...快速启动|S0|睡眠|S4|S0|S0||
|关闭到 。|S5|关机/重置/关闭|S0|S5|S5||
|...系统启动||||||没有用于启动的 S-IRP|

## <a name="output-parameters"></a>输出参数


**SystemContext**保留供系统使用。

## <a name="io-status-block"></a>I/O 状态块


驱动程序将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS，以指示设备已进入请求状态。

驱动程序不得对设置系统电源状态的请求失败。

位于总线驱动程序之上的函数和筛选器驱动程序不能使设置设备电源状态的请求失败。 如果设备被删除或正在被删除，则总线驱动程序可以使设备的开机请求失败。

<a name="operation"></a>操作
---------

电源管理器或驱动程序可以 **\_电源 IRP 请求 IRP\_MN\_集**。 由于以下原因之一，电源管理器会发送此 IRP：

-   通知驱动程序系统电源状态更改

-   更改电源管理器正在执行空闲检测的设备的电源状态

-   若要在驱动程序失败之后重申当前系统状态， **IRP\_MN\_查询\_** 系统电源状态的电源请求。  有关详细信息，请参阅[**IRP_MN_QUERY_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power#operation)。

拥有设备电源策略的驱动程序将**IRP\_MN\_设置\_电源**，以更改其设备的电源状态。

在任意给定时间，系统仅允许每个设备对象的一个此类 IRP 处于活动状态。

每个驱动程序都必须通过调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) （从 Windows Vista 开始）或[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) （Windows SERVER 2003、windows XP 和 windows 2000），将每个电源 IRP 向下传递到下一个较低的驱动程序。 **PoCallDriver**接口与**IoCallDriver**类似，只是电源管理子系统可能会延迟 IRP，然后将其传递到下一个驱动程序。 例如，如果设备需要浪涌电流，并因此必须使用其他此类设备进行串行处理，则**PowerDeviceD0**请求上可能会出现延迟。

当驱动程序收到**IRP\_MN\_** 在 windows Server 2003、windows XP 或 windows 2000 上设置\_POWER request，驱动程序必须调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)，如[调用 PoStartNextPowerIrp](https://docs.microsoft.com/windows-hardware/drivers/kernel/calling-postartnextpowerirp)中所述。 从 Windows Vista 开始，不需要调用**PoStartNextPowerIrp** ，此类调用不会执行任何电源管理操作。

**IRP\_MN\_为系统电源状态设置\_电源**

只有系统电源管理器才能发送系统设置-power IRP。

驱动程序不得对设置系统电源状态的请求失败。

如有可能，在发送 Irp 之前，电源管理器会发送[**irp\_MN\_查询\_power**](irp-mn-query-power.md) **\_\_\_设置**，以请求系统睡眠状态。 但是，在某些情况下（例如用户按下 "**关闭电源**" 按钮或电池过期），电源管理器可能会发出**IRP\_MN\_设置\_电源**，无需先进行查询。 仅限睡眠状态的电源管理器查询;它在启动前永远不会查询。

**\_将 IRP\_集\_电源**请求发送到设备堆栈中的顶层驱动程序。 顶层驱动程序将 IRP 向下传递到下一个较低的驱动程序，依此类推，直到 IRP 到达必须完成 IRP 的总线驱动程序。

筛选器驱动程序通常不需要对系统设置-电源 IRP 执行操作，而不是将其传递到。

然而，设备电源策略所有者在传递 IRP 之前设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程。 在*IoCompletion*例程中，它会向设备电源 IRP **\_电源请求发送 IRP\_MN\_集**。 有关详细信息，请参阅[在设备电源策略所有者中处理系统集电源 IRP](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-a-system-set-power-irp-in-a-device-power-policy-owner)。

系统设置-power IRP 通知驱动程序对系统电源状态的更改即将发生，驱动程序必须为其做好准备。 但是，驱动程序不应更改其设备的电源状态，直到它收到**IRP\_MN\_设置***设备*电源状态\_电源。

**ShutdownType**中的值提供有关挂起的操作的其他信息。 当 IRP 指定**PowerSystemShutdown** （S5）时，驱动程序可以确定系统是重置（**PowerActionShutdownReset**）还是无限期关机以稍后重新启动（**PowerActionShutdownOff**）。 对于大多数设备的驱动程序，差别是无关紧要。 但对于某些设备（如视频流式处理设备），驱动程序可能会关闭设备，以便在系统重置时停止 i/o。

在 Windows 2000 和更高版本的操作系统上， **ShutdownType**处的值也可以是**PowerActionShutdown**。 在这种情况下，驱动程序无法判断请求哪种类型的关闭，因此应继续进行重置。

**设备电源状态**

位于总线驱动程序之上的函数和筛选器驱动程序不能使设置设备电源状态的请求失败。 如果设备被删除或正在被删除，则总线驱动程序可以使设备的开机请求失败。

在完成 IRP 之前，驱动程序必须将设备设置为请求的状态。

当 IRP 请求转换到更低的电源状态时，驱动程序必须在该 IRP 向下移动时处理 IRP，并保存任何上下文，驱动程序将需要将设备还原到工作状态。 在总线驱动程序收到 IRP 后，该驱动程序：

-   保存驱动程序将设备还原到工作状态所需的所有上下文。

-   将设备设置为请求电源状态。

-   调用[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)以通知电源管理器。

-   调用**PoStartNextPowerIrp**启动下一个 power IRP （仅限 windows Server 2003、windows XP 和 windows 2000）。

-   完成设备电源 IRP。

驱动程序必须及时完成此 IRP。 通常，驱动程序应避免典型用户明显降低的延迟。 例如，驱动程序可能会延迟系统状态更改以刷新缓存磁盘或网络数据，但不应使网络连接保持活动状态或格式化磁带。 有关详细信息，请参阅[通过电源 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/passing-power-irps)。

在 Windows 2000 和更高版本的操作系统上，如果 IRP 指定**PowerDeviceD1**、 **PowerDeviceD2**或**PowerDeviceD3**，并且系统设置-power IRP 处于活动状态，则中的值**将提供**有关系统 IRP 的信息。

休眠路径上设备的驱动程序应该检查此值。 如果 IRP 请求**PowerDeviceD3**和**ShutdownType**为**PowerActionHibernate**，则此类驱动程序应保存恢复设备所需的任何上下文，但不应关闭设备电源;当计算机断电时，设备将进入 D3 状态。

在 Windows 2000 和更高版本的操作系统上，如果请求的电源状态为**PowerDeviceD0**，则驱动程序不应依赖于**ShutdownType**处的值。

在 Windows 98/Me 上，如果 IRP 请求设备电源状态， **ShutdownType**始终为**PowerActionNone**。

确定何时关闭设备电源的驱动程序因设备类而异。

确定设备启动时间的驱动程序几乎始终是访问设备寄存器的驱动程序。 在访问设备的硬件寄存器之前，驱动程序必须验证设备是否处于 D0 状态。 如果设备未处于 D0 状态，则驱动程序必须调用**PoRequestPowerIrp**来发送 IRP，以启动设备。 驱动程序无法访问其设备，除非设备处于 D0 状态。

当驱动程序收到设备状态 D0 的设置-电源 IRP 时，它将设置一个*IoCompletion*例程，并将 IRP 传递到下一个较低的驱动程序。

当 IRP 达到总线驱动程序时，该驱动程序会将电源应用（或重置）到设备上，调用**PoStartNextPowerIrp** （仅限 windows Server 2003、windows XP 和 windows 2000），并调用**PoSetPowerState**将新电源设备的状态。

在总线驱动程序完成开机 IRP 后，函数和筛选器驱动程序会在其*IoCompletion*例程中处理 IRP，因为它将在设备堆栈上传输。 在*IoCompletion*例程中，每个驱动程序还原或重新初始化其设备上下文，并执行任何其他必需的启动任务。

有关详细信息，请参阅[处理 IRP\_MN\_设置设备电源状态\_电源](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irp-mn-set-power-for-device-power-states)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdm .h （包括 Wdm、Ntddk 或 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**设备\_电源\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_device_power_state)

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[**IRP\_MN\_QUERY\_POWER**](irp-mn-query-power.md)

[**IRP\_MN\_集\_电源**](irp-mn-set-power.md)

[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)

[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)

[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)

[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)

[**系统\_电源\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_system_power_state)

[**系统\_电源\_状态\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_system_power_state_context)

 

 




