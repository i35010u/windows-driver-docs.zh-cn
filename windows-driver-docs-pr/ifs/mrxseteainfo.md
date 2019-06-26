---
title: MRxSetEaInfo routine
description: TheMRxSetEaInfo 例程调用 RDBSS 请求网络微型重定向程序集扩展文件系统对象的属性信息。
ms.assetid: 6882ab3c-a679-491b-a35f-71cfbf77bb39
keywords:
- MRxSetEaInfo 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxSetEaInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5b68cf37fc4c1bf23a8e0dda7c7912540ff25fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385652"
---
# <a name="mrxseteainfo-routine"></a>MRxSetEaInfo routine


*MRxSetEaInfo*由调用例程[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)请求网络微型重定向程序集扩展文件系统对象的属性信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxSetEaInfo;

NTSTATUS MRxSetEaInfo(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>Parameters
----------

*RxContext* \[in、 out\]  
指向 RX\_上下文结构。 此参数包含 IPR 请求该操作。

<a name="return-value"></a>返回值
------------

*MRxSetEaInfo*将返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><strong>STATUS_EA_TOO_LARGE</strong></td>
<td align="left"><p>传递的扩展的特性信息大于支持的远程共享的大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_FILE_CLOSED</strong></td>
<td align="left"><p>SRV_OPEN 结构已关闭。</p></td>
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
<td align="left"><strong>STATUS_NETWORK_ACCESS_DENIED</strong></td>
<td align="left"><p>网络访问被拒绝。 如果网络微型重定向需要只读共享上设置扩展的属性，可以返回此错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现请求，例如在远程页面文件上设置的扩展的信息的功能。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>不支持扩展的属性。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_NAME_NOT_FOUND</strong></td>
<td align="left"><p>找不到对象名称。 如果要求网络微型重定向文件，设置扩展的属性，但该文件不存在，则可以返回此错误。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_OBJECT_PATH_NOT_FOUND</strong></td>
<td align="left"><p>找不到对象路径。 如果传入非 NTFS 流对象，并且远程文件系统不支持流，可以返回此错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_ONLY_IF_CONNECTED</strong></td>
<td align="left"><p>未连接 SRV_OPEN 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REPARSE</strong></td>
<td align="left"><p>重新分析需要处理符号链接。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 发出调用*MRxSetEaInfo*接收响应[ **IRP\_MJ\_设置\_EA** ](irp-mj-set-ea.md)请求。

然后再调用*MRxSetEaInfo*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**Info.Buffer** I/O 请求数据包从成员设置为用户缓冲区。 如果需要通过 RDBSS 已锁定已此缓冲区。

**Info.LengthRemaining**成员设置为**IrpSp-&gt;Parameters.QueryEa.Length**。

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

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






