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
ms.openlocfilehash: 21480769e65f93c1e433ee74dfd1c3a1513c1be8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841082"
---
# <a name="mrxqueryvolumeinfo-routine"></a>MRxQueryVolumeInfo 例程


*MRxQueryVolumeInfo*例程由[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用，请求网络最小化重定向器查询卷信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryVolumeInfo;

NTSTATUS MRxQueryVolumeInfo(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>参数
----------

*RxContext* \[in，out\]  
指向 RX\_上下文结构的指针。 此参数包含请求操作的 IRP。

<a name="return-value"></a>返回值
------------

*MRxQueryVolumeInfo*返回成功的状态\_成功或使用适当的 NTSTATUS 值，如以下之一：

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
<p>应将此返回值视为成功，并且应尽可能多的有效数据返回到由<em>RxContext</em>参数指向的 RX_CONTEXT 结构的<strong>信息. Buffer</strong>成员中。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>缓冲区太小，无法接收请求的数据。</p>
<p>如果返回此值，则<em>RxContext</em>参数指向的 RX_CONTEXT 结构的<strong>InformationToReturn</strong>成员应设置为预期缓冲区的最小大小，以便调用成功。</p></td>
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

在以下任一情况下，RDBSS 都会发出对*MRxQueryVolumeInfo*的调用：

-   RDBSS 接收[**IRP\_MJ\_QUERY\_VOLUME\_信息**](irp-mj-query-volume-information.md)请求。

-   RDBSS 接收[**IRP\_MJ\_文件\_系统\_控制**](irp-mj-file-system-control.md)请求 FSCTL\_LMR\_获取\_链接\_跟踪\_信息控制代码。

在为 IRP\_MJ\_QUERY\_VOLUME\_信息请求的情况下调用*MRxQueryVolumeInfo*之前，RDBSS 会修改*RXCONTEXT*指向的 RX\_上下文结构中的以下成员。参数

**FsInformationClass**成员设置为**IrpSp-&gt;QueryVolume. FsInformationClass**。

**Info. Buffer**成员设置为**Irp-&gt;AssociatedIrp. SystemBuffer**。

**LengthRemaining**成员设置为**IrpSp-&gt;QueryVolume**。

对于 IRP\_MJ\_QUERY\_VOLUME\_信息请求，如果在从*MRxQueryVolumeInfo*返回时 RX\_上下文结构的**PostRequest**成员为**TRUE** ，则 RDBSS 将调用[**RxFsdPostRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)发送请求。 在这种情况下，IRP\_MJ\_QUERY\_VOLUME\_信息请求会传递 RX\_上下文结构，将 RX\_上下文传递给辅助队列，以供文件系统进程（FSP）进行处理。

如果 RX\_上下文结构的**PostRequest**成员在从*MRxQueryVolumeInfo*返回时为**FALSE** ，则网络小型重定向程序必须将 RX\_上下文结构的**LengthRemaining**成员设置为返回的卷信息的长度。 RDBSS 将 IRP 的**IoStatus**成员设置为**IrpSp-&gt;参数。 QueryVolume**减去 RX\_上下文结构的**信息。**

如果对*MRxQueryVolumeInfo*的调用成功，则网络小型重定向程序应将\_RX 的**LengthRemaining**成员设置为**info。 length**成员减去卷信息的长度返回. 如果对*MRxQueryVolumeInfo*的调用成功，则 RDBSS 会将 IRP 的 IoStatus 成员设置为 **&gt;IrpSp** ，并**将的**成员减到 RX\_上下文结构。

对于 IRP\_MJ\_QUERY\_VOLUME\_信息请求，并将**FsInformationClass**成员设置为**FileFsDeviceInformation**，网络小型重定向器会在 RX 中返回以下信息 @no__*RxContext*参数指向的 t_6_ 上下文结构：

**Info. Buffer**成员包含文件\_FS\_设备\_信息结构

**信息. Buffer**成员设置为卷的特征，其中必须包含文件\_远程\_设备作为选项之一。

**DeviceType**成员设置为关联的 NET\_根结构的**DeviceType**成员。 如果关联的 NET\_根的**类型**成员是 NET\_根\_管道，则将**DeviceType**成员设置为\_名为\_管道的设备\_的文件。

对于 IRP\_MJ\_QUERY\_VOLUME\_信息请求，并将**FsInformationClass**成员设置为**FileFsVolumeInformation**，网络小型重定向器会在 RX 中返回以下信息 @no__*RxContext*参数指向的 t_6_ 上下文结构：

**Info. Buffer**成员包含文件\_FS\_卷\_信息结构。

**Info. Buffer**成员设置为关联的 NET\_根结构的**VolumeInfo**成员。

**LengthRemaining**成员设置为关联的 NET\_根结构的**VolumeInfoLength**成员。

用于[**IRP\_MJ\_文件\_系统\_控件**](irp-mj-file-system-control.md)*的 RDBSS 调用是*对链接跟踪信息的请求。 在为 IRP\_MJ\_FILE\_SYSTEM\_CONTROL 之前调用*MRxQueryVolumeInfo*之前，RDBSS 会修改*RxContext*参数指向的 RX\_上下文结构中的以下成员：

**FsInformationClass**成员设置为**FileFsObjectIdInformation**。

信息 **. Buffer**成员设置为\_FS\_OBJECTID\_信息结构的文件。

**LengthRemaining**成员设置为**sizeof**（FILE\_FS\_OBJECTID\_信息）。

对于 IRP\_MJ\_文件\_系统\_控制请求的这种情况，IRP 的**SystemBuffer**成员指向链接\_跟踪\_信息结构。

如果请求作为 IRP 启动\_MJ\_文件\_系统\_控件到*MRxQueryVolumeInfo* ，返回值为状态\_成功或状态\_缓冲区\_溢出，RDBSS 会将文件\_FS\_OBJECTID\_信息结构中**传递的** **OBJECTID**成员作为 RX\_上下文结构传递到**NetRoot-&gt;** FCB 结构的 DiskParameters 成员，以及 IRP 的**AssociatedIrp**成员的成员。 如果对*MRxQueryVolumeInfo*的调用成功，则 RDBSS 会将链接的**类型**成员设置\_跟踪\_信息结构。 如果 FCB 结构的 **&gt;NetRoot 标志**成员具有 NETROOT\_标志\_DFS\_感知\_NetRoot 位集，则**类型**成员由 RDBSS 设置为**DfsLinkTrackingInformation**。 如果 FCB 结构的 **&gt;NetRoot Flags**成员没有 NETROOT\_标志\_DFS\_感知\_NetRoot 位集，则**类型**成员由 RDBSS 设置为**NtfsLinkTrackingInformation**。 成功后，RDBSS 会将 IRP 的**IoStatus**成员设置\_跟踪\_信息结构的链接大小。

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
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Mrx （包括 Mrx）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MRxIsValidDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown)

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

[**RxFsdPostRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)

 

 






