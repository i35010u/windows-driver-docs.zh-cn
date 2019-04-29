---
title: IRP_MN_QUERY_PNP_DEVICE_STATE
description: 函数、 筛选和总线驱动程序可以处理此请求。
ms.date: 08/12/2017
ms.assetid: 24362a20-9e9d-4566-bc95-ce52b91056af
keywords:
- IRP_MN_QUERY_PNP_DEVICE_STATE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 945a7056bc30bc9455a569dcd586044c0ad19443
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381429"
---
# <a name="irpmnquerypnpdevicestate"></a>IRP\_MN\_查询\_PNP\_设备\_状态


函数、 筛选和总线驱动程序可以处理此请求。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器设备的驱动程序返回从成功后，将发送此 IRP [ **IRP\_MN\_启动\_设备**](irp-mn-start-device.md)发送第一个设备时请求已启动。 此 IRP，才会在启动后停下来购买资源重新平衡。 PnP 管理器还会发送设备调用的驱动程序时此 IRP [ **IoInvalidateDeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff549361)。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别的任意线程上下文中。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


返回在 I/O 状态块中。

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，例如状态\_未成功。

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**到[ **PNP\_设备\_状态**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request#about-pnpdevicestate)位掩码。


如果函数或筛选器驱动程序不处理此 IRP，则会调用[ **IoSkipCurrentIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff550355)，不会设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程，并将 IRP 到下一步的驱动程序。 此类驱动程序不能修改**Irp-&gt;IoStatus** ，必须完成 IRP。

如果总线驱动程序不处理此 IRP，则将保留**Irp-&gt;IoStatus.Status**完成 IRP 和时。

<a name="operation"></a>操作
---------

按设备堆栈顶部的驱动程序，然后按每个堆栈中下一个较低的驱动程序，首先处理此 IRP。

驱动程序处理此 IRP，如果它具有关于设备的即插即用的状态信息。 驱动程序可以设置或清除标志中 PNP\_设备\_状态位掩码。 如果另一个驱动程序已设置 PNP\_设备\_状态中**Irp-&gt;IoStatus.Information**，驱动程序必须小心以修改该位掩码中的标记，而不是覆盖整个结构。

请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

**发送此 IRP**

保留供系统使用。 驱动程序必须发送此 IRP。

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


[**IoInvalidateDeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff549361)

[**PNP\_DEVICE\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request#about-pnpdevicestate)
