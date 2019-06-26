---
title: IRP_MJ_CLEANUP
description: 维护特定于进程的上下文信息的驱动程序必须处理 DispatchCleanup 例程中的清理请求。
ms.date: 08/12/2017
ms.assetid: 097f5f1d-3e88-4db0-bb79-db2267bdaf38
keywords:
- IRP_MJ_CLEANUP Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 47c51e1c775002577f4d2ae9f89ac95cbc6c439f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370917"
---
# <a name="irpmjcleanup"></a>IRP\_MJ\_CLEANUP


维护特定于进程的上下文信息的驱动程序必须处理中的清除请求[ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

<a name="when-sent"></a>发送时间
---------

此请求的回执指示与目标设备对象相关联的文件对象的最后一个句柄已关闭 （但是，由于未完成 I/O 请求，可能不具有已发布）。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

此 IRP 发送关闭文件对象句柄的进程的上下文中。 因此，驱动程序应释放特定于进程的资源，例如用户内存、 驱动程序以前锁定或映射。

如果已设置驱动程序的设备对象设置为独占，以便只有一个线程可以一次使用设备驱动程序必须完成每个 IRP 的当前排队到目标设备对象并将状态设置\_中每个 IRP I/O 状态已取消块。

否则为该驱动程序必须取消和完成仅与正在发布文件对象句柄相关联的当前排队的 Irp。 (指向文件对象的指针是否位于**的文件对象**驱动程序的成员[ **IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)的 IRP。)取消这些排队 Irp 后，该驱动程序完成清理 IRP 和设置状态\_它 I/O 状态块中的取得成功。

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
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**IO\_堆栈\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)

[**IRP\_MJ\_CLOSE**](irp-mj-close.md)

 

 




