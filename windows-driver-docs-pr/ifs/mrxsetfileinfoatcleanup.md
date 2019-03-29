---
title: MRxSetFileInfoAtCleanup routine
description: MRxSetFileInfoAtCleanup 例程调用 RDBSS 请求网络微型重定向，在清理的文件系统对象上设置文件的信息。
ms.assetid: 099244ee-cc66-4500-9fee-a10238aaa66c
keywords:
- MRxSetFileInfoAtCleanup 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxSetFileInfoAtCleanup
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4fdd8d5637ad3796f6f27357ee934ceec746694
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563187"
---
# <a name="mrxsetfileinfoatcleanup-routine"></a>MRxSetFileInfoAtCleanup routine


*MRxSetFileInfoAtCleanup*由调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)请求网络微型重定向，在清理的文件系统对象上设置文件的信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxSetFileInfoAtCleanup;

NTSTATUS MRxSetFileInfoAtCleanup(
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

*MRxSetFileInfoAtCleanup*将返回状态\_成功或适当的 NTSTATUS 值成功。

<a name="remarks"></a>备注
-------

RDBSS 发出调用*MRxSetFileInfoAtCleanup*期间文件对象的最后一个句柄已关闭时清除。 这是不同于关闭操作，删除对文件对象的最后一个引用时调用。

*MRxSetFileInfoAtCleanup* RDBSS 如果上一个文件或文件的大小的时间戳已更改调用。 对调用*MRxSetFileInfoAtCleanup*通过 RDBSS 进行单独为每个这些更改。 如果文件大小和时间戳已更改，则 RDBSS 调用两*MRxSetFileInfoAtCleanup*。

然后再调用*MRxSetFileInfoAtCleanup*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数如果有一个文件上的时间戳更改：

**Info.FileInformationClass**成员设置为一个文件\_信息\_FileBasicInformation 类值。

**Info.Buffer**成员设置为一个文件\_BASIC\_在堆栈上分配的信息结构。

**Info.Length**成员设置为 sizeof 文件\_BASIC\_信息结构。

然后再调用*MRxSetFileInfoAtCleanup*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*如果文件的大小已更改的参数：

**Info.FileInformationClass**成员设置为一个文件\_信息\_FileEndOfFileInformation 类值。

**Info.Buffer**成员设置为一个文件\_最终\_OF\_文件\_在堆栈上分配的信息结构。

**Info.Length**成员设置为<strong>sizeof (</strong>文件\_最终\_OF\_文件\_信息<strong>)</strong>。

RDBSS 忽略的返回值*MRxSetFileInfoAtCleanup*。

网络微型重定向可以选择执行此例程中的任何内容，并返回状态\_成功。 对文件大小或时间戳的任何更改将在清理操作期间处理。

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

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






