---
title: IRP_MJ_CLEANUP
description: 维护特定于进程的上下文信息的驱动程序必须在 DispatchCleanup 例程中处理清除请求。
ms.date: 08/12/2017
ms.assetid: 097f5f1d-3e88-4db0-bb79-db2267bdaf38
keywords:
- IRP_MJ_CLEANUP 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 8fedc61336f807370094f01a5c3bd1d926196c46
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184443"
---
# <a name="irp_mj_cleanup"></a>IRP\_MJ\_CLEANUP


维护特定于进程的上下文信息的驱动程序必须在 [*DispatchCleanup*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中处理清除请求。

<a name="when-sent"></a>发送时间
---------

此请求的接收表明已关闭与目标设备对象相关联的文件对象的最后一个句柄， (但由于未完成的 i/o 请求，可能未) 释放该句柄。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

此 IRP 在关闭文件对象句柄的进程的上下文中发送。 因此，驱动程序应释放先前锁定或映射的特定于进程的资源，例如用户内存。

如果驱动程序的设备对象设置为 "专用"，以便一次只有一个线程可以使用设备，则驱动程序必须将当前排队的每个 IRP 都完成为目标设备对象，并 \_ 在每个 irp 的 i/o 状态块中设置 "已取消" 状态。

否则，驱动程序必须取消并只完成当前排队的 Irp，该 Irp 与正在发布的文件对象句柄关联。  (指向文件对象的指针位于 IRP 的驱动程序[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的**FileObject**成员中。 ) 在取消这些已排队的 irp 后，该驱动程序将完成清除 irp 并 \_ 在其 I/o 状态块中设置状态 "成功"。

有关处理此请求的详细信息，请参阅 [DispatchCleanup 例程](./dispatchcleanup-routines.md)。

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


[*DispatchCleanup*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IRP \_ MJ \_ 关闭**](irp-mj-close.md)

 

