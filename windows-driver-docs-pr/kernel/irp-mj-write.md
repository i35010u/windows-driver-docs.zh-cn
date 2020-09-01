---
title: IRP_MJ_WRITE
description: 每个将数据从系统传输到其设备的设备驱动程序必须在 DispatchWrite 或 DispatchReadWrite 例程中处理写入请求，就像此类设备驱动程序上的任何更高级别的驱动程序一样。
ms.date: 08/12/2017
ms.assetid: d0db505e-2b3c-4b69-83ef-1a52e37e5d1a
keywords:
- IRP_MJ_WRITE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 3d691569219d87ab6ee9688ca24a3353c97d79a4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188241"
---
# <a name="irp_mj_write"></a>IRP\_MJ\_WRITE


每个将数据从系统传输到其设备的设备驱动程序必须在 [*DispatchWrite*](./dispatchread--dispatchwrite--and-dispatchreadwrite-routines.md) 或 [*DispatchReadWrite*](./dispatchread--dispatchwrite--and-dispatchreadwrite-routines.md) 例程中处理写入请求，就像此类设备驱动程序上的任何更高级别的驱动程序一样。

<a name="when-sent"></a>发送时间
---------

在成功完成创建请求之后的任何时间。

用户模式应用程序或 Win32 组件（表示目标设备对象的文件对象的句柄）已请求将数据传输到设备。 或许，更高级别的驱动程序已经创建并设置了写入 IRP。

## <a name="input-parameters"></a>输入参数


IRP 中驱动程序的 i/o 堆栈位置指示要在参数上传输的字节数 **。写入长度**。

某些驱动程序使用 **参数. write. 键** 将传入写入请求排序为驱动程序在设备队列中确定的顺序，或在 irp 的驱动程序托管的内部队列中进行排序。

某些类型的驱动程序还使用 **ByteOffset 参数**值，后者指示传输操作的起始偏移量。 有关示例，请参阅可安装的文件系统 (IFS) 文档中的 [**IRP \_ MJ \_ 写入**](../ifs/irp-mj-write.md) 主题。

根据基础设备驱动程序是用 DO 缓冲 IO 还是按 DO DIRECT io 来设置目标设备对象的 **标志** \_ ，将 \_ \_ \_ 从以下项之一传输数据：

-   Irp 中的缓冲区 **- &gt;AssociatedIrp.SystemBuffer**，如果驱动程序使用缓冲 i/o

-   如果基础设备驱动程序使用直接 i/o (DMA 或 PIO) ，则由 **Irp 在 &gt; MdlAddress**中描述的缓冲区

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

收到写入请求时，较高级别的驱动程序会在 IRP 中为下一个较低版本的驱动程序设置 i/o 堆栈位置，或为一个或多个较低版本的驱动程序创建和设置其他 Irp。 它可以通过调用[**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)设置其[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，该例程对于输入 IRP 是可选的，但对于驱动程序创建的 irp 是必需的。 然后，驱动程序将请求传递给下一个带 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的低的驱动程序。

收到写入请求时，设备驱动程序会将数据从系统内存传输到其设备。 设备驱动程序将 i/o 状态块的 **信息** 字段设置为完成 IRP 后传输的字节数。

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


[*DispatchReadWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)

[**IoSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)

 

