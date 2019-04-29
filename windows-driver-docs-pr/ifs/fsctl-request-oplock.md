---
title: FSCTL_REQUEST_OPLOCK 控制代码
description: FSCTL\_请求\_OPLOCK 控制代码请求对文件的机会锁 (oplock) 或确认破坏 oplock 发生。
ms.assetid: a36f2a13-d450-4903-b999-6ba574ab3f6e
keywords:
- FSCTL_REQUEST_OPLOCK 控制代码可安装文件系统驱动程序
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
ms.openlocfilehash: cb0a204fb81b43ce9e4160ab280dfb29848f46d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372693"
---
# <a name="fsctlrequestoplock-control-code"></a>FSCTL\_请求\_OPLOCK 控制代码


**FSCTL\_请求\_OPLOCK**控制代码请求对文件的机会锁 (oplock) 或确认破坏 oplock 发生。

机会锁有关的详细信息，请参阅[机会锁](https://docs.microsoft.com/windows/desktop/FileIO/opportunistic-locks)Windows 桌面文档中。 有关用户模式 OPLOCK 控件的详细信息，请参阅[文件管理控制代码](https://docs.microsoft.com/windows/desktop/FileIO/file-management-control-codes)Windows 桌面文档中。

若要处理此控制代码，文件系统或筛选器驱动程序调用[ **FsRtlOplockFsctrlEx** ](https://msdn.microsoft.com/library/windows/hardware/ff547113)使用以下参数。

**Parameters**

<a href="" id="oplock"></a>*Oplock*  
该文件的不透明 oplock 对象指针。

<a href="" id="irp"></a>*Irp*  
指向 IRP IRP\_MJ\_文件\_系统\_控件 FSCTL 请求。 *FsControlCode*操作的参数必须为 FSCTL\_请求\_OPLOCK。

<a href="" id="opencount"></a>*OpenCount*  
该请求是否为独占 oplock，文件句柄的用户数。 如果请求是针对可共享 oplock *OpenCount*为零，如果该文件不存在任何字节范围锁。 否则为*OpenCount*为非零值。 调用方可以调用[ **FsRtlOplockIsSharedRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547128)例程上 IRP，以确定请求是否为可共享 oplock。

<a href="" id="flags"></a>*标志*  
关联的 oplock 操作一个位掩码。 文件系统或筛选器驱动程序设置以指定的行为的位[ **FsRtlOplockFsctrlEx**](https://msdn.microsoft.com/library/windows/hardware/ff547113)。 *标志*参数具有以下选项：

<a href="" id="oplock-fsctrl-flag-all-keys-match--0x00000001-"></a>OPLOCK\_FSCTRL\_标志\_所有\_密钥\_匹配 (0x00000001)  
指定文件系统已验证所有伺机锁定密钥匹配任何当前已打开的句柄。 通过指定此标志，oplock 包可以授予级别 RW 或 RWH 的 oplock 时存在的文件的多个打开句柄。 有关 oplock 类型的详细信息，请参阅[概述](https://msdn.microsoft.com/library/windows/hardware/ff551011)。

<a name="status-block"></a>状态块
------------

[**FsRtlOplockFsctrlEx** ](https://msdn.microsoft.com/library/windows/hardware/ff547113)返回值对于此操作的以下 NTSTATUS 之一：

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
<td align="left"><p>被授予 oplock。 这是一个成功代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_CANCELLED</strong></p></td>
<td align="left"><p>IRP FSCTL_REQUEST_OPLOCK 操作已完成之前取消。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_OPLOCK_NOT_GRANTED</strong></p></td>
<td align="left"><p>不被授予 oplock。 这是一个错误代码。</p></td>
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
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h 或 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FsRtlOplockFsctrlEx**](https://msdn.microsoft.com/library/windows/hardware/ff547113)

[**FsRtlOplockIsSharedRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547128)

[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)

 

 






