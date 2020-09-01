---
title: IRP_MN_WAIT_WAKE
description: 此 IRP 使驱动程序能够唤醒睡眠系统或唤醒睡眠设备。
ms.date: 08/12/2017
ms.assetid: b79fd057-bf95-457e-882a-42221789e6e6
keywords:
- IRP_MN_WAIT_WAKE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 6f59d8dfaeb329ffeea58b6247cb45f21813aa54
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189321"
---
# <a name="irp_mn_wait_wake"></a>IRP \_ MN \_ 等待 \_ 唤醒


此 IRP 使驱动程序能够唤醒睡眠系统或唤醒睡眠设备。

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ POWER**](irp-mj-power.md)

<a name="when-sent"></a>发送时间
---------

拥有电源策略的驱动程序将此 IRP 定位到其 PDO 上，以使其设备能够唤醒，以响应外部事件，例如传入的电话呼叫。 驱动程序必须调用 [**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) 来发送此 IRP。

作为一般规则，驱动程序应该尽快发送此 IRP，因为它确定应该为其设备启用唤醒功能。 因此，大多数此类设备的驱动程序在打开设备后以及在完成 [**IRP \_ MN \_ 启动 \_ 设备**](irp-mn-start-device.md) 请求之前，将发送此 IRP。

但是，每当设备处于工作状态时，驱动程序都可以发送 IRP (**PowerDeviceD0**) 。 设备堆栈不能处于转换中;也就是说，驱动程序不应发送 **IRP \_ MN \_ 等待 \_ 唤醒** ，而在其设备堆栈中任何其他 power IRP 处于活动状态。

等待/唤醒 IRP 不会更改设备或系统的电源状态。 它只是从设备启用唤醒信号。 唤醒信号到达后，策略所有者必须调用 **PoRequestPowerIrp** ，以发送设置电源 IRP，使其设备返回到 D0。

若要发送此 IRP，驱动程序必须以 IRQL = 被动 \_ 级别运行。 但是，可以在 IRQL = 调度级别完成 IRP \_ 。

## <a name="input-parameters"></a>输入参数


<a href="" id="parameters-waitwake-powerstate-contains-the-lowest--least-powered--system-power-state-from-which-the-device-should-be-allowed-to-awaken-the-system-"></a>**WaitWake. PowerState** 包含应允许设备唤醒系统的最低 (功率) 系统电源状态。  

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/o 状态块


驱动程序将 **Irp- &gt; IoStatus** 设置为以下其中一项：

<a href="" id="status-pending-"></a>状态已 \_ 挂起   
驱动程序收到 IRP，正在等待设备进入唤醒状态。

<a href="" id="status-invalid-device-state-"></a>状态 \_ 无效的 \_ 设备 \_ 状态   
设备的状态小于设备的[**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构中指定的**DeviceWake**状态，或者设备无法唤醒系统在 IRP 中传递的**SystemWake**状态。

<a href="" id="status-not-supported-"></a>\_不 \_ 支持的状态   
设备不支持唤醒。

<a href="" id="status-device-busy-"></a>状态 \_ 设备 \_ 忙   
**Irp \_ MN \_ 等待 \_ 唤醒**请求已挂起，必须先完成或取消，然后才能发出其他 IRP \_ MN \_ wait \_ 唤醒请求。

<a href="" id="status-success"></a>状态 \_ 成功  
设备已终止唤醒事件。

<a href="" id="status-cancelled"></a>已 \_ 取消状态  
IRP 已取消。

如果驱动程序必须失败此 IRP，它会立即完成 IRP，不会将 IRP 传递到下一个较低版本的驱动程序。

<a name="operation"></a>操作
---------

驱动程序出于以下两个原因之一发送 **IRP \_ MN \_ 等待 \_ 唤醒** ：

1.  使其设备能够唤醒休眠系统以响应外部唤醒信号。

2.  使其设备从设备睡眠状态唤醒，以响应外部唤醒信号。

IRP 必须按设备堆栈向下传递到设备的总线驱动程序，这将调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 并返回 \_ 其 [*DISPATCHPOWER*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程的挂起状态。 IRP 始终处于挂起状态，直到出现唤醒信号，或直到发送 IRP 的驱动程序将其取消。

在任何给定时间，都只能为 PDO 保留一个等待/唤醒 IRP。 如果驱动程序已包含 PDO 的等待/唤醒 IRP，则它必须使任何其他此类具有状态设备繁忙的 Irp 失败 \_ \_ 。 枚举多个子 PDO 的驱动程序可以为每个此类 PDO 等待等待/唤醒 IRP。

每个驱动程序在 IRP 向下遍历设备堆栈时设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。 如果设备发出唤醒事件信号，则总线驱动程序会为唤醒信号服务并完成 IRP，并返回状态 "成功" \_ 。 然后，i/o 管理器会调用下一个更高版本的驱动程序的 *IoCompletion* 例程，依此类推。

当驱动程序发送 wait/唤醒 IRP 时，它应在 **PoRequestPowerIrp** 调用中指定一个回调例程。 在回调例程中，驱动程序通常会为设备服务。 例如，设备的电源策略所有者必须调用 **PoRequestPowerIrp** ，以便为设备状态 D0 发送 [**IRP \_ MN \_ 设置 \_ 电源**](irp-mn-set-power.md) 。

作为一个设备的总线驱动程序的驱动程序和父设备的策略所有者在从子 PDO 收到**irp \_ MN \_ 等待 \_ 唤醒**请求时，将为父设备的策略所有者请求**irp \_ MN \_ 等待 \_ 唤醒**IRP。 如果驱动程序枚举了多个子 PDO，无论有多少个子 PDOs 发送等待/唤醒请求，它都应该只为父设备堆栈请求一个等待/唤醒 IRP。 相反，此类驱动程序应保留等待/唤醒 Irp 的内部计数，每次收到请求时递增计数，并在每次完成请求时递减计数。 如果在完成等待/唤醒 IRP 后，计数为非零，则驱动程序应将另一个等待/唤醒 IRP 发送到其设备堆栈，以便 "重置" 自身进行唤醒。 有关详细信息，请参阅 [通过设备树了解等待/唤醒 irp 的路径](./understanding-the-path-of-wait-wake-irps-through-a-device-tree.md)。

若要取消 **IRP \_ MN \_ 等待 \_ 唤醒**，驱动程序将调用 [**IoCancelIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)。 只有源自 IRP 的驱动程序才能取消它。 如果发生以下任何情况，驱动程序将取消挂起的 **IRP \_ MN \_ 等待 \_ 唤醒** ：

-   驱动程序将收到一个 PnP IRP，该 IRP 将停止或删除该设备。

-   系统将进入睡眠状态，并且设备唤醒信号不能唤醒。

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
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)

 

