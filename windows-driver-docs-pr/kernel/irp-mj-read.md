---
title: IRP_MJ_READ
description: 将数据从其设备传输到系统的每个设备驱动程序都必须在 DispatchRead 或 DispatchReadWrite 例程中处理 read 请求，就像此类设备驱动程序中的任何更高级别的驱动程序一样。
ms.date: 08/12/2017
ms.assetid: 5ae4c6c5-d8f2-4dc5-8cfd-ecb751fc88be
keywords:
- IRP_MJ_READ 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: fd041bfc2919f10af54df641ce8dc6e68a741fb8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188253"
---
# <a name="irp_mj_read"></a>IRP\_MJ\_READ


将数据从其设备传输到系统的每个设备驱动程序都必须在 [*DispatchRead*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 或 [*DispatchReadWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中处理 read 请求，就像此类设备驱动程序中的任何更高级别的驱动程序一样。

<a name="when-sent"></a>发送时间
---------

在成功完成创建请求之后的任何时间。

对于表示目标设备对象的文件对象，用户模式应用程序或 Win32 组件可能已请求从设备进行数据传输。 或许，更高级别的驱动程序已经创建并设置了读取 IRP。

## <a name="input-parameters"></a>输入参数


IRP 中驱动程序的 i/o 堆栈位置指示在参数上传输的字节数 **。读取. 长度**。

某些驱动程序使用参数中的值 **。读取. Key** 用于将传入的读取请求按驱动程序在设备队列中的顺序进行排序，或在由驱动程序管理的 irp 的内部队列中进行排序。

某些类型的驱动程序也使用 **ByteOffset**，后者指示传输操作的起始偏移量。 例如，请参阅可安装的文件系统 (IFS) 文档中的 [**IRP \_ MJ \_ 读取**](../ifs/irp-mj-read.md) 主题。

## <a name="output-parameters"></a>输出参数


根据基础设备驱动程序是通过 "执行缓冲 io" 还是 "执行直接 IO" 来设置目标设备对象的 **标志** \_ ，将 \_ \_ \_ 数据传输到以下项之一：

-   如果驱动程序使用缓冲 i/o，则为 **Irp &gt;AssociatedIrp.SystemBuffer** 的缓冲区。

-   如果基础设备驱动程序使用直接 i/o (DMA 或 PIO) ，则由 **Irp 在 &gt; MdlAddress** 中描述的缓冲区。

<a name="operation"></a>操作
---------

收到读取请求后，较高级别的驱动程序会在 IRP 中为下一个较低版本的驱动程序设置 i/o 堆栈位置，或为一个或多个较低版本的驱动程序创建和设置其他 Irp。 它可以通过调用[**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)设置其[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，该例程对于输入 IRP 是可选的，但对于驱动程序创建的 irp 是必需的。 然后，驱动程序将请求传递给下一个带 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的低的驱动程序。

收到读取请求后，设备驱动程序将数据从其设备传输到系统内存。 设备驱动程序将 i/o 状态块的 **信息** 字段设置为完成 IRP 后传输的字节数。

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


[*DispatchRead*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchReadWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)

 

