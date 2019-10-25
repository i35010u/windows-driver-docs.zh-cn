---
title: IRP_MJ_CLEANUP
description: 维护特定于进程的上下文信息的驱动程序必须在 DispatchCleanup 例程中处理清除请求。
ms.date: 08/12/2017
ms.assetid: 097f5f1d-3e88-4db0-bb79-db2267bdaf38
keywords:
- IRP_MJ_CLEANUP 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 2305708032d2ad491766481b78194de4af836efd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828135"
---
# <a name="irp_mj_cleanup"></a>IRP\_MJ\_CLEANUP


维护特定于进程的上下文信息的驱动程序必须在[*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中处理清除请求。

<a name="when-sent"></a>发送时间
---------

此请求的接收表明已关闭与目标设备对象相关联的文件对象的最后一个句柄，但由于未完成的 i/o 请求，可能尚未释放。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

此 IRP 在关闭文件对象句柄的进程的上下文中发送。 因此，驱动程序应释放先前锁定或映射的特定于进程的资源，例如用户内存。

如果驱动程序的设备对象设置为 "专用"，以便一次只有一个线程可以使用设备，则驱动程序必须将当前排队的每个 IRP 都完成为目标设备对象，并在每个 IRP 的 i/o 状态块中设置 "状态\_" 已取消 "。

否则，驱动程序必须取消并只完成当前排队的 Irp，该 Irp 与正在发布的文件对象句柄关联。 （指向文件对象的指针位于 IRP 的 " [ **\_堆栈" 堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的 " **FileObject** " 成员中。）取消这些已排队的 Irp 后，该驱动程序将完成清除 IRP 并在其 i/o 状态块中设置状态\_SUCCESS。

有关处理此请求的详细信息，请参阅[DispatchCleanup 例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchcleanup-routines)。

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


[*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IRP\_MJ\_关闭**](irp-mj-close.md)

 

 




