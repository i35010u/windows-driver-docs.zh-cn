---
title: MRxQuerySdInfo routine
description: TheMRxQuerySdInfo 例程由调用 RDBSS 来请求网络微型重定向查询安全描述符信息上的文件系统对象。
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
ms.openlocfilehash: 072590cdf56942140b974362c1b3ec13928a5128
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324263"
---
# <a name="mrxquerysdinfo-routine"></a>MRxQuerySdInfo routine


*MRxQuerySdInfo*由调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)请求网络微型重定向查询对文件系统对象的安全描述符信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQuerySdInfo;

NTSTATUS MRxQuerySdInfo(
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

*MRxQuerySdInfo*将返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><p>要接收的安全描述符信息的缓冲区太小。</p>
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
<td align="left"><strong>STATUS_NETWORK_ACCESS_DENIED</strong></td>
<td align="left"><p>网络访问被拒绝。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现请求，如远程页面文件的信息的功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>在远程共享上不支持安全描述符信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_OBJECT_PATH_NOT_FOUND</strong></td>
<td align="left"><p>找不到对象路径。 如果请求 NTFS 流对象的信息和远程文件系统不支持流，可以返回此错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REPARSE</strong></td>
<td align="left"><p>重新分析需要处理符号链接。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 发出调用*MRxQuerySdInfo*接收响应[ **IRP\_MJ\_查询\_安全**](irp-mj-query-security.md)请求。

然后再调用*MRxQuerySdInfo*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**QuerySecurity.SecurityInformation**成员设置为**IrpSp-&gt;Parameters.QuerySecurity.SecurityInformation**。

**Info.Buffer** I/O 请求数据包从成员设置为用户缓冲区。 如果需要通过 RDBSS 已锁定已此缓冲区。

**Info.LengthRemaining**成员设置为**IrpSp-&gt;Parameters.QuerySecurity.Length**。

如果成功，应设置网络微型重定向**InformationToReturn** RX 成员\_上下文结构到安全信息的长度返回。 如果在调用*MRxQuerySdInfo*已成功，RDBSS 集**IoStatus.Information**到 IRP 的成员**InformationToReturn** RX 成员\_上下文。

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

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






