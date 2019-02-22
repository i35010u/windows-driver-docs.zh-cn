---
title: FSCTL_OPLOCK_BREAK_ACK_NO_2 control code
description: FSCTL\_OPLOCK\_中断\_ACK\_否\_2 的控制代码响应通知的排他 （级别 1、 批处理或筛选器） 文件中的机会锁 (oplock) 已中断。
ms.assetid: f76c98ba-e0bf-4b86-bda4-92f233ea5839
keywords:
- FSCTL_OPLOCK_BREAK_ACK_NO_2 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_OPLOCK_BREAK_ACK_NO_2
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2885de10de1e1d9c31986ce23b5af9f853e4bff5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522538"
---
# <a name="fsctloplockbreakackno2-control-code"></a>FSCTL\_OPLOCK\_中断\_ACK\_否\_2 控制代码


**FSCTL\_OPLOCK\_中断\_ACK\_否\_2**控制代码响应通知的排他 （级别 1、 批处理或筛选器） 机会锁 (oplock)文件已损坏。

客户端应用程序将发送此控制代码，以指示它确认破坏 oplock，并且，如果 oplock 已断开为级别 2 级别 1 oplock，它不希望级别 2 oplock。

若要处理此控制代码，微筛选器调用[ **FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)使用以下参数。 文件系统或旧筛选器驱动程序调用[ **FsRtlOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff547112)。

有关详细信息，有关伺机锁定以及 FSCTL\_OPLOCK\_中断\_ACK\_否\_2 控制代码，请参阅 Microsoft Windows SDK 文档。

**参数**

<a href="" id="oplock"></a>*Oplock*  
该文件的不透明 oplock 对象指针。

<a href="" id="callbackdata"></a>*CallbackData*  
[**FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)仅。 回调数据 ([**FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 的 IRP 结构\_MJ\_文件\_系统\_控件 FSCTL请求。 *FsControlCode*操作的参数必须为 FSCTL\_OPLOCK\_中断\_ACK\_否\_2。

<a href="" id="irp"></a>*Irp*  
[**FsRtlOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff547112)仅。 IRP 的 IRP\_MJ\_文件\_系统\_控件 FSCTL 请求。 *FsControlCode*操作的参数必须为 FSCTL\_OPLOCK\_中断\_ACK\_否\_2。

<a href="" id="opencount"></a>*OpenCount*  
不用于此操作;设置为零。

<a name="status-block"></a>状态块
------------

[**FltOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff543398)始终返回 FLT\_PREOP\_完成此操作。

[**FsRtlOplockFsctrl** ](https://msdn.microsoft.com/library/windows/hardware/ff547112)返回值对于此操作的以下 NTSTATUS 之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_SUCCESS</strong></p></td>
<td align="left"><p>确认破坏 oplock。 不保存任何剩余 oplock。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_OPLOCK_PROTOCOL</strong></p></td>
<td align="left"><p>通过此句柄，持有没有机会锁的时间或需要破坏 oplock 不是当前正在进行中。 这是一个错误代码。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h 或 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT\_CALLBACK\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FLT\_IRP 的参数\_MJ\_文件\_系统\_控件**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff543398)

[**FSCTL\_OPBATCH\_ACK\_CLOSE\_PENDING**](fsctl-opbatch-ack-close-pending.md)

[**FSCTL\_OPLOCK\_BREAK\_ACKNOWLEDGE**](fsctl-oplock-break-acknowledge.md)

[**FSCTL\_OPLOCK\_BREAK\_NOTIFY**](fsctl-oplock-break-notify.md)

[**FSCTL\_REQUEST\_BATCH\_OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL\_REQUEST\_FILTER\_OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL\_REQUEST\_OPLOCK\_LEVEL\_1**](fsctl-request-oplock-level-1.md)

[**FSCTL\_REQUEST\_OPLOCK\_LEVEL\_2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](https://msdn.microsoft.com/library/windows/hardware/ff547112)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

 

 






