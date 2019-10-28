---
title: MRxSetVolumeInfo 例程
description: TheMRxSetVolumeInfo 例程由 RDBSS 调用，请求网络小型重定向器设置卷信息。
ms.assetid: 88a1809f-545a-4822-8fc3-27adf1c94835
keywords:
- MRxSetVolumeInfo 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxSetVolumeInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fa544c2a60c3906b3a4737df4761c43bff92305
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841071"
---
# <a name="mrxsetvolumeinfo-routine"></a>MRxSetVolumeInfo 例程


[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用*MRxSetVolumeInfo*例程来请求网络小型重定向程序设置卷信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxSetVolumeInfo;

NTSTATUS MRxSetVolumeInfo(
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

*MRxSetVolumeInfo*返回成功的状态\_成功或使用适当的 NTSTATUS 值，如以下之一：

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
<td align="left"><strong>STATUS_NETWORK_NAME_DELETED</strong></td>
<td align="left"><p>网络名称已被删除。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现所请求的功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>远程共享上不支持该请求。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 发出对*MRxSetVolumeInfo*的调用，以响应接收[**IRP\_MJ\_设置\_卷\_信息**](irp-mj-set-volume-information.md)请求。

在调用*MRxSetVolumeInfo*之前，RDBSS 会修改 RX\_由*RxContext*参数指向的上下文结构：

**FsInformationClass**成员设置为**IrpSp-&gt;SetVolume. FsInformationClass**。

**Info. Buffer**成员设置为**Irp-&gt;AssociatedIrp. SystemBuffer**。

**LengthRemaining**成员设置为**IrpSp-&gt;SetVolume**。

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

[**MRxQueryFileInfo**](mrxqueryfileinfo.md)

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

 

 






