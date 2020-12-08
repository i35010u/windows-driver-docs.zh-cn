---
title: MRxQueryDirectory 例程
description: RDBSS 调用 MRxQueryDirectory 例程来请求一个有关文件目录的网络微重定向程序查询信息。
keywords:
- MRxQueryDirectory 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxQueryDirectory
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4264aaa83a48acae001e88b5822113f407d6c81
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833523"
---
# <a name="mrxquerydirectory-routine"></a>MRxQueryDirectory 例程


[RDBSS](./the-rdbss-driver-and-library.md)调用 *MRxQueryDirectory* 例程来请求一个有关文件目录的网络微重定向程序查询信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryDirectory;

NTSTATUS MRxQueryDirectory(
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

*MRxQueryDirectory* 返回成功的状态 \_ 成功或适当的 NTSTATUS 值，如以下之一：

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
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>资源不足，无法完成查询。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>从远程服务器接收到无效的文件信息缓冲区，或返回的文件名长度超出了允许的最大长度。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p><em>RxContext</em>参数指向的 RX_CONTEXT 结构中的<strong>FileInformationClass</strong>成员中指定的 FileInformationClass 无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_LINK_FAILED</strong></td>
<td align="left"><p>尝试重新连接到远程服务器以完成查询失败。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NO_SUCH_FILE</strong></td>
<td align="left"><p>查询找不到任何条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_SHARING_VIOLATION</strong></td>
<td align="left"><p>发生共享冲突。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在调用 *MRxQueryDirectory* 之前，RDBSS 会修改 \_ *RXCONTEXT* 参数指向的 RX 上下文结构中的以下成员：

**FileInformationClass** 成员设置为 **IrpSp- &gt; QueryDirectory. FileInformationClass**。

**信息. Buffer** 成员设置为 i/o 请求数据包中的用户缓冲区。 如果需要，此缓冲区已被 RDBSS 锁定。

**LengthRemaining** 成员设置为 **IrpSp &gt; 参数. QueryDirectory**。

**QueryDirectory. FileIndex** 成员设置为 **IrpSp-QueryDirectory. &gt; FileIndex**。

如果 **QueryDirectory.RestartScan** IrpSp 在上具有 SL **&gt;** \_ RESTART \_ 扫描位，则 RestartScan 成员将设置为非零值。

如果 **QueryDirectory.ReturnSingleEntry** **IrpSp &gt;** \_ \_ \_ 在上返回单比 bit，则 ReturnSingleEntry 成员将设置为非零值。

如果 **&gt; IrpSp** 在上指定了 SL 索引，则 **QueryDirectory IndexSpecified** 成员将设置为非零值 \_ \_ 。

如果关联的 FOBX 的 **UnicodeQueryTemplate** 成员为 NULL，并且 FOBX 的 **Flags** 成员不具有 tialQuery **NULL** 中的 **QueryDirectory.InitialQuery** \_ \_ 所有位的 FOBX 标志，则将QueryDirectory.Ini此成员设置为非零值 \_ 。

对于通配符查询 ( " \* . \* "，如) ，RDBSS 会将关联的 FOBX 的 **UnicodeQueryTemplate** 成员设置为通过的通配符查询。

如果 RX 上下文结构的 **PostRequest** 成员 \_ 在从 *MRxQueryDirectory* 返回时为 **TRUE** ，则 RDBSS 将调用 [**RxFsdPostRequest**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)将 RX \_ 上下文结构传递到辅助队列，以供文件系统进程 (FSP) 进行处理。

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

[**MRxQueryEaInfo**](mrxqueryeainfo.md)

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

[**RxFsdPostRequest**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)

 

