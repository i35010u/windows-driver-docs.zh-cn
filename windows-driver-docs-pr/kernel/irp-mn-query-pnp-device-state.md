---
title: IRP_MN_QUERY_PNP_DEVICE_STATE
description: 函数、 筛选和总线驱动程序可以处理此请求。
ms.date: 08/12/2017
ms.assetid: 24362a20-9e9d-4566-bc95-ce52b91056af
keywords:
- IRP_MN_QUERY_PNP_DEVICE_STATE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 1afe46bba59aa0c583d67619522f60ab71080d26
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370867"
---
# <a name="irpmnquerypnpdevicestate"></a>IRP\_MN\_查询\_PNP\_设备\_状态


函数、 筛选和总线驱动程序可以处理此请求。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器设备的驱动程序返回从成功后，将发送此 IRP [ **IRP\_MN\_启动\_设备**](irp-mn-start-device.md)发送第一个设备时请求已启动。 此 IRP，才会在启动后停下来购买资源重新平衡。 PnP 管理器还会发送设备调用的驱动程序时此 IRP [ **IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicestate)。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别的任意线程上下文中。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


返回在 I/O 状态块中。

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，例如状态\_未成功。

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**到[ **PNP\_设备\_状态**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request#about-pnpdevicestate)位掩码。


如果函数或筛选器驱动程序不处理此 IRP，则会调用[ **IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)，不会设置[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，并将 IRP 到下一步的驱动程序。 此类驱动程序不能修改**Irp-&gt;IoStatus** ，必须完成 IRP。

如果总线驱动程序不处理此 IRP，则将保留**Irp-&gt;IoStatus.Status**完成 IRP 和时。

<a name="operation"></a>操作
---------

按设备堆栈顶部的驱动程序，然后按每个堆栈中下一个较低的驱动程序，首先处理此 IRP。

驱动程序处理此 IRP，如果它具有关于设备的即插即用的状态信息。 驱动程序可以设置或清除标志中 PNP\_设备\_状态位掩码。 如果另一个驱动程序已设置 PNP\_设备\_状态中**Irp-&gt;IoStatus.Information**，驱动程序必须小心以修改该位掩码中的标记，而不是覆盖整个结构。

请参阅[插](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

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


[**IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicestate)

[**PNP\_DEVICE\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-an-irp-mn-surprise-removal-request#about-pnpdevicestate)
