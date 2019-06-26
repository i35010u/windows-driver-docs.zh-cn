---
title: IRP_MN_START_DEVICE
description: 所有即插即用驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 0aac1346-b5c7-4dcc-ab86-03e8fd151505
keywords:
- IRP_MN_START_DEVICE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 1d182f36599bff8df3a14b308903684a30161184
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371847"
---
# <a name="irpmnstartdevice"></a>IRP\_MN\_START\_DEVICE


所有即插即用驱动程序必须处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器将发送此 IRP，如果有，向设备分配硬件资源。 设备可能已被最近枚举和启动第一次，或可能的资源重新平衡正在停止后重新启动设备。

PnP 管理器发送有时**IRP\_MN\_启动\_设备**到已启动设备，提供一组不同的资源与当前所用设备。 驱动程序将启动此操作通过调用[ **IoInvalidateDeviceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicestate)和响应的后续[ **IRP\_MN\_查询\_PNP\_设备\_状态**](irp-mn-query-pnp-device-state.md) PNP 请求\_资源\_要求\_CHANGED 标志设置。 总线驱动程序可能会使用此机制，例如，若要打开 PCI PCI 网桥上的新 aperture。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别在系统线程的上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.StartDevice.AllocatedResources**的成员[ **IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)结构指向[ **CM\_资源\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_resource_list)描述的即插即用的管理器分配给设备的硬件资源。 此列表包含原始窗体中的资源。 使用原始资源的设备。

**Parameters.StartDevice.AllocatedResourcesTranslated**指向[ **CM\_资源\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_resource_list)描述的硬件资源的即插即用管理器分配给设备。 此列表包含已翻译的窗体中的资源。 使用转换的资源连接中断矢量、 映射 I/O 空间中，并映射内存。

## <a name="output-parameters"></a>输出参数


无

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，例如状态\_未成功或状态\_不足\_资源。

如果驱动程序需要一些时间才能运行设备及其开始操作，它可以将标记挂起的 IRP，并返回状态\_PENDING。

<a name="operation"></a>操作
---------

按设备父总线驱动程序，然后按设备堆栈中每个更高版本的驱动程序，必须首先处理此 IRP。

在响应此 IRP，驱动程序第一次启动设备，或重新启动已停止的设备。 若要启动设备所需的确切操作不同设备的但可以包含支持在设备上，执行特定于设备的初始化和连接中断。

驱动程序可以通常处理此 IRP 相同的方式是否它是第一次启动设备或重新启动后的设备[ **IRP\_MN\_停止\_设备**](irp-mn-stop-device.md)，除非在驱动程序所需设备上还原状态重新启动后停止。

在 Windows Vista 和更高版本操作系统上，我们建议，驱动程序始终挂起**IRP\_MN\_启动\_设备**IRP 并完成其处理更高版本。 此顺序可让系统以进行异步处理设备重启。 (在 Windows Vista 之前的操作系统、 驱动程序可以返回状态\_PENDING 其调度例程，而即插即用管理器中的不重叠设备重新启动与任何其他操作。)

有关处理开始 IRP 的详细信息，请参阅[启动设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device)。

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


[**IRP\_MN\_STOP\_DEVICE**](irp-mn-stop-device.md)

 

 




