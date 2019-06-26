---
title: MRxQueryQuotaInfo routine
description: MRxQueryQuotaInfo 例程由调用 RDBSS 来请求网络微型重定向查询配额信息上的文件系统对象。
ms.assetid: 44bf976b-09bc-4270-8c2e-8e55784aaa38
keywords:
- MRxQueryQuotaInfo 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxQueryQuotaInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c638972c78b43b8b2331ccc32a0e0961299a0187
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370979"
---
# <a name="mrxqueryquotainfo-routine"></a>MRxQueryQuotaInfo routine


*MRxQueryQuotaInfo*由调用例程[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)请求网络微型重定向查询文件系统对象的配额信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryQuotaInfo;

NTSTATUS MRxQueryQuotaInfo(
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

*MRxQueryQuotaInfo*将返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><p>要接收的配额信息的缓冲区太小。</p>
<p>此返回值应被视为成功，并且作为有效得多的数据应该返回在<strong>Info.Buffer</strong> RX_CONTEXT 结构成员指向的<em>RxContext</em>参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>缓冲区是太小，无法接收请求的数据。</p>
<p>如果返回此值，则<strong>InformationToReturn</strong> RX_CONTEXT 结构成员指向的<em>RxContext</em>参数应设置为调用的预期缓冲区的最小大小会成功。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_CONNECTION_DISCONNECTED</strong></td>
<td align="left"><p>连接已断开连接。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>没有资源不足，无法完成查询。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>指定的参数无效。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>不支持的配额。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 发出调用*MRxQueryQuotaInfo*接收响应[ **IRP\_MJ\_查询\_配额**](irp-mj-query-quota.md)请求。

然后再调用*MRxQueryQuotaInfo*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**Info.Buffer** I/O 请求数据包从成员设置为用户缓冲区。 如果需要通过 RDBSS 已锁定已此缓冲区。

**Info.LengthRemaining**成员设置为**IrpSp-&gt;Parameters.QueryQuota.Length**。

**QueryQuota.SidList**成员设置为**IrpSp-&gt;Parameters.QueryQuota.SidList**。

**QueryQuota.SidListLength**成员设置为**IrpSp-&gt;Parameters.QueryQuota.SidListLength**。

**QueryQuota.StartSid**成员设置为**IrpSp-&gt;Parameters.QueryQuota.StartSid**。

**QueryQuota.Length**成员设置为**IrpSp-&gt;Parameters.QueryQuota.Length**。

**QueryQuota.RestartScan**成员设置为非零**IrpSp-&gt;标志**具有 SL\_重启\_扫描位集。

**QueryQuota.ReturnSingleEntry**成员设置为非零**IrpSp-&gt;标志**具有 SL\_返回\_单一\_条目位集。

**QueryQuota.IndexSpecified**成员设置为非零**IrpSp-&gt;标志**具有 SL\_索引\_设置指定位。

如果成功，应设置网络微型重定向**Info.LengthRemaining** RX 成员\_上下文结构到要返回的配额信息的长度。 如果在调用*MRxQueryQuotaInfo*已成功，RDBSS 集**IoStatus.Information**到 IRP 的成员**Info.LengthRemaining** RX成员\_上下文。

如果在调用*MRxQueryQuotaInfo*成功， **InformationToReturn** RX 成员\_上下文结构应设置为返回的配额的长度。 如果调用不成功， **InformationToReturn** RX 成员\_上下文应设置为零。

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

[**MRxQueryEaInfo**](mrxqueryeainfo.md)

[**MRxQueryFileInfo**](mrxqueryfileinfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






