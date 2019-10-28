---
title: FSCTL_REQUEST_OPLOCK 控制代码
description: FSCTL\_请求\_OPLOCK 控制代码请求文件上的机会锁（OPLOCK），或确认发生 OPLOCK 中断。
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
ms.openlocfilehash: 183ea154d8e53243c22056c5532349e0a71451a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841254"
---
# <a name="fsctl_request_oplock-control-code"></a>FSCTL\_请求\_OPLOCK 控制代码


**FSCTL\_请求\_oplock**控制代码请求文件上的机会锁（OPLOCK），或确认发生 OPLOCK 中断。

有关机会锁定的详细信息，请参阅 Windows 桌面文档中的[机会锁](https://docs.microsoft.com/windows/desktop/FileIO/opportunistic-locks)。 有关用户模式 OPLOCK 控制的详细信息，请参阅 Windows 桌面文档中的[文件管理控制代码](https://docs.microsoft.com/windows/desktop/FileIO/file-management-control-codes)。

为了处理此控制代码，文件系统或筛选器驱动程序使用以下参数调用[**FsRtlOplockFsctrlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex) 。

**Parameters**

<a href="" id="oplock"></a>*机会*  
文件的不透明 oplock 对象指针。

<a href="" id="irp"></a>*Irp*  
一个指针，它指向 IRP 的 IRP\_MJ\_文件\_系统\_控制 FSCTL 请求。 操作的*FsControlCode*参数必须是 FSCTL\_请求\_OPLOCK。

<a href="" id="opencount"></a>*OpenCount*  
如果请求用于排他 oplock，则为该文件的用户句柄数。 如果请求针对可共享的 oplock，则如果文件中不存在任何字节范围锁，则*OpenCount*为零。 否则， *OpenCount*为非零值。 调用方可以调用 IRP 上的[**FsRtlOplockIsSharedRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockissharedrequest)例程来确定请求是否用于可共享的 oplock。

<a href="" id="flags"></a>*随意*  
关联的 oplock 操作的位掩码。 文件系统或筛选器驱动程序设置位以指定[**FsRtlOplockFsctrlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)的行为。 *Flags*参数具有以下选项：

<a href="" id="oplock-fsctrl-flag-all-keys-match--0x00000001-"></a>OPLOCK\_FSCTRL\_标志\_所有\_密钥\_匹配（0x00000001）  
指定文件系统已验证所有机会锁定键是否与当前打开的任何句柄匹配。 通过指定此标志，在存在多个打开的文件句柄时，oplock 包可以授予级别为 RW 或 RWH 的 oplock。 有关 oplock 类型的详细信息，请参阅[概述](https://docs.microsoft.com/windows-hardware/drivers/ifs/overview)。

<a name="status-block"></a>状态块
------------

对于此操作， [**FsRtlOplockFsctrlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)返回以下 NTSTATUS 值之一：

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
<td align="left">Ntifs （包括 Ntifs 或 Fltkernel）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**FsRtlOplockFsctrlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockfsctrlex)

[**FsRtlOplockIsSharedRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtloplockissharedrequest)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

 

 






