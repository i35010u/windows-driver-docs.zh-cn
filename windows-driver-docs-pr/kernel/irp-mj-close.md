---
title: IRP_MJ_CLOSE
description: 每个驱动程序必须在 DispatchClose 例程中处理关闭请求，这可能会导致无法在不关闭系统的情况下在计算机上禁用或删除其设备的驱动程序例外。
ms.date: 08/12/2017
keywords:
- IRP_MJ_CLOSE Kernel-Mode 驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 7db7234b9c422c57e7e60f08e6b82ad6becc7bb6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833417"
---
# <a name="irp_mj_close"></a>IRP\_MJ\_CLOSE


每个驱动程序必须在 [*DispatchClose*](separate-dispatchcreate-and-dispatchclose-routines.md) 例程中处理关闭请求，这可能会导致无法在不关闭系统的情况下在计算机上禁用或删除其设备的驱动程序例外。 其设备包含系统页面文件的磁盘驱动程序就是这样一个驱动程序的示例。 请注意，此类设备的驱动程序也无法动态卸载。

<a name="when-sent"></a>发送时间
---------

此请求的接收表明已关闭并释放与目标设备对象相关联的文件对象的最后一个句柄。 所有未完成的 i/o 请求均已完成或取消。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

许多设备和中间驱动程序只是 \_ 在 IRP 的 i/o 状态块中设置状态 "成功" 并完成关闭请求。 但是，给定的驱动程序在收到关闭请求时所执行的操作取决于驱动程序的设计。 通常，驱动程序应撤消在收到 [**IRP \_ MJ \_ CREATE**](irp-mj-create.md) 请求时所执行的任何操作。 设备对象专用（如串行驱动程序）的设备驱动程序还可以在收到关闭请求时重置硬件。

**IRP \_ MJ \_ 关闭** 请求不一定在关闭文件对象句柄的进程的上下文中发送。 如果驱动程序必须释放该驱动程序以前锁定或映射的特定于进程的资源（例如用户内存），则它必须为响应 [**IRP \_ MJ \_ 清除**](irp-mj-cleanup.md) 请求而执行此操作。

**IRP \_ MJ \_ 关闭** 请求将始终在被动级别发送 \_ 。

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

## <a name="see-also"></a>请参阅

[*DispatchClose*](separate-dispatchcreate-and-dispatchclose-routines.md)

[**IRP \_ MJ \_ 清除**](irp-mj-cleanup.md)

[**IRP \_ MJ \_ 创建**](irp-mj-create.md)

 

 




