---
title: MRxQueryVolumeInfo 例程
description: MRxQueryVolumeInfo 例程由 RDBSS 调用，请求网络最小化重定向器查询卷信息。
ms.assetid: 28e36992-2b6b-4484-9e7e-2cea7a2953e9
keywords:
- MRxQueryVolumeInfo 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxQueryVolumeInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf9b40902f2569bfcfd1c22aaf172cb9ad176883
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066888"
---
# <a name="mrxqueryvolumeinfo-routine"></a>MRxQueryVolumeInfo 例程


*MRxQueryVolumeInfo*例程由[RDBSS](./the-rdbss-driver-and-library.md)调用，请求网络最小化重定向器查询卷信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryVolumeInfo;

NTSTATUS MRxQueryVolumeInfo(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>parameters
----------

*RxContext* \[in、out\]  
指向 RX \_ 上下文结构的指针。 此参数包含请求操作的 IRP。

<a name="return-value"></a>返回值
------------

*MRxQueryVolumeInfo* 返回成功的状态 \_ 成功或适当的 NTSTATUS 值，如以下之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回代码</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_ACCESS_DENIED</strong></td>
<td align="left"><p>调用方缺乏此操作的正确安全性。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_BUFFER_OVERFLOW</strong></td>
<td align="left"><p>用于接收卷信息的缓冲区太小。</p>
<p>应将此返回值视为成功，并尽可能多地在<em>RxContext</em>参数指向的 RX_CONTEXT 结构的<strong>信息. Buffer</strong>成员中返回尽可能多的数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>缓冲区太小，无法接收请求的数据。</p>
<p>如果返回此值，则应将<em>RxContext</em>参数指向的 RX_CONTEXT 结构的<strong>InformationToReturn</strong>成员设置为预期缓冲区的最小大小，以便调用成功。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_CONNECTION_DISCONNECTED</strong></td>
<td align="left"><p>连接已断开连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>资源不足，无法完成查询。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>指定的参数无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NETWORK_NAME_DELETED</strong></td>
<td align="left"><p>网络名称已被删除。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现所请求的功能。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在以下任一情况下，RDBSS 都会发出对 *MRxQueryVolumeInfo* 的调用：

-   RDBSS 接收 [**IRP \_ MJ \_ 查询 \_ 卷 \_ 信息**](irp-mj-query-volume-information.md) 请求。

-   RDBSS 为 FSCTL LMR 获取链接跟踪信息控制代码接收 [**IRP \_ MJ \_ 文件 \_ 系统 \_ 控制**](irp-mj-file-system-control.md) 请求 \_ \_ \_ \_ \_ 。

在 IRP MJ 查询卷信息请求的情况下调用 *MRxQueryVolumeInfo* 之前 \_ \_ \_ \_ ，RDBSS 会修改 \_ *RxContext* 参数指向的 RX 上下文结构中的以下成员：

**FsInformationClass**成员设置为**IrpSp- &gt; QueryVolume. FsInformationClass**。

**Info. Buffer**成员设置为**Irp- &gt;AssociatedIrp.SystemBuffer**。

**LengthRemaining**成员设置为**IrpSp &gt; 参数. QueryVolume**。

对于 IRP \_ MJ \_ 查询 \_ 卷 \_ 信息请求，如果在从 MRxQueryVolumeInfo 返回时 RX 上下文结构的**PostRequest**成员 \_ 为**TRUE** ， *MRxQueryVolumeInfo*则 RDBSS 将调用[**RxFsdPostRequest**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)以发送请求。 在这种情况下，IRP \_ MJ \_ 查询 \_ 卷 \_ 信息请求将传递 rx 上下文 \_ 结构以将 rx 上下文传递给辅助队列，以 \_ 供文件系统进程在 FSP)  (处理。

如果从 MRxQueryVolumeInfo 返回时 RX 上下文结构的**PostRequest**成员 \_ 为**FALSE** ， *MRxQueryVolumeInfo*则网络小型重定向程序必须将 RX 上下文结构的**LengthRemaining**成员设置 \_ 为返回的卷信息的长度。 RDBSS 将 IRP 的**IoStatus**成员设置为**IrpSp- &gt; QueryVolume**减去 RX 上下文结构的**信息. LengthRemaining**成员。 \_

如果对 *MRxQueryVolumeInfo* 的调用成功，则网络小型重定向程序应将 RX 上下文结构的 **LengthRemaining** 成员设置 \_ 为 **info。 length** 成员减去返回的卷信息的长度。 如果对*MRxQueryVolumeInfo*的调用成功，则 RDBSS 会将 IRP 的**IoStatus**成员设置为 IrpSp，而不是 RX 上下文结构的**QueryVolume**成员。 ** &gt; ** \_

对于 IRP \_ MJ \_ 查询 \_ 卷 \_ 信息请求，并将 **FsInformationClass** 成员设置为 **FileFsDeviceInformation**，网络微重定向器会返回 \_ *RxContext* 参数指向的 RX 上下文结构中的以下信息：

**Info. Buffer**成员包含文件 \_ FS \_ 设备 \_ 信息结构

**信息. Buffer**成员设置为卷的特征，其中必须包含文件 \_ 远程 \_ 设备作为选项之一。

**DeviceType**成员设置为关联的网络根结构的**DeviceType**成员 \_ 。 如果关联网络根的 **类型** 成员 \_ 为网络 \_ 根 \_ 管道，则 **DeviceType** 成员设置为文件 \_ 设备 \_ 命名 \_ 管道。

对于 IRP \_ MJ \_ 查询 \_ 卷 \_ 信息请求，并将 **FsInformationClass** 成员设置为 **FileFsVolumeInformation**，网络微重定向器会返回 \_ *RxContext* 参数指向的 RX 上下文结构中的以下信息：

**Info. Buffer**成员包含文件 \_ FS \_ 卷 \_ 信息结构。

**Info. Buffer**成员设置为关联的网络根结构的**VolumeInfo**成员 \_ 。

**LengthRemaining**成员设置为关联的网络根结构的**VolumeInfoLength**成员 \_ 。

用于[**IRP \_ MJ \_ 文件 \_ 系统 \_ 控件**](irp-mj-file-system-control.md)的 RDBSS 的*MRxQueryVolumeInfo*调用是对链接跟踪信息的请求。 在为*MRxQueryVolumeInfo* IRP \_ MJ \_ 文件系统控件调用 MRxQueryVolumeInfo 之前 \_ \_ ，RDBSS 会修改 \_ *RxContext*参数指向的 RX 上下文结构中的以下成员：

**FsInformationClass**成员设置为**FileFsObjectIdInformation**。

**Info. Buffer**成员设置为文件 \_ FS \_ OBJECTID \_ 信息结构。

**LengthRemaining**成员设置为**sizeof** (文件 \_ FS \_ OBJECTID \_ 信息) 。

对于 IRP \_ MJ \_ 文件 \_ 系统 \_ 控制请求，irp 的 **AssociatedIrp.SystemBuffer** 成员指向链接 \_ 跟踪 \_ 信息结构。

如果请求是作为 IRP \_ MJ \_ 文件系统控件启动的， \_ \_ 并且*MRxQueryVolumeInfo*返回值为状态 \_ 成功或状态 \_ 缓冲区 \_ 溢出，则 RDBSS 将传递给 MRxQueryVolumeInfo **ObjectId** \_ 结构的信息中的文件 FS \_ objectid objectid 信息结构的 objectid 成员复制 \_ **Info.Buffer** \_ 到 FCB 结构的**NetRoot- &gt; DiskParameters**成员和 IRP 的**AssociatedIrp.SystemBuffer**成员。 如果对 *MRxQueryVolumeInfo* 的调用成功，则 RDBSS 将设置链接跟踪信息结构的 **类型** 成员 \_ \_ 。 如果 FCB 结构的 **NetRoot &gt; ** 成员具有 NetRoot \_ 标记 \_ DFS \_ 感知 \_ NetRoot 位集，则 **类型** 成员由 RDBSS 设置为 **DfsLinkTrackingInformation**。 如果 FCB 结构的 **NetRoot &gt; ** 成员不具有 NetRoot \_ 标记 \_ DFS \_ 感知 \_ NetRoot 位集，则 **类型** 成员由 RDBSS 设置为 **NtfsLinkTrackingInformation**。 成功后，RDBSS 会将 IRP 的 **IoStatus** 成员设置为链接 \_ 跟踪 \_ 信息结构的大小。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面型</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Mrx (包含 Mrx) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MRxIsValidDirectory**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown)

[**MRxQueryDirectory**](mrxquerydirectory.md)

[**MRxQueryEaInfo**](mrxqueryeainfo.md)

[**MRxQueryFileInfo**](mrxqueryfileinfo.md)

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

[**RxFsdPostRequest**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)

 

