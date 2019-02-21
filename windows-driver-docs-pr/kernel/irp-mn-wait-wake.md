---
title: IRP_MN_WAIT_WAKE
description: 此 IRP，若要唤醒处于睡眠状态的系统或唤醒处于睡眠状态的设备驱动程序。
ms.date: 08/12/2017
ms.assetid: b79fd057-bf95-457e-882a-42221789e6e6
keywords:
- IRP_MN_WAIT_WAKE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: ee57b89cba2d0aeefee1621ab9c1f42182896d3e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542740"
---
# <a name="irpmnwaitwake"></a>IRP\_MN\_WAIT\_WAKE


此 IRP，若要唤醒处于睡眠状态的系统或唤醒处于睡眠状态的设备驱动程序。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_电源**](irp-mj-power.md)时发送
---------

拥有电源策略的驱动程序针对此 IRP 到其 PDO，若要启用其设备以唤醒以响应外部事件，例如传入的电话呼叫。 驱动程序必须调用[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)发送此 IRP。

作为一般规则，驱动程序应发送此 IRP，只要它确定应为唤醒启用的其设备。 因此，大多数此类设备的驱动程序之后，将发送此 IRP 增强其设备上以及在完成前[ **IRP\_MN\_启动\_设备**](irp-mn-start-device.md)请求.

但是，驱动程序可以发送的 IRP 每当设备是处于工作状态 (**PowerDeviceD0**)。 设备堆栈不能转换; 中也就是说，驱动程序不应发送**IRP\_MN\_等待\_唤醒**任何其他电源 IRP 其设备堆栈中处于活动状态时。

等待/唤醒 IRP 不会更改的设备或系统电源状态。 它只是使来自设备的唤醒信号。 当唤醒信号到达时，必须调用策略所有者**PoRequestPowerIrp**发送集 power IRP，若要将其设备恢复至 D0。

该驱动程序必须运行在 IRQL = 被动\_要发送此 IRP 级别。 但是，可以在 IRQL 完成 IRP = 调度\_级别。

## <a name="input-parameters"></a>输入参数


<a href="" id="parameters-waitwake-powerstate-contains-the-lowest--least-powered--system-power-state-from-which-the-device-should-be-allowed-to-awaken-the-system-"></a>**Parameters.WaitWake.PowerState**包含从其设备应允许唤醒系统的最低 （最少支持） 的系统电源状态。  

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**到以下项之一：

<a href="" id="status-pending-"></a>状态\_PENDING   
该驱动程序接收 IRP 和等待信号唤醒设备。

<a href="" id="status-invalid-device-state-"></a>状态\_无效\_设备\_状态   
设备处于不支持状态比**DeviceWake**中指定的状态[**设备\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)为设备或设备的结构不能被从系统唤醒**SystemWake**中 IRP 传递状态。

<a href="" id="status-not-supported-"></a>状态\_不\_支持   
设备不支持唤醒。

<a href="" id="status-device-busy-"></a>状态\_设备\_忙   
**IRP\_MN\_等待\_唤醒**请求已被挂起并且必须已完成或在另一个 IRP 之前取消\_MN\_等待\_唤醒请求可以是颁发。

<a href="" id="status-success"></a>状态\_成功  
设备已向唤醒事件发出信号。

<a href="" id="status-cancelled"></a>状态\_已取消  
已取消 IRP。

如果驱动程序必须失败此 IRP，它将立即完成 IRP 并不将 IRP 传递到下一个较低的驱动程序。

<a name="operation"></a>操作
---------

驱动程序发送**IRP\_MN\_等待\_唤醒**为上述两个原因：

1.  若要允许其设备被唤醒处于睡眠状态以响应外部的唤醒信号系统。

2.  若要启用其设备以进行从外部唤醒信号响应中的设备睡眠状态唤醒。

到设备，从而调用总线驱动程序，必须将 IRP 传递设备堆栈的下层[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422) ，并返回状态\_PENDING 从其[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 IRP 一直处于挂起状态唤醒信号发生之前或直到发送 IRP 的驱动程序取消它。

只有一个等待/唤醒 IRP 可保持挂起的 PDO 在任何给定时间。 如果驱动程序已持有的 PDO 等待/唤醒 IRP，它必须无法通过任何其他状态与此类 Irp\_设备\_忙。 枚举多个子 PDO 驱动程序可以对每个此类 PDO 有等待/唤醒 IRP 挂起。

每个驱动程序设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) IRP 传输时向设备堆栈下例程。 当设备向唤醒事件发出信号时，总线驱动程序服务唤醒信号，并完成 IRP，返回状态\_成功。 然后，I/O 管理器调用*IoCompletion*例程的下一个更高版本驱动程序，并以此类推遍历设备堆栈。

当驱动程序发送等待/唤醒 IRP 时，还应指定中的回调例程**PoRequestPowerIrp**调用。 在回调例程中，该驱动程序通常服务设备。 例如，设备的电源策略所有者必须调用**PoRequestPowerIrp**发送[ **IRP\_MN\_设置\_POWER** ](irp-mn-set-power.md)设备状态 D0。

充当一个设备的总线驱动程序和父设备的策略所有者的驱动程序请求**IRP\_MN\_等待\_唤醒**IRP 的父级的设备堆栈时收到**IRP\_MN\_等待\_唤醒**来自子 PDO 请求。 如果驱动程序枚举多个子 PDO，则应请求只能有一个等待/唤醒 IRP 的父级的设备堆栈无论子 PDOs 发送等待/唤醒请求数。 相反，此类驱动程序应请等待/唤醒 Irp 的内部计数，递增计数每次收到的请求和递减计数每次完成一个请求时。 如果计数为零，完成等待/唤醒 IRP 后，驱动程序应发送另一个等待/唤醒 IRP 到其设备堆栈以"rearm"本身为唤醒。 有关详细信息，请参阅[了解路径的等待/唤醒 Irp 通过设备树](https://msdn.microsoft.com/library/windows/hardware/ff564867)。

若要取消**IRP\_MN\_等待\_唤醒**，驱动程序调用[ **IoCancelIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548338)。 源自 IRP 的驱动程序可以取消它。 驱动程序取消挂起**IRP\_MN\_等待\_唤醒**发生任何以下情况时：

-   驱动程序收到 PnP IRP 将停止或删除设备。

-   系统将进入睡眠状态，设备唤醒信号必须不被唤醒它。

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
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734)

 

 




