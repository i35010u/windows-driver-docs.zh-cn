---
title: FSCTL_OPLOCK_BREAK_ACKNOWLEDGE 控制代码
description: FSCTL \_ oplock \_ 中断 \_ 确认控制代码响应，指出文件上的独占 (级别1、批处理或筛选器) 机会锁定 () OPLOCK 锁定已中断。
ms.assetid: 067aa36b-fa5b-4bc8-bcec-e221509c0d4d
keywords:
- FSCTL_OPLOCK_BREAK_ACKNOWLEDGE 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_OPLOCK_BREAK_ACKNOWLEDGE
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69182fa71800e8d0a7a10e2caf9e36af1e48b93f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066186"
---
# <a name="fsctl_oplock_break_acknowledge-control-code"></a>FSCTL \_ OPLOCK \_ 中断 \_ 确认控制代码


**FSCTL \_ oplock \_ 中断 \_ 确认**控制代码响应，指出文件上的独占 (级别1、批处理或筛选器) 机会锁定 () OPLOCK 锁定已中断。

客户端应用程序发送此控制代码以指示它确认 oplock 中断，并且，如果 oplock 是已分解为级别2的第1级 oplock，则它需要2级 oplock。

若要处理此控制代码，微筛选器将使用以下参数调用 [**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl) 。 文件系统或旧筛选器驱动程序调用 [**FsRtlOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)。

有关机会锁定和 **FSCTL \_ OPLOCK \_ 中断 \_ 确认** 控制代码的详细信息，请参阅 Microsoft Windows SDK 文档。

**参数**

<a href="" id="oplock"></a>*机会*  
文件的不透明 oplock 对象指针。

<a href="" id="callbackdata"></a>*CallbackData*  
仅[**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl) 。 为 IRP MJ [** \_ \_ **](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data) \_ \_ 文件 \_ 系统 \_ 控制 FSCTL 请求 (FLT 回调数据) 结构的回叫数据。 操作的 *FsControlCode* 参数必须是 FSCTL \_ OPLOCK \_ 中断 \_ 确认。

<a href="" id="irp"></a>*Irp*  
仅[**FsRtlOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl) 。 Irp \_ MJ \_ 文件 \_ 系统 \_ 控件 FSCTL 请求。 操作的 *FsControlCode* 参数必须是 FSCTL \_ OPLOCK \_ 中断 \_ 确认。

<a href="" id="opencount"></a>*OpenCount*  
不与此操作一起使用;设置为零。

<a name="status-block"></a>状态块
------------

[**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl) \_ \_ 如果第1级 oplock 被分解为级别2，并且已授予2级 oplock，则 FltOplockFsctrl 将为此操作返回 FLT PREOP。 否则，它会返回 FLT \_ PREOP \_ COMPLETE。

对于此操作， [**FsRtlOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)返回以下 NTSTATUS 值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_SUCCESS</strong></p></td>
<td align="left"><p>将确认 oplock 中断。 不保留剩余的 oplock。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_OPLOCK_PROTOCOL</strong></p></td>
<td align="left"><p>此句柄未持有 oplock，或 oplock 中断当前未进行。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_PENDING</strong></p></td>
<td align="left"><p>将确认 oplock 中断。 返回时， <strong>FSCTL_OPLOCK_BREAK_ACKNOWLEDGE</strong> 控制代码的发件人包含2级 OPLOCK。 这是一个成功代码。</p></td>
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
<td align="left">Ntifs (包含 Ntifs 或 Fltkernel) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT \_ 参数**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**\_IRP \_ MJ \_ 文件 \_ 系统 \_ 控件的 FLT 参数**](flt-parameters-for-irp-mj-file-system-control.md)

[**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl)

[**FSCTL \_ OPBATCH \_ ACK \_ CLOSE \_ 挂起**](fsctl-opbatch-ack-close-pending.md)

[**FSCTL \_ OPLOCK \_ 中断 \_ ACK \_ NO \_ 2**](fsctl-oplock-break-ack-no-2.md)

[**FSCTL \_ OPLOCK \_ 中断 \_ 通知**](fsctl-oplock-break-notify.md)

[**FSCTL \_ 请求 \_ 批处理 \_ OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL \_ 请求 \_ 筛选器 \_ OPLOCK**](fsctl-request-filter-oplock.md)

[**FSCTL \_ 请求 \_ OPLOCK \_ LEVEL \_ 1**](fsctl-request-oplock-level-1.md)

[**FSCTL \_ 请求 \_ OPLOCK \_ LEVEL \_ 2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)

[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](irp-mj-file-system-control.md)

 

