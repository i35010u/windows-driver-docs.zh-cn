---
title: MRxQueryVolumeInfo routine
description: MRxQueryVolumeInfo 例程会调用 RDBSS 来请求网络微型重定向查询卷信息。
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
ms.openlocfilehash: 09d3b8389f85c7f140adc2ab86bf9d9e41386b89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577593"
---
# <a name="mrxqueryvolumeinfo-routine"></a>MRxQueryVolumeInfo routine


*MRxQueryVolumeInfo*由调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)请求网络微型重定向查询卷的信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryVolumeInfo;

NTSTATUS MRxQueryVolumeInfo(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>Parameters
----------

*RxContext* \[in、 out\]  
指向 RX\_上下文结构。 此参数包含 IRP 请求该操作。

<a name="return-value"></a>返回值
------------

*MRxQueryVolumeInfo*将返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><p>调用方不具备适当的安全，此操作。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_BUFFER_OVERFLOW</strong></td>
<td align="left"><p>要接收的卷信息的缓冲区太小。</p>
<p>此返回值应被视为成功，并且作为有效得多的数据应该返回在<strong>Info.Buffer</strong> RX_CONTEXT 结构成员指向的<em>RxContext</em>参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>缓冲区是太小，无法接收请求的数据。</p>
<p>如果返回此值，则<strong>InformationToReturn</strong> RX_CONTEXT 结构成员指向的<em>RxContext</em>参数应设置为调用的预期缓冲区的最小大小会成功。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_CONNECTION_DISCONNECTED</strong></td>
<td align="left"><p>连接已断开连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>没有资源不足，无法完成查询。</p></td>
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
<td align="left"><p>未实现请求的功能。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 发出调用*MRxQueryVolumeInfo*以下情况之一：

-   接收 RDBSS [ **IRP\_MJ\_查询\_卷\_信息**](irp-mj-query-volume-information.md)请求。

-   接收 RDBSS [ **IRP\_MJ\_文件\_系统\_控制**](irp-mj-file-system-control.md)请求 FSCTL\_LMR\_GET\_链接\_跟踪\_信息控制代码。

然后再调用*MRxQueryVolumeInfo* IRP 对于\_MJ\_查询\_卷\_信息请求，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**Info.FsInformationClass**成员设置为**IrpSp-&gt;Parameters.QueryVolume.FsInformationClass**。

**Info.Buffer**成员设置为**Irp-&gt;AssociatedIrp.SystemBuffer**。

**Info.LengthRemaining**成员设置为**IrpSp-&gt;Parameters.QueryVolume.Length**。

有关 IRP\_MJ\_查询\_卷\_信息请求，如果**PostRequest** RX 成员\_上下文结构**TRUE**返回时从*MRxQueryVolumeInfo*，将调用 RDBSS [ **RxFsdPostRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff554472)将申请发布。 这种情况下，IRP\_MJ\_查询\_卷\_信息请求将传递 RX\_上下文结构到队列 RX\_到辅助队列中进行处理的文件系统的上下文过程 (FSP)。

如果**PostRequest** RX 成员\_CONTEXT 结构**FALSE**返回时从*MRxQueryVolumeInfo*，必须设置网络微型重定向**Info.LengthRemaining** RX 成员\_上下文结构到的卷信息长度返回。 RDBSS 集**IoStatus.Information** IRP 到成员**IrpSp-&gt;Parameters.QueryVolume.Length**减去**Info.LengthRemaining**的成员RX\_上下文结构。

如果在调用*MRxQueryVolumeInfo*是成功，则应设置网络微型重定向**Info.LengthRemaining** RX 成员\_上下文结构到**Info.Length**返回成员的卷信息长度减。 如果在调用*MRxQueryVolumeInfo*已成功，RDBSS 集**IoStatus.Information**成员到 IRP **IrpSp-&gt;Parameters.QueryVolume.Length**减去**Info.LengthRemaining** RX 成员\_上下文结构。

有关 IRP\_MJ\_查询\_卷\_信息请求**Info.FsInformationClass**成员设置为**FileFsDeviceInformation**，网络微型重定向返回以下信息中 RX\_指向上下文结构*RxContext*参数：

**Info.Buffer**成员包含的文件\_FS\_设备\_信息结构

**Info.Buffer.Characteristics**成员设置为卷，其中必须包括文件的特征\_远程\_设备作为一个选项。

**Info.Buffer.DeviceType**成员设置为**DeviceType**成员相关联的 NET\_根结构。 如果**类型**相关联的 NET 成员\_根是 NET\_根\_管道**Info.Buffer.DeviceType**成员设置为文件\_设备\_名为\_管道。

有关 IRP\_MJ\_查询\_卷\_信息请求**Info.FsInformationClass**成员设置为**FileFsVolumeInformation**，网络微型重定向返回以下信息中 RX\_指向上下文结构*RxContext*参数：

**Info.Buffer**成员包含的文件\_FS\_卷\_信息结构。

**Info.Buffer**成员设置为**VolumeInfo**成员相关联的 NET\_根结构。

**Info.LengthRemaining**成员设置为**VolumeInfoLength**成员相关联的 NET\_根结构。

*MRxQueryVolumeInfo* RDBSS 为从调用[ **IRP\_MJ\_文件\_系统\_控制**](irp-mj-file-system-control.md)是请求有关跟踪信息的链接。 然后再调用*MRxQueryVolumeInfo* IRP 有关\_MJ\_文件\_系统\_控件，RDBSS 修改 RX 中的以下成员\_上下文结构指向通过*RxContext*参数：

**Info.FsInformationClass**成员设置为**FileFsObjectIdInformation**。

**Info.Buffer**成员设置为一个文件\_FS\_OBJECTID\_信息结构。

**Info.LengthRemaining**成员设置为**sizeof**(文件\_FS\_OBJECTID\_信息)。

这种情况下的 IRP\_MJ\_文件\_系统\_控制请求**AssociatedIrp.SystemBuffer**的 IRP 成员指向链接\_跟踪\_信息结构。

如果发出一个请求作为 IRP\_MJ\_文件\_系统\_控制对*MRxQueryVolumeInfo*具有状态的返回值\_成功或状态\_缓冲区\_溢出、 RDBSS 副本**ObjectId**文件的成员\_FS\_OBJECTID\_信息结构传入**Info.Buffer**成员的 RX\_上下文结构到**NetRoot-&gt;DiskParameters.VolumeId**成员的 FCB 结构和**AssociatedIrp.SystemBuffer.VolumeId** IRP 的成员。 如果在调用*MRxQueryVolumeInfo*已成功，RDBSS 集**类型**的链接的成员\_跟踪\_信息结构。 如果**NetRoot-&gt;标志**FCB 结构的成员都有 NETROOT\_标志\_DFS\_意识到\_NETROOT 设置位，**类型**成员设置到 RDBSS **DfsLinkTrackingInformation**。 如果**NetRoot-&gt;标志**FCB 结构的成员没有 NETROOT\_标志\_DFS\_意识到\_NETROOT 设置位，**类型**成员设置为 RDBSS **NtfsLinkTrackingInformation**。 如果成功，设置 RDBSS **IoStatus.Information** IRP 到链接的大小的成员\_跟踪\_信息结构。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Mrx.h （包括 Mrx.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**MRxIsValidDirectory**](https://msdn.microsoft.com/library/windows/hardware/ff550696)

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

[**RxFsdPostRequest**](https://msdn.microsoft.com/library/windows/hardware/ff554472)

 

 






