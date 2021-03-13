---
title: IRP_MN_SET_POWER
description: 此 IRP 通知驱动程序系统电源状态的更改或设置设备的设备电源状态。
ms.date: 08/12/2017
keywords:
- IRP_MN_SET_POWER Kernel-Mode 驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 66e1735c4cb14c91c3a8efe9e5206fbc41324dfc
ms.sourcegitcommit: 5524e265f46836100be5fb36ca6fdcac488ab274
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2021
ms.locfileid: "103417246"
---
# <a name="irp_mn_set_power"></a>IRP \_ MN \_ 设置 \_ 电源


此 IRP 通知驱动程序系统电源状态的更改或设置设备的设备电源状态。

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ POWER**](irp-mj-power.md)

<a name="when-sent"></a>发送时间
---------

系统电源管理器或设备电源策略所有者可以发送此 IRP。

电源管理器发送此 IRP，以通知驱动程序系统电源状态的更改。 如果驱动程序已将其设备注册到空闲检测，则电源管理器会发送此 IRP 来更改空闲设备的电源状态。

拥有电源策略的驱动程序将发送此 IRP，以设置其设备的设备电源状态。 驱动程序必须调用 [**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) 来发送此 IRP。

\_对于 \_ 在 PDO 中设置 DO power PAGABLE 标志的设备堆栈，电源管理器以 IRQL = 被动级别发送此 IRP \_ 。 此类堆栈中的驱动程序可以触及分页的代码或数据来完成请求。

\_如果设置了 "DO \_ power 浪涌" 标志，则电源管理器可以以 IRQL 为间隔发送 IRP \_ 。 此类驱动程序不能直接或间接访问任何分页的代码或数据。

## <a name="input-parameters"></a>输入参数


**Parameters. Type** 成员指定所设置的电源状态的类型（ **SystemPowerState** 或 **DevicePowerState**）。

**参数. power. state** 成员指定电源状态本身，如下所示：

-   如果 **SystemPowerState**，则值为 [**系统 \_ 电源 \_ 状态**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_system_power_state)类型的枚举 **器。**

-   如果 **DevicePowerState**，则值为 [**设备 \_ 电源 \_ 状态**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_device_power_state)类型的枚举 **器。**

**ShutdownType** 成员指定有关所请求转换的其他信息。 此成员的可能值为 " **电源 \_ 操作** " 枚举值。 有关详细信息，请参阅 [系统电源操作](./system-power-actions.md)。

从 Windows Vista 开始， **Parameters.Power.SystemPowerStateContext** 成员是一个只读的、部分透明的 [**系统 \_ 电源 \_ 状态 \_ 上下文**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_system_power_state_context) 结构，它包含有关计算机以前系统电源状态的信息。 如果 **SystemPowerState** 为 PowerSystemWorking，**则为参数** **。 power. State** 为，此结构中的两个标志位指示计算机是否进入 S0 () 系统状态下运行。 有关详细信息，请参阅将 [快速启动从休眠状态中唤醒](./distinguishing-fast-startup-from-wake-from-hibernation.md)。

下表显示 IRP_MN_SET_POWER 的内容 **。Parameters。幂{State |ShutdownType}** 和每个系统电源转换的 [**SYSTEM_POWER_STATE_CONTEXT**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_system_power_state_context)结构中的 **CurrentSystemState**、 **TargetSystemState** 和 **EffectiveSystemState** 位域。  每一行代表一个 **IRP_MN_SET_POWER**。

|切换|状态|关闭类型|当前 SystemState|目标 SystemState|有效的 SystemState|注释|
|--- |--- |--- |--- |--- |--- |--- |
|睡眠 .。。|S3|睡眠状态|S0|S3|S3||
|...醒来|S0|睡眠状态|S3|S0|S0||
|混合睡眠到 .。。|S4|休眠|S0|S3|S4|睡眠文件睡眠 (Fast S4) |
|...醒来|S0|睡眠状态|S3|S0|S0||
|...唤醒/PwrLost|S0|睡眠状态|S4|S0|S0||
|休眠到 .。。|S4|休眠|S0|S4|S4||
|...醒来|S0|睡眠状态|S4|S0|S0||
|混合关闭到 .。。|S4|休眠|S0|S5|S4|应用已关闭，用户已注销，如同关机 (Hiber Boot) |
|...快速启动|S0|睡眠状态|S4|S0|S0||
|关闭到 .。。|S5|关机/重置/关闭|S0|S5|S5||
|...System Boot||||||没有用于启动的 S-IRP|

## <a name="output-parameters"></a>输出参数


**Parameters.Power.SystemContext** 保留供系统使用。

## <a name="io-status-block"></a>I/o 状态块


驱动程序将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功" 以指示设备已进入请求的状态。

驱动程序不得对设置系统电源状态的请求失败。

位于总线驱动程序之上的函数和筛选器驱动程序不能使设置设备电源状态的请求失败。 如果设备被删除或正在被删除，则总线驱动程序可以使设备的开机请求失败。

<a name="operation"></a>操作
---------

电源管理器或驱动程序可以请求 **IRP \_ MN \_ 集 \_ 电源** irp。 由于以下原因之一，电源管理器会发送此 IRP：

-   通知驱动程序系统电源状态更改

-   更改电源管理器正在执行空闲检测的设备的电源状态

-   若要在驱动程序失败之后重申当前系统状态，请使用 **IRP \_ MN \_ QUERY \_ power** request 获取系统电源状态。  有关详细信息，请参阅 [**IRP_MN_QUERY_POWER**](./irp-mn-query-power.md#operation)。

拥有设备电源策略的驱动程序将 **IRP \_ MN \_ 设置 \_** 为更改其设备的电源状态。

在任意给定时间，系统仅允许每个设备对象的一个此类 IRP 处于活动状态。

每个驱动程序都必须通过从 Windows Vista) 或 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (windows Server 2003、windows XP 和 windows 2000) 开始调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) (，将每个电源 IRP 向下传递到下一个较低的驱动程序。 **PoCallDriver** 接口与 **IoCallDriver** 类似，只是电源管理子系统可能会延迟 IRP，然后将其传递到下一个驱动程序。 例如，如果设备需要浪涌电流，并因此必须使用其他此类设备进行串行处理，则 **PowerDeviceD0** 请求上可能会出现延迟。

驱动程序在 Windows Server 2003、Windows XP 或 Windows 2000 上收到 **IRP \_ MN \_ 设置 \_ 电源** 请求后，驱动程序必须调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)，如 [调用 PoStartNextPowerIrp](./calling-postartnextpowerirp.md)中所述。 从 Windows Vista 开始，不需要调用 **PoStartNextPowerIrp** ，此类调用不会执行任何电源管理操作。

**IRP \_ MN \_ \_ 为系统电源状态设置电源**

只有系统电源管理器才能发送系统设置-power IRP。

驱动程序不得对设置系统电源状态的请求失败。

只要有可能，电源管理器就会发送 irp [**\_ MN \_ 查询 \_ 功能**](irp-mn-query-power.md) ，然后再发送 **irp \_ MN \_ \_** ，以请求系统睡眠状态。 但是，在某些情况下 (例如用户按下 " **关闭电源** " 按钮或电池过期) ，则在没有首次查询的情况下，电源管理器可能会发出 **IRP \_ MN 的 \_ \_ 电源** 。 仅限睡眠状态的电源管理器查询;它在启动前永远不会查询。

**IRP \_ MN \_ SET \_ POWER** request 发送到设备堆栈中的顶层驱动程序。 顶层驱动程序将 IRP 向下传递到下一个较低的驱动程序，依此类推，直到 IRP 到达必须完成 IRP 的总线驱动程序。

筛选器驱动程序通常不需要对系统设置-电源 IRP 执行操作，而不是将其传递到。

然而，设备电源策略所有者在传递 IRP 之前设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。 在 *IoCompletion* 例程中，它为设备电源 Irp 发送 **IRP \_ MN \_ 设置 \_ 电源** 请求。 有关详细信息，请参阅 [在设备电源策略所有者中处理 System Set-Power IRP](./handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)。

系统设置-power IRP 通知驱动程序对系统电源状态的更改即将发生，驱动程序必须为其做好准备。 但是，驱动程序不应更改其设备的电源状态，直到收到 **IRP \_ MN \_ 设置 \_** *设备* 电源状态的电源。

**ShutdownType** 中的值提供有关挂起的操作的其他信息。 当 IRP 指定 **PowerSystemShutdown** (S5) 时，驱动程序可以确定系统是否正在重置 (**PowerActionShutdownReset**) 或无限期关闭，稍后 (**PowerActionShutdownOff**) 。 对于大多数设备的驱动程序，差别是无关紧要。 但对于某些设备（如视频流式处理设备），驱动程序可能会关闭设备，以便在系统重置时停止 i/o。

在 Windows 2000 和更高版本的操作系统上， **ShutdownType** 处的值也可以是 **PowerActionShutdown**。 在这种情况下，驱动程序无法判断请求哪种类型的关闭，因此应继续进行重置。

**设备电源状态**

位于总线驱动程序之上的函数和筛选器驱动程序不能使设置设备电源状态的请求失败。 如果设备被删除或正在被删除，则总线驱动程序可以使设备的开机请求失败。

在完成 IRP 之前，驱动程序必须将设备设置为请求的状态。

当 IRP 请求转换到更低的电源状态时，驱动程序必须在该 IRP 向下移动时处理 IRP，并保存任何上下文，驱动程序将需要将设备还原到工作状态。 在总线驱动程序收到 IRP 后，该驱动程序：

-   保存驱动程序将设备还原到工作状态所需的所有上下文。

-   将设备设置为请求电源状态。

-   调用 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate) 以通知电源管理器。

-   调用 **PoStartNextPowerIrp** 来启动下一个 power IRP (仅) windows Server 2003、windows XP 和 windows 2000。

-   完成设备电源 IRP。

驱动程序必须及时完成此 IRP。 通常，驱动程序应避免典型用户明显降低的延迟。 例如，驱动程序可能会延迟系统状态更改以刷新缓存磁盘或网络数据，但不应使网络连接保持活动状态或格式化磁带。 有关详细信息，请参阅 [通过电源 irp](./passing-power-irps.md)。

在 Windows 2000 和更高版本的操作系统上，如果 IRP 指定 **PowerDeviceD1**、 **PowerDeviceD2** 或 **PowerDeviceD3**，并且系统设置-power IRP 处于活动状态，则 **参数. SHUTDOWNTYPE** 中的值提供有关系统 IRP 的信息。

休眠路径上设备的驱动程序应该检查此值。 如果 IRP 请求 **PowerDeviceD3** 和 **ShutdownType** 为 **PowerActionHibernate**，则此类驱动程序应保存恢复设备所需的任何上下文，但不应关闭设备电源;当计算机断电时，设备将进入 D3 状态。

在 Windows 2000 和更高版本的操作系统上，如果请求的电源状态为 **PowerDeviceD0**，则驱动程序不应依赖于 **ShutdownType** 处的值。

在 Windows 98/Me 上，如果 IRP 请求设备电源状态， **ShutdownType** 始终为 **PowerActionNone**。

确定何时关闭设备电源的驱动程序因设备类而异。

确定设备启动时间的驱动程序几乎始终是访问设备寄存器的驱动程序。 在访问设备的硬件寄存器之前，驱动程序必须验证设备是否处于 D0 状态。 如果设备未处于 D0 状态，则驱动程序必须调用 **PoRequestPowerIrp** 来发送 IRP，以启动设备。 驱动程序无法访问其设备，除非设备处于 D0 状态。

当驱动程序收到设备状态 D0 的设置-电源 IRP 时，它将设置一个 *IoCompletion* 例程，并将 IRP 传递到下一个较低的驱动程序。

当 IRP 达到总线驱动程序时，该驱动程序将应用 (或重置设备) 电源、仅)  (Windows Server 2003、Windows XP 和 Windows 2000 上调用 **PoStartNextPowerIrp** ，并调用 **PoSetPowerState** 来向电源管理器通知设备的新电源状态。

在总线驱动程序完成开机 IRP 后，函数和筛选器驱动程序会在其 *IoCompletion* 例程中处理 IRP，因为它将在设备堆栈上传输。 在 *IoCompletion* 例程中，每个驱动程序还原或重新初始化其设备上下文，并执行任何其他必需的启动任务。

有关详细信息，请参阅 [处理 IRP \_ MN \_ 设置 \_ 设备电源状态的电源](./handling-irp-mn-set-power-for-device-power-states.md)。

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
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**设备 \_ 电源 \_ 状态**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_device_power_state)

[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[**IRP \_ MN \_ 查询 \_ 能力**](irp-mn-query-power.md)

[**IRP \_ MN \_ 设置 \_ 电源**](irp-mn-set-power.md)

[**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)

[**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)

[**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)

[**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)

[**系统 \_ 电源 \_ 状态**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_system_power_state)

[**系统 \_ 电源 \_ 状态 \_ 上下文**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_system_power_state_context)

 

