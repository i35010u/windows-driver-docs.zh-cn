---
title: IRP_MN_WAIT_WAKE
description: 此 IRP 使驱动程序能够唤醒睡眠系统或唤醒睡眠设备。
ms.date: 08/12/2017
ms.assetid: b79fd057-bf95-457e-882a-42221789e6e6
keywords:
- IRP_MN_WAIT_WAKE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: fb4d5364c4ecde5f255ffea117ed2533f0b3cad9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827935"
---
# <a name="irp_mn_wait_wake"></a>IRP\_MN\_等待\_唤醒


此 IRP 使驱动程序能够唤醒睡眠系统或唤醒睡眠设备。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_POWER**](irp-mj-power.md)发送时间
---------

拥有电源策略的驱动程序将此 IRP 定位到其 PDO 上，以使其设备能够唤醒，以响应外部事件，例如传入的电话呼叫。 驱动程序必须调用[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)来发送此 IRP。

作为一般规则，驱动程序应该尽快发送此 IRP，因为它确定应该为其设备启用唤醒功能。 因此，大多数此类设备的驱动程序会在打开设备后和完成 Irp 之前发送此 IRP， [ **\_MN\_开始\_设备**](irp-mn-start-device.md)请求。

但是，驱动程序可以在设备处于工作状态时随时发送 IRP （**PowerDeviceD0**）。 设备堆栈不能处于转换中;也就是说，驱动程序不应发送**IRP\_MN\_等待\_唤醒**，而任何其他 power IRP 在其设备堆栈中处于活动状态。

等待/唤醒 IRP 不会更改设备或系统的电源状态。 它只是从设备启用唤醒信号。 唤醒信号到达后，策略所有者必须调用**PoRequestPowerIrp** ，以发送设置电源 IRP，使其设备返回到 D0。

若要发送此 IRP，驱动程序必须在 IRQL = 被动\_级别下运行。 但是，可以在 IRQL = 调度\_级别完成 IRP。

## <a name="input-parameters"></a>输入参数


<a href="" id="parameters-waitwake-powerstate-contains-the-lowest--least-powered--system-power-state-from-which-the-device-should-be-allowed-to-awaken-the-system-"></a>**WaitWake. PowerState**包含允许设备唤醒系统的最低（最小）系统电源状态。  

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/O 状态块


驱动程序将**Irp&gt;IoStatus**设置为以下其中一项：

<a href="" id="status-pending-"></a>状态\_挂起   
驱动程序收到 IRP，正在等待设备进入唤醒状态。

<a href="" id="status-invalid-device-state-"></a>状态\_无效\_设备\_状态   
设备的电源状态小于设备[ **\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构中指定的**DeviceWake**状态，或者设备无法唤醒系统从 IRP 中传递的**SystemWake**状态。

<a href="" id="status-not-supported-"></a>状态\_不\_支持   
设备不支持唤醒。

<a href="" id="status-device-busy-"></a>\_设备\_繁忙状态   
**IRP\_MN\_等待\_唤醒**请求已挂起，必须先完成或取消，然后另一 IRP\_MN\_等待\_唤醒请求可以发出。

<a href="" id="status-success"></a>成功\_状态  
设备已终止唤醒事件。

<a href="" id="status-cancelled"></a>状态\_已取消  
IRP 已取消。

如果驱动程序必须失败此 IRP，它会立即完成 IRP，不会将 IRP 传递到下一个较低版本的驱动程序。

<a name="operation"></a>操作
---------

出于以下两个原因之一，驱动程序将**IRP\_MN\_等待\_唤醒**：

1.  使其设备能够唤醒休眠系统以响应外部唤醒信号。

2.  使其设备从设备睡眠状态唤醒，以响应外部唤醒信号。

IRP 必须按设备堆栈向下传递到设备的总线驱动程序，这将调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)并返回其[*DISPATCHPOWER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程\_挂起的状态。 IRP 始终处于挂起状态，直到出现唤醒信号，或直到发送 IRP 的驱动程序将其取消。

在任何给定时间，都只能为 PDO 保留一个等待/唤醒 IRP。 如果驱动程序已经包含用于 PDO 的等待/唤醒 IRP，则它必须将状态为\_设备\_的任何其他此类 Irp 停止。 枚举多个子 PDO 的驱动程序可以为每个此类 PDO 等待等待/唤醒 IRP。

每个驱动程序在 IRP 向下遍历设备堆栈时设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程。 如果设备发出唤醒事件信号，则总线驱动程序会为唤醒信号服务并完成 IRP，并返回状态\_"成功"。 然后，i/o 管理器会调用下一个更高版本的驱动程序的*IoCompletion*例程，依此类推。

当驱动程序发送 wait/唤醒 IRP 时，它应在**PoRequestPowerIrp**调用中指定一个回调例程。 在回调例程中，驱动程序通常会为设备服务。 例如，设备的电源策略所有者必须调用**PoRequestPowerIrp** ，以便发送[**IRP\_MN\_设置**](irp-mn-set-power.md)设备状态 D0\_电源。

作为一个设备的总线驱动程序的驱动程序和父设备的策略所有者请求**IRP\_MN\_** 在收到**irp\_MN\_等待时，为父级的设备堆栈等待\_唤醒 IRP @no__t_** 从子 PDO 7_ 唤醒请求。 如果驱动程序枚举了多个子 PDO，无论有多少个子 PDOs 发送等待/唤醒请求，它都应该只为父设备堆栈请求一个等待/唤醒 IRP。 相反，此类驱动程序应保留等待/唤醒 Irp 的内部计数，每次收到请求时递增计数，并在每次完成请求时递减计数。 如果在完成等待/唤醒 IRP 后，计数为非零，则驱动程序应将另一个等待/唤醒 IRP 发送到其设备堆栈，以便 "重置" 自身进行唤醒。 有关详细信息，请参阅[通过设备树了解等待/唤醒 irp 的路径](https://docs.microsoft.com/windows-hardware/drivers/kernel/understanding-the-path-of-wait-wake-irps-through-a-device-tree)。

若要取消**IRP\_MN\_等待\_唤醒**，驱动程序将调用[**IoCancelIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)。 只有源自 IRP 的驱动程序才能取消它。 如果发生以下任何情况，驱动程序将取消挂起的**IRP\_MN\_等待\_唤醒**：

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
<td><p>标头</p></td>
<td>Wdm .h （包括 Wdm、Ntddk 或 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)

 

 




