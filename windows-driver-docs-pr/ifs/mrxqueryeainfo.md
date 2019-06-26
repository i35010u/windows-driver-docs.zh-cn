---
title: MRxQueryEaInfo routine
description: MRxQueryEaInfo 例程调用 RDBSS 请求网络微型重定向查询扩展文件系统对象的属性信息。
ms.assetid: 4471eb82-c176-4976-b722-5a6e067a7e69
keywords:
- MRxQueryEaInfo 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxQueryEaInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a5f029e179f6b31d3fa78ed367c68c67a735ad2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370077"
---
# <a name="mrxqueryeainfo-routine"></a>MRxQueryEaInfo routine


*MRxQueryEaInfo*由调用例程[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)请求网络微型重定向查询扩展文件系统对象的属性信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryEaInfo;

NTSTATUS MRxQueryEaInfo(
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

*MRxQueryEaInfo*将返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><p>要接收扩展的属性信息的缓冲区太小。</p>
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
<td align="left"><strong>STATUS_EA_CORRUPT_ERROR</strong></td>
<td align="left"><p>从远程服务器收到了无效的扩展的属性信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>没有资源不足，无法完成查询。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>指定的参数无效。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NONEXISTENT_EA_ENTRY</strong></td>
<td align="left"><p>在文件对象上没有任何扩展的属性和用户提供的扩展的属性索引。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>不支持扩展的属性。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_ONLY_IF_CONNECTED</strong></td>
<td align="left"><p>未连接 SRV_OPEN 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REQUEST_ABORTED</strong></td>
<td align="left"><p>网络请求已中止。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 发出调用*MRxQueryEaInfo*接收响应[ **IRP\_MJ\_查询\_EA** ](irp-mj-query-ea.md)请求。

然后再调用*MRxQueryEaInfo*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**Info.Buffer** I/O 请求数据包从成员设置为用户缓冲区。 如果需要通过 RDBSS 已锁定已此缓冲区。

**Info.LengthRemaining**成员设置为**IrpSp-&gt;Parameters.QueryEa.Length**。

**QueryEa.UserEaList**成员设置为**IrpSp-&gt;Parameters.QueryEa.EaList**。

**QueryEa.UserEaListLength**成员设置为**IrpSp-&gt;Parameters.QueryEa.EaListLength**。

**QueryEa.UserEaIndex**成员设置为**IrpSp-&gt;Parameters.QueryEa.EaIndex**。

**QueryEa.RestartScan**成员设置为非零**IrpSp-&gt;标志**具有 SL\_重启\_位上的扫描。

**QueryEa.ReturnSingleEntry**成员设置为非零**IrpSp-&gt;标志**具有 SL\_返回\_单一\_位上的条目。

**QueryEa.IndexSpecified**成员设置为非零**IrpSp-&gt;标志**具有 SL\_索引\_指定位。

如果成功， *MRxQueryEaInfo*应设置**Info.LengthRemaininging** RX 成员\_上下文结构到返回的扩展的特性信息以及更新的长度**Fobx-&gt;OffsetOfNextEaToReturn**成员。 如果在调用*MRxQueryEaInfo*已成功，RDBSS 集**IoStatus.Information**成员到 IRP **IrpSp-&gt;Parameters.QueryEa.Length**减**Info.LengthRemaining** RX 成员\_上下文。

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


[**MRxIsValidDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_chkdir_calldown)

[**MRxQueryDirectory**](mrxquerydirectory.md)

[**MRxQueryFileInfo**](mrxqueryfileinfo.md)

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






