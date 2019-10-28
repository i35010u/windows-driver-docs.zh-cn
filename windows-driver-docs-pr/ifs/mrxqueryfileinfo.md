---
title: MRxQueryFileInfo 例程
description: TheMRxQueryFileInfo 例程由 RDBSS 调用，以请求在文件系统对象上进行网络微型重定向程序查询文件信息。
ms.assetid: 201b749c-527b-4c02-a860-d2f54777dc32
keywords:
- MRxQueryFileInfo 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxQueryFileInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 982ad1abf13c3115cf3593b764d96b043eee5013
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841091"
---
# <a name="mrxqueryfileinfo-routine"></a>MRxQueryFileInfo 例程


[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用*MRxQueryFileInfo*例程来请求一个有关文件系统对象的网络微重定向程序查询文件信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryFileInfo;

NTSTATUS MRxQueryFileInfo(
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

*MRxQueryFileInfo*返回成功的状态\_成功或使用适当的 NTSTATUS 值，如以下之一：

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
<td align="left"><p>用于接收文件信息的缓冲区太小。</p>
<p>应将此返回值视为成功，并且应尽可能多的有效数据返回到由<em>RxContext</em>参数指向的 RX_CONTEXT 结构的<strong>信息. Buffer</strong>成员中。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>缓冲区太小，无法接收请求的数据。</p>
<p>如果返回此值，则<em>RxContext</em>参数指向的 RX_CONTEXT 结构的<strong>InformationToReturn</strong>成员应设置为预期缓冲区的最小大小，以便调用成功。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>资源不足，无法完成查询。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>从远程服务器接收到无效的文件信息缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>指定的参数无效。</p>
<p>如果传递 RX_CONTEXT 中的<strong>FileInformationClass</strong>成员的值无效，则可以返回此值。 如果指定的<strong>FileInformationClass</strong>成员用于<strong>FileStreamInformation</strong> ，而远程文件系统不支持流，也可以返回此值。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_NAME_NOT_FOUND</strong></td>
<td align="left"><p>找不到对象名称。 这是一个错误代码。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 发出对*MRxQueryFileInfo*的调用，以响应接收[**IRP\_\_MJ\_信息**](irp-mj-query-information.md)请求。

在调用*MRxQueryFileInfo*之前，RDBSS 会修改 RX\_由*RxContext*参数指向的上下文结构：

**FileInformationClass**成员设置为**IrpSp&gt;FileInformationClass**，请求的文件\_信息\_类值。

**信息. buffer**成员设置为 i/o 请求数据包中的用户缓冲区。

**LengthRemaining**成员设置为**IrpSp-&gt;QueryFile**。

**FileIndex**成员设置为**IrpSp&gt;QueryDirectory. FileIndex**。

如果**IrpSp&gt;标志**具有 SL\_RESTART\_扫描位集，则设置**RestartScan**成员。

如果**IrpSp&gt;标志**具有 SL\_返回\_单一\_条目位集，则设置**ReturnSingleEntry**成员。

如果**Fobx&gt;UnicodeQueryTemplate**为**NULL** ，并且**Fobx&gt;标志**没有 FOBX\_标志\_匹配\_所有位集，则设置**InitialQuery**成员。

成功时，网络小型重定向程序应将\_RX 的**LengthRemaining**成员设置为**info。 length**成员减去返回的文件信息的长度。 如果对*MRxQueryFileInfo*的调用成功，则 RDBSS 会将 IRP 的**IoStatus**成员设置为 **&gt;IrpSp** ，并将 RX\_**上下文的 QueryFile 成员减**。

RDBSS 不支持具有 SL\_索引的请求\_指定的位 **&gt;IrpSp 标记**集。 网络小型重定向程序将不会使用 SL\_索引\_指定的位 **&gt;标志**集接收对*MRxQueryFileInfo*的调用。

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

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






