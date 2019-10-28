---
title: MRxQueryEaInfo 例程
description: MRxQueryEaInfo 例程由 RDBSS 调用，请求网络小型重定向器查询文件系统对象上的扩展属性信息。
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
ms.openlocfilehash: 75056b9a71e5fa8aba216b0df9297bf05154ba39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841089"
---
# <a name="mrxqueryeainfo-routine"></a>MRxQueryEaInfo 例程


*MRxQueryEaInfo*例程由[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用，请求网络小型重定向器查询文件系统对象上的扩展属性信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryEaInfo;

NTSTATUS MRxQueryEaInfo(
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

*MRxQueryEaInfo*返回成功的状态\_成功或使用适当的 NTSTATUS 值，如以下之一：

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
<td align="left"><p>用于接收扩展属性信息的缓冲区太小。</p>
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
<td align="left"><strong>STATUS_EA_CORRUPT_ERROR</strong></td>
<td align="left"><p>从远程服务器接收到的扩展属性信息无效。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>资源不足，无法完成查询。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>指定的参数无效。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NONEXISTENT_EA_ENTRY</strong></td>
<td align="left"><p>文件对象没有扩展属性，用户提供了扩展属性索引。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>不支持扩展属性。</p></td>
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

RDBSS 发出对*MRxQueryEaInfo*的调用，以响应接收[**IRP\_\_MJ\_EA**](irp-mj-query-ea.md)请求。

在调用*MRxQueryEaInfo*之前，RDBSS 会修改 RX\_由*RxContext*参数指向的上下文结构：

**信息. buffer**成员设置为 i/o 请求数据包中的用户缓冲区。 如果需要，此缓冲区已被 RDBSS 锁定。

**LengthRemaining**成员设置为**IrpSp-&gt;QueryEa**。

**UserEaList**成员设置为**IrpSp&gt;QueryEa. EaList**。

**UserEaListLength**成员设置为**IrpSp&gt;QueryEa. EaListLength**。

**UserEaIndex**成员设置为**IrpSp&gt;QueryEa. EaIndex**。

如果**IrpSp&gt;标志**具有 SL\_RESTART\_扫描位，则将**QueryEa**成员设置为非零值。

如果**IrpSp&gt;标志**具有 SL\_返回上\_单一\_项位，则将**QueryEa**成员设置为非零值。

如果**IrpSp&gt;标志**的\_索引\_指定的位，则将**QueryEa**成员设置为非零值。

成功后， *MRxQueryEaInfo*应将 RX\_上下文结构的**LengthRemaininging**成员设置为返回的扩展属性信息的长度，同时更新**Fobx&gt;OffsetOfNextEaToReturn**职员. 如果对*MRxQueryEaInfo*的调用成功，则 RDBSS 会将 IRP 的**IoStatus**成员设置为 **&gt;IrpSp** ，并将 RX\_**上下文的 QueryEa 成员减**。

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

 

 






