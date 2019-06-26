---
title: IRP_MJ_WRITE
description: 每个将数据从系统传输到其设备的设备驱动程序必须处理 DispatchWrite 或 DispatchReadWrite 例程中的写入请求，因为必须上层的此类设备驱动程序的任何更高级别的驱动程序。
ms.date: 08/12/2017
ms.assetid: d0db505e-2b3c-4b69-83ef-1a52e37e5d1a
keywords:
- IRP_MJ_WRITE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 6e14ca513aa13f26cee3da3c2147e151b9685ab0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385615"
---
# <a name="irpmjwrite"></a>IRP\_MJ\_WRITE


每个将数据从系统传输到其设备的设备驱动程序必须处理中的写入请求[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchread--dispatchwrite--and-dispatchreadwrite-routines)或[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchread--dispatchwrite--and-dispatchreadwrite-routines)例程，必须为任何更高级别的驱动程序上层的此类设备驱动程序。

<a name="when-sent"></a>发送时间
---------

每当创建请求在成功完成后。

可能是用户模式应用程序或具有表示目标设备对象的文件对象的句柄的 Win32 组件请求的数据传输到设备。 可能是更高级别的驱动程序已创建并设置了写入 IRP。

## <a name="input-parameters"></a>输入参数


驱动程序的 I/O 堆栈位置中 IRP 指示在传输的字节数**Parameters.Write.Length**。

某些驱动程序使用处的值**Parameters.Write.Key**排序传入的写入请求到设备队列中或驱动程序管理的 Irp 的内部队列中以驱动程序确定的顺序。

某些类型的驱动程序还使用处的值**Parameters.Write.ByteOffset**，指示在传输操作的起始偏移量。 有关示例，请参阅[ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-write)可安装文件系统 (IFS) 文档中的主题。

具体取决于基础设备驱动程序是否设置了目标设备对象的**标志**使用\_缓冲\_IO 或使用\_直接\_IO，数据传输从之一以下内容：

-   在缓冲区**Irp-&gt;AssociatedIrp.SystemBuffer**，如果驱动程序将使用缓冲的 I/O

-   描述在 MDL 缓冲区**Irp-&gt;MdlAddress**，如果基础设备驱动程序使用直接 I/O （DMA 或 PIO）

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

接收的写入请求时，会更高级别的驱动程序设置中的下一步较低的驱动程序，IRP 的 I/O 堆栈位置或它会创建并设置其他 Irp 的一个或多个较低的驱动程序。 可以设置其[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，这是可选的输入 IRP，但所需的驱动程序创建 Irp，通过调用[ **IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine). 然后，该驱动程序将传递到下一步低驱动程序和请求[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。

接收到的写入请求，将设备驱动程序将数据传输从系统内存到其设备。 设备驱动程序集**信息**时完成 IRP，传输的 I/O 状态块的字节数的字段。

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


[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)

[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)

[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)

 

 




