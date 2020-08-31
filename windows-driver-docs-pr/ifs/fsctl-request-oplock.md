---
title: FSCTL_REQUEST_OPLOCK 控制代码
description: FSCTL \_ 请求 \_ oplock 控制代码请求) 文件的 oplock (锁定，或确认发生 OPLOCK 中断。
ms.assetid: a36f2a13-d450-4903-b999-6ba574ab3f6e
keywords:
- FSCTL_REQUEST_OPLOCK 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_REQUEST_OPLOCK
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bae4ae9fc68cc29c300610681ba59926a309147b
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063364"
---
# <a name="fsctl_request_oplock-control-code"></a>FSCTL \_ 请求 \_ OPLOCK 控制代码


**FSCTL \_ 请求 \_ oplock**控制代码请求) 文件的 oplock (锁定，或确认发生 OPLOCK 中断。

有关机会锁定的详细信息，请参阅 Windows 桌面文档中的 [机会锁](/windows/desktop/FileIO/opportunistic-locks) 。 有关用户模式 OPLOCK 控制的详细信息，请参阅 Windows 桌面文档中的 [文件管理控制代码](/windows/desktop/FileIO/file-management-control-codes) 。

为了处理此控制代码，文件系统或筛选器驱动程序使用以下参数调用 [**FsRtlOplockFsctrlEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex) 。

**参数**

<a href="" id="oplock"></a>*机会*  
文件的不透明 oplock 对象指针。

<a href="" id="irp"></a>*Irp*  
指向 IRP \_ MJ \_ 文件 \_ 系统 \_ 控件 FSCTL 请求的 irp 的指针。 操作的 *FsControlCode* 参数必须是 FSCTL \_ 请求 \_ OPLOCK。

<a href="" id="opencount"></a>*OpenCount*  
如果请求用于排他 oplock，则为该文件的用户句柄数。 如果请求针对可共享的 oplock，则如果文件中不存在任何字节范围锁，则 *OpenCount* 为零。 否则， *OpenCount* 为非零值。 调用方可以调用 IRP 上的 [**FsRtlOplockIsSharedRequest**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockissharedrequest) 例程来确定请求是否用于可共享的 oplock。

<a href="" id="flags"></a>*随意*  
关联的 oplock 操作的位掩码。 文件系统或筛选器驱动程序设置位以指定 [**FsRtlOplockFsctrlEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)的行为。 *Flags*参数具有以下选项：

<a href="" id="oplock-fsctrl-flag-all-keys-match--0x00000001-"></a>OPLOCK \_ FSCTRL \_ 标志 \_ 所有 \_ 键都 \_ 匹配 (0x00000001)   
指定文件系统已验证所有机会锁定键是否与当前打开的任何句柄匹配。 通过指定此标志，在存在多个打开的文件句柄时，oplock 包可以授予级别为 RW 或 RWH 的 oplock。 有关 oplock 类型的详细信息，请参阅 [概述](./oplock-overview.md)。

<a name="status-block"></a>状态块
------------

对于此操作， [**FsRtlOplockFsctrlEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)返回以下 NTSTATUS 值之一：

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
<td align="left"><p>IRP 在 FSCTL_REQUEST_OPLOCK 操作完成前被取消。 这是一个错误代码。</p></td>
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


[**FsRtlOplockFsctrlEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)

[**FsRtlOplockIsSharedRequest**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockissharedrequest)

[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](irp-mj-file-system-control.md)

 

