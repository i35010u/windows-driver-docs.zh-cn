---
title: IRP_MJ_CLOSE
description: 每个驱动程序必须处理 DispatchClose 例程，但可能不能禁用或不降低系统性能的情况下从计算机中删除其设备的驱动程序中的关闭请求。
ms.date: 08/12/2017
ms.assetid: 109819a8-3787-448d-a766-5d53dbcf55f4
keywords:
- IRP_MJ_CLOSE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 46dcf7742a7c57527dd6e3206890c263e493ccd5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520115"
---
# <a name="irpmjclose"></a>IRP\_MJ\_CLOSE


每个驱动程序必须处理中的关闭请求[ *DispatchClose* ](separate-dispatchcreate-and-dispatchclose-routines.md)例程，但可能不能禁用或不降低系统性能的情况下从计算机中删除其设备的驱动程序. 其设备拥有系统页面文件磁盘驱动程序是这样的驱动程序的示例。 请注意，此类设备的驱动程序也不能卸载动态。

<a name="when-sent"></a>发送时间
---------

此请求的回执指示已关闭并释放与目标设备对象相关联的文件对象的最后一个句柄。 已完成或取消所有未完成的 I/O 请求。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

许多设备和中间驱动程序只是将状态设置\_I/O 状态成功 IRP 的阻止和完成关闭请求。 但是，给定的驱动程序在收到关闭请求的作用取决于驱动程序的设计。 一般情况下，驱动程序应撤消所需的任何操作[ **IRP\_MJ\_创建**](irp-mj-create.md)请求。 设备驱动程序的设备对象是独占的如串行驱动程序，还可以重置收到关闭请求上的硬件。

**IRP\_MJ\_关闭**关闭文件对象句柄的进程的上下文中不一定是发送请求。 如果该驱动程序必须释放特定于进程的资源，如用户内存，该驱动程序以前锁定，或映射，它必须执行操作以响应[ **IRP\_MJ\_清理**](irp-mj-cleanup.md)请求。

**IRP\_MJ\_关闭**始终会在被动时发送请求\_级别。

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
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[*DispatchClose*](separate-dispatchcreate-and-dispatchclose-routines.md)

[**IRP\_MJ\_CLEANUP**](irp-mj-cleanup.md)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

 

 




