---
title: MRxQueryFileInfo 例程
description: TheMRxQueryFileInfo 例程由 RDBSS 调用，以请求在文件系统对象上进行网络微型重定向程序查询文件信息。
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
ms.openlocfilehash: c39e5a39edb2a734097dded47fbc7f5c7152eec2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823224"
---
# <a name="mrxqueryfileinfo-routine"></a>MRxQueryFileInfo 例程


[RDBSS](./the-rdbss-driver-and-library.md)调用 *MRxQueryFileInfo* 例程来请求一个有关文件系统对象的网络微重定向程序查询文件信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryFileInfo;

NTSTATUS MRxQueryFileInfo(
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

*MRxQueryFileInfo* 返回成功的状态 \_ 成功或适当的 NTSTATUS 值，如以下之一：

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
<p>应将此返回值视为成功，并尽可能多地在<em>RxContext</em>参数指向的 RX_CONTEXT 结构的<strong>信息. Buffer</strong>成员中返回尽可能多的数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_BUFFER_TOO_SMALL</strong></td>
<td align="left"><p>缓冲区太小，无法接收请求的数据。</p>
<p>如果返回此值，则应将<em>RxContext</em>参数指向的 RX_CONTEXT 结构的<strong>InformationToReturn</strong>成员设置为预期缓冲区的最小大小，以便调用成功。</p></td>
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
<p>如果 RX_CONTEXT 中的 <strong>FileInformationClass</strong> 成员的值无效，则会返回此值。 如果指定的 <strong>FileInformationClass</strong> 成员用于 <strong>FileStreamInformation</strong> ，而远程文件系统不支持流，也可以返回此值。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_NAME_NOT_FOUND</strong></td>
<td align="left"><p>找不到对象名称。 这是一个错误代码。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 发出对 *MRxQueryFileInfo* 的调用，以响应接收 [**IRP \_ MJ \_ 查询 \_ 信息**](irp-mj-query-information.md) 请求。

在调用 *MRxQueryFileInfo* 之前，RDBSS 会修改 \_ *RXCONTEXT* 参数指向的 RX 上下文结构中的以下成员：

**FileInformationClass** 成员设置为 **IrpSp- &gt; QueryFile。 FILEINFORMATIONCLASS**，请求的文件 \_ 信息 \_ 类值。

**信息. buffer** 成员设置为 i/o 请求数据包中的用户缓冲区。

**LengthRemaining** 成员设置为 **IrpSp &gt; 参数. QueryFile**。

**QueryDirectory. FileIndex** 成员设置为 **IrpSp-QueryDirectory. &gt; FileIndex**。

如果 **IrpSp &gt;** 设置了 SL RESTART 扫描位集，则设置 **QueryDirectory RestartScan** 成员 \_ \_ 。

如果 **QueryDirectory.ReturnSingleEntry** **IRPSP &gt; 标记** 有 SL \_ 返回 \_ 单 \_ 项位集，则设置 ReturnSingleEntry 成员。

如果 Fobx 为 **NULL** ，则设置 **&gt;** **QueryDirectory.InitialQuery** 成员，并且 **Fobx &gt; 标记** 不会将 Fobx \_ 标志 \_ 与 \_ 所有位集匹配。

成功时，网络小型重定向程序应将 RX 上下文结构的 **LengthRemaining** 成员设置 \_ 为 **info。 length** 成员减去返回的文件信息的长度。 如果对 *MRxQueryFileInfo* 的调用成功，则 RDBSS 会将 IRP 的 **IoStatus** 成员设置为 IrpSp，而不是 RX 上下文的 **QueryFile** 成员。 **&gt;** \_

RDBSS 不支持具有 SL \_ 索引 \_ 指定位的 **IrpSp &gt;** 集的请求。 网络小型重定向程序将不会接收到 *MRxQueryFileInfo* 的调用，其中 SL \_ 索引 \_ 指定的位为 **IrpSp &gt;** 集。

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

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

