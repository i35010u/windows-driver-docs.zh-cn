---
title: MRxQueryQuotaInfo 例程
description: MRxQueryQuotaInfo 例程由 RDBSS 调用，请求网络微型重定向程序查询有关文件系统对象的配额信息。
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
ms.openlocfilehash: 12dba11aef8823327b08e6431d0b5e4e1b4f61b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823229"
---
# <a name="mrxqueryquotainfo-routine"></a>MRxQueryQuotaInfo 例程


*MRxQueryQuotaInfo* 例程由 [RDBSS](./the-rdbss-driver-and-library.md)调用，请求网络微型重定向程序查询有关文件系统对象的配额信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryQuotaInfo;

NTSTATUS MRxQueryQuotaInfo(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>参数
----------

*RxContext* \[in、out\]  
指向 RX \_ 上下文结构的指针。 此参数包含请求操作的 IRP。

<a name="return-value"></a>返回值
------------

*MRxQueryQuotaInfo* 返回成功的状态 \_ 成功或适当的 NTSTATUS 值，如以下之一：

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
<td align="left"><p>用于接收配额信息的缓冲区太小。</p>
<p>应将此返回值视为成功，并尽可能多地在<em>RxContext</em>参数指向的 RX_CONTEXT 结构的<strong>信息. Buffer</strong>成员中返回尽可能多的数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>缓冲区太小，无法接收请求的数据。</p>
<p>如果返回此值，则应将<em>RxContext</em>参数指向的 RX_CONTEXT 结构的<strong>InformationToReturn</strong>成员设置为预期缓冲区的最小大小，以便调用成功。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_CONNECTION_DISCONNECTED</strong></td>
<td align="left"><p>连接已断开连接。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>资源不足，无法完成查询。 这是一个错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>指定的参数无效。 这是一个错误代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>不支持配额。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 发出对 *MRxQueryQuotaInfo* 的调用，以响应接收 [**IRP \_ MJ \_ 查询 \_ 配额**](irp-mj-query-quota.md) 请求。

在调用 *MRxQueryQuotaInfo* 之前，RDBSS 会修改 \_ *RXCONTEXT* 参数指向的 RX 上下文结构中的以下成员：

**信息. Buffer** 成员设置为 i/o 请求数据包中的用户缓冲区。 如果需要，此缓冲区已被 RDBSS 锁定。

**LengthRemaining** 成员设置为 **IrpSp &gt; 参数. QueryQuota**。

**QueryQuota. SidList** 成员设置为 **IrpSp-QueryQuota. &gt; SidList**。

**QueryQuota. SidListLength** 成员设置为 **IrpSp-QueryQuota. &gt; SidListLength**。

**QueryQuota. StartSid** 成员设置为 **IrpSp-QueryQuota. &gt; StartSid**。

**QueryQuota** 成员设置为 **IrpSp &gt; 参数. QueryQuota**。

如果 **QueryQuota.RestartScan** IrpSp 设置了 SL **&gt;** \_ RESTART \_ 扫描位集，则 RestartScan 成员将设置为非零值。

如果 **IrpSp 的 &gt;** "SL 返回 **QueryQuota.ReturnSingleEntry** \_ \_ 单一 \_ 条目位" 位集，则 QueryQuota ReturnSingleEntry 成员将设置为非零值。

如果 **QueryQuota.IndexSpecified** **IrpSp &gt; 标志** 的 \_ \_ 指定位设置为0，则 IndexSpecified 成员将设置为非零值。

成功时，网络小型重定向程序应将 RX 上下文结构的 **LengthRemaining** 成员设置为 \_ 要返回的配额信息的长度。 如果对 *MRxQueryQuotaInfo* 的调用成功，则 RDBSS 会将 IRP 的 **IoStatus** 成员设置为 RX 上下文的 **LengthRemaining** 成员 \_ 。

如果对 *MRxQueryQuotaInfo* 的调用成功，则 RX 上下文结构的 **InformationToReturn** 成员 \_ 应设置为返回的配额信息的长度。 如果调用失败，RX 上下文的 **InformationToReturn** 成员 \_ 应设置为零。

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
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Mrx (包含 Mrx) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**MRxIsValidDirectory**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown)

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

 

