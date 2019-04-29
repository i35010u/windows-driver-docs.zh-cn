---
title: MRxSetQuotaInfo routine
description: TheMRxSetQuotaInfo 例程调用 RDBSS 请求网络微型重定向，在文件系统对象设置的配额信息。
ms.assetid: 43d8669f-d122-4385-87a3-bf31bac9dfd2
keywords:
- MRxSetQuotaInfo 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxSetQuotaInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3ab64a3b59b7aff11d306011eb34e199b25f80b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352841"
---
# <a name="mrxsetquotainfo-routine"></a>MRxSetQuotaInfo routine


*MRxSetQuotaInfo*由调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)请求网络微型重定向，在文件系统对象设置的配额信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxSetQuotaInfo;

NTSTATUS MRxSetQuotaInfo(
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

*MRxSetQuotaInfo*将返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>不支持的配额。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 发出调用*MRxSetQuotaInfo*接收响应[ **IRP\_MJ\_设置\_配额**](irp-mj-set-quota.md)请求。

然后再调用*MRxSetQuotaInfo*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

*Info.Buffer* I/O 请求数据包从成员设置为用户缓冲区。 如果需要通过 RDBSS 已锁定已此缓冲区。

**Info.LengthRemaining**成员设置为**IrpSp-&gt;Parameters.SetQuota.Length**。

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

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






