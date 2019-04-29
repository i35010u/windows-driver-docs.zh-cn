---
title: MRxQueryDirectory 例程
description: MRxQueryDirectory 例程调用 RDBSS 来请求网络微型重定向查询信息上的文件目录。
ms.assetid: 26c7c7fa-7dfa-43fb-a1db-cfc2fc40b969
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
ms.openlocfilehash: 3e4d3d93833fc553b4a2e98f2fcc3e1129ba7214
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324344"
---
# <a name="mrxquerydirectory-routine"></a>MRxQueryDirectory 例程


*MRxQueryDirectory*由调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)请求网络微型重定向查询文件目录的信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxQueryDirectory;

NTSTATUS MRxQueryDirectory(
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

*MRxQueryDirectory*将返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>没有资源不足，无法完成查询。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_NETWORK_RESPONSE</strong></td>
<td align="left"><p>从远程服务器接收到无效的文件信息缓冲区或返回文件名长度超过最大允许长度。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>中指定了无效的 FileInformationClass <strong>Info.FileInformationClass</strong> RX_CONTEXT 结构中的成员由指向<em>RxContext</em>参数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_LINK_FAILED</strong></td>
<td align="left"><p>尝试重新连接到远程服务器以完成查询失败。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NO_SUCH_FILE</strong></td>
<td align="left"><p>查询未找到任何条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_SHARING_VIOLATION</strong></td>
<td align="left"><p>发生共享冲突。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

然后再调用*MRxQueryDirectory*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**Info.FileInformationClass**成员设置为**IrpSp-&gt;Parameters.QueryDirectory.FileInformationClass**。

**Info.Buffer** I/O 请求数据包从成员设置为用户缓冲区。 如果需要通过 RDBSS 已锁定已此缓冲区。

**Info.LengthRemaining**成员设置为**IrpSp-&gt;Parameters.QueryDirectory.Length**。

**QueryDirectory.FileIndex**成员设置为**IrpSp-&gt;Parameters.QueryDirectory.FileIndex**。

**QueryDirectory.RestartScan**成员设置为非零**IrpSp-&gt;标志**具有 SL\_重启\_位上的扫描。

**QueryDirectory.ReturnSingleEntry**成员设置为非零**IrpSp-&gt;标志**具有 SL\_返回\_单一\_位上的条目。

**QueryDirectory.IndexSpecified**成员设置为非零**IrpSp-&gt;标志**具有 SL\_索引\_指定位。

**QueryDirectory.InitialQuery**成员设置为非零**UnicodeQueryTemplate.Buffer**成员相关联的 FOBX **NULL**和**标志** FOBX 成员没有 FOBX\_标志\_匹配\_所有位。

通配符查询 ("\*。\*"，例如)，将设置 RDBSS **UnicodeQueryTemplate.Buffer**传递关联 FOBX 通配符查询的成员。

如果**PostRequest** RX 成员\_上下文结构**TRUE**返回时从*MRxQueryDirectory*，然后将调用 RDBSS [ **RxFsdPostRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff554472)传递 RX\_上下文结构到辅助队列中进行处理的文件系统进程 (FSP)。

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

[**RxFsdPostRequest**](https://msdn.microsoft.com/library/windows/hardware/ff554472)

 

 






