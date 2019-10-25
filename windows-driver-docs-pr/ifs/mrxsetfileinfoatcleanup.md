---
title: MRxSetFileInfoAtCleanup 例程
description: RDBSS 调用 MRxSetFileInfoAtCleanup 例程来请求网络小型重定向程序在清理时在文件系统对象上设置文件信息。
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
ms.openlocfilehash: 13c2fe54d41d7e46d010c3f3ef6be336284f39ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841077"
---
# <a name="mrxsetfileinfoatcleanup-routine"></a>MRxSetFileInfoAtCleanup 例程


[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用*MRxSetFileInfoAtCleanup*例程来请求网络小型重定向程序在清理时在文件系统对象上设置文件信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxSetFileInfoAtCleanup;

NTSTATUS MRxSetFileInfoAtCleanup(
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

*MRxSetFileInfoAtCleanup*返回成功的状态\_成功或使用适当的 NTSTATUS 值。

<a name="remarks"></a>备注
-------

当关闭文件对象的最后一个句柄时，RDBSS 会发出对*MRxSetFileInfoAtCleanup*的调用。 这与 close 操作不同，后者是在删除对文件对象的最后一个引用时调用的。

如果文件上的时间戳或文件大小已更改，则 RDBSS 调用*MRxSetFileInfoAtCleanup* 。 对每个此类更改分别进行对*MRxSetFileInfoAtCleanup*的调用。 如果文件大小和时间戳都发生了更改，则 RDBSS 对*MRxSetFileInfoAtCleanup*进行两次调用。

在调用*MRxSetFileInfoAtCleanup*之前，如果文件上的时间戳已更改，RDBSS 将修改 RX 中的以下成员，\_上下文结构指向*RxContext*参数：

**FileInformationClass**成员设置为文件\_信息\_类值为 FileBasicInformation。

**Info. Buffer**成员设置为一个文件\_在堆栈上分配的基本\_信息结构。

**信息. Length**成员设置为 sizeof 文件\_基本\_信息结构。

在调用*MRxSetFileInfoAtCleanup*之前，RDBSS 会修改\_RX 中的以下成员，如果文件大小已更改，则由*RxContext*参数指向的上下文结构：

**FileInformationClass**成员设置为文件\_信息\_类值为 FileEndOfFileInformation。

**Info. Buffer**成员设置为在堆栈上分配的\_\_文件\_结束\_的文件。

将**Length**成员设置为<strong>sizeof （</strong>file\_END\_\_文件\_信息<strong>）</strong>。

RDBSS 忽略*MRxSetFileInfoAtCleanup*的返回值。

网络小型重定向程序可选择在此例程中执行任何操作，并返回状态\_成功。 文件大小或时间戳的任何更改将在清理操作期间进行处理。

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

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

 






