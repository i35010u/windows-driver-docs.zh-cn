---
title: MRxQuerySdInfo 例程
description: TheMRxQuerySdInfo 例程由 RDBSS 调用，请求网络小型重定向程序查询有关文件系统对象的安全描述符信息。
ms.assetid: 5bab05f1-2a79-42c0-ba70-e1124f7b1528
keywords:
- MRxQuerySdInfo 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxQuerySdInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dc50b2c07c89d959ff959a9d763e6ff32730af1
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065534"
---
# <a name="mrxquerysdinfo-routine"></a>MRxQuerySdInfo 例程


*MRxQuerySdInfo*例程由[RDBSS](./the-rdbss-driver-and-library.md)调用，以请求网络小型重定向程序查询有关文件系统对象的安全描述符信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQuerySdInfo;

NTSTATUS MRxQuerySdInfo(
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

*MRxQuerySdInfo* 返回成功的状态 \_ 成功或适当的 NTSTATUS 值，如以下之一：

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
<td align="left"><p>用于接收安全描述符信息的缓冲区太小。</p>
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
<td align="left"><strong>STATUS_NETWORK_ACCESS_DENIED</strong></td>
<td align="left"><p>网络访问被拒绝。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现请求的功能，如远程页面文件上的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>远程共享不支持安全描述符信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_OBJECT_PATH_NOT_FOUND</strong></td>
<td align="left"><p>找不到对象路径。 如果已请求有关 NTFS stream 对象的信息，并且远程文件系统不支持流，则会返回此错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REPARSE</strong></td>
<td align="left"><p>需要重新分析才能处理符号链接。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 发出对 *MRxQuerySdInfo* 的调用，以响应接收 [**IRP \_ MJ \_ 查询 \_ 安全**](irp-mj-query-security.md) 请求。

在调用 *MRxQuerySdInfo*之前，RDBSS 会修改 \_ *RXCONTEXT* 参数指向的 RX 上下文结构中的以下成员：

**QuerySecurity. SecurityInformation**成员设置为**IrpSp-QuerySecurity. &gt; SecurityInformation**。

**信息. Buffer**成员设置为 i/o 请求数据包中的用户缓冲区。 如果需要，此缓冲区已被 RDBSS 锁定。

**LengthRemaining**成员设置为**IrpSp &gt; 参数. QuerySecurity**。

成功时，网络小型重定向程序应将 RX 上下文结构的 **InformationToReturn** 成员设置 \_ 为返回的安全信息的长度。 如果对 *MRxQuerySdInfo* 的调用成功，则 RDBSS 会将 IRP 的 **IoStatus** 成员设置为 RX 上下文的 **InformationToReturn** 成员 \_ 。

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

## <a name="see-also"></a>请参阅


[**MRxIsValidDirectory**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown)

[**MRxQueryDirectory**](mrxquerydirectory.md)

[**MRxQueryEaInfo**](mrxqueryeainfo.md)

[**MRxQueryFileInfo**](mrxqueryfileinfo.md)

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

