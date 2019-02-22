---
title: MRxQueryFileInfo routine
description: TheMRxQueryFileInfo 例程由调用 RDBSS 来请求网络微型重定向查询文件信息上的文件系统对象。
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
ms.openlocfilehash: e7d7f73472f66c4a8a389a9ebb94a28c02124438
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522373"
---
# <a name="mrxqueryfileinfo-routine"></a>MRxQueryFileInfo routine


*MRxQueryFileInfo*由调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)请求网络微型重定向查询文件系统对象的文件信息。

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

*RxContext* \[in、 out\]  
指向 RX\_上下文结构。 此参数包含 IRP 请求该操作。

<a name="return-value"></a>返回值
------------

*MRxQueryFileInfo*将返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><p>要接收的文件信息的缓冲区太小。</p>
<p>此返回值应被视为成功，并且作为有效得多的数据应该返回在<strong>Info.Buffer</strong> RX_CONTEXT 结构成员指向的<em>RxContext</em>参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>缓冲区是太小，无法接收请求的数据。</p>
<p>如果返回此值，则<strong>InformationToReturn</strong> RX_CONTEXT 结构成员指向的<em>RxContext</em>参数应设置为调用的预期缓冲区的最小大小会成功。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>没有资源不足，无法完成查询。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>从远程服务器收到无效的文件信息缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>指定的参数无效。</p>
<p>如果的值无效，可能会返回此值<strong>FileInformationClass</strong>传递 RX_CONTEXT 中的成员。 如果，也会返回此值<strong>FileInformationClass</strong>指定的成员是有关<strong>FileStreamInformation</strong>和远程文件系统不支持流。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_NAME_NOT_FOUND</strong></td>
<td align="left"><p>找不到对象名称。 这是一个错误代码。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 发出调用*MRxQueryFileInfo*接收响应[ **IRP\_MJ\_查询\_信息**](irp-mj-query-information.md)请求。

然后再调用*MRxQueryFileInfo*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**Info.FileInformationClass**成员设置为**IrpSp-&gt;Parameters.QueryFile.FileInformationClass**，则请求文件\_信息\_类值。

**Info.Buffer** I/O 请求数据包从成员设置为用户缓冲区。

**Info.LengthRemaining**成员设置为**IrpSp-&gt;Parameters.QueryFile.Length**。

**QueryDirectory.FileIndex**成员设置为**IrpSp-&gt;Parameters.QueryDirectory.FileIndex**。

**QueryDirectory.RestartScan**成员设置如果**IrpSp-&gt;标志**具有 SL\_重启\_扫描位集。

**QueryDirectory.ReturnSingleEntry**成员设置如果**IrpSp-&gt;标志**具有 SL\_返回\_单一\_条目位集。

**QueryDirectory.InitialQuery**成员设置如果**Fobx-&gt;UnicodeQueryTemplate.Buffer**是**NULL**和**Fobx&gt;标志**没有 FOBX\_标志\_匹配\_所有位集。

如果成功，应设置网络微型重定向**Info.LengthRemaining** RX 成员\_上下文结构到**Info.Length**减去的时间长度文件信息的成员返回。 如果在调用*MRxQueryFileInfo*已成功，RDBSS 集**IoStatus.Information**成员到 IRP **IrpSp-&gt;Parameters.QueryFile.Length**减去**Info.LengthRemaining** RX 成员\_上下文。

RDBSS 不支持请求的 SL\_索引\_的指定位**IrpSp-&gt;标志**设置。 网络微型重定向将不会收到对调用*MRxQueryFileInfo*与 SL\_索引\_的指定位**IrpSp-&gt;标志**设置。

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
<td align="left"><p>标头</p></td>
<td align="left">Mrx.h （包括 Mrx.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MRxIsValidDirectory**](https://msdn.microsoft.com/library/windows/hardware/ff550696)

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

 

 






