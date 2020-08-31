---
title: FSCTL_REQUEST_FILTER_OPLOCK 控制代码
description: FSCTL \_ 请求 \_ 筛选器 \_ OPLOCK 控制代码请求对文件进行) 的筛选器机会锁 (OPLOCK。
ms.assetid: 9d6b2773-db87-492c-8fe9-f5fd4ef2eb7b
keywords:
- FSCTL_REQUEST_FILTER_OPLOCK 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_REQUEST_FILTER_OPLOCK
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 262079979a6776079607ad37046b9b45c24cc5d5
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063370"
---
# <a name="fsctl_request_filter_oplock-control-code"></a>FSCTL \_ 请求 \_ 筛选器 \_ OPLOCK 控制代码


**FSCTL \_ 请求 \_ 筛选器 \_ OPLOCK**控制代码请求对文件进行) 的筛选器机会锁 (OPLOCK。

若要处理此控制代码，微筛选器将使用以下参数调用 [**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl) 。 文件系统或旧筛选器驱动程序调用 [**FsRtlOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)。

有关机会锁定以及有关 **FSCTL \_ 请求 \_ 筛选器 \_ OPLOCK** 控制代码的详细信息，请参阅 Microsoft Windows SDK 文档。

**参数**

<a href="" id="oplock"></a>*机会*  
文件的不透明 oplock 对象指针。

<a href="" id="callbackdata"></a>*CallbackData*  
仅[**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl) 。 为 IRP MJ [** \_ \_ **](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data) \_ \_ 文件 \_ 系统 \_ 控制 FSCTL 请求 (FLT 回调数据) 结构的回叫数据。 操作的 *FsControlCode* 参数必须是 FSCTL \_ 请求 \_ 筛选器 \_ OPLOCK。

<a href="" id="irp"></a>*Irp*  
仅[**FsRtlOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl) 。 Irp \_ MJ \_ 文件 \_ 系统 \_ 控件 FSCTL 请求。 操作的 *FsControlCode* 参数必须是 FSCTL \_ 请求 \_ 筛选器 \_ OPLOCK。

<a href="" id="opencount"></a>*OpenCount*  
文件的用户句柄数。

<a name="status-block"></a>状态块
------------

[**FltOplockFsctrl**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltoplockfsctrl) \_ \_ 如果已授予 oplock，FltOplockFsctrl 将为此操作返回 FLT PREOP。 否则，它会返回 FLT \_ PREOP \_ COMPLETE。

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
<td align="left"><p><strong>STATUS_PENDING</strong></p></td>
<td align="left"><p>已授予 oplock。 这是一个成功代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_CANCELLED</strong></p></td>
<td align="left"><p>IRP 在 FSCTL_REQUEST_BATCH_OPLOCK 操作完成前被取消。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_OPLOCK_NOT_GRANTED</strong></p></td>
<td align="left"><p>无法授予 oplock。 这是一个错误代码。</p></td>
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

[**FSCTL \_ OPLOCK \_ 中断 \_ 确认**](fsctl-oplock-break-acknowledge.md)

[**FSCTL \_ OPLOCK \_ 中断 \_ 通知**](fsctl-oplock-break-notify.md)

[**FSCTL \_ 请求 \_ 批处理 \_ OPLOCK**](fsctl-request-batch-oplock.md)

[**FSCTL \_ 请求 \_ OPLOCK \_ LEVEL \_ 1**](fsctl-request-oplock-level-1.md)

[**FSCTL \_ 请求 \_ OPLOCK \_ LEVEL \_ 2**](fsctl-request-oplock-level-2.md)

[**FsRtlOplockFsctrl**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrl)

[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](irp-mj-file-system-control.md)

 

