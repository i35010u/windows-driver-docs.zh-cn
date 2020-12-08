---
title: MRxSetFileInfoAtCleanup 例程
description: RDBSS 调用 MRxSetFileInfoAtCleanup 例程来请求网络小型重定向程序在清理时在文件系统对象上设置文件信息。
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
ms.openlocfilehash: a4e84817a8f8a129dbca79473c297f7902d3b082
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817353"
---
# <a name="mrxsetfileinfoatcleanup-routine"></a>MRxSetFileInfoAtCleanup 例程


[RDBSS](./the-rdbss-driver-and-library.md)调用 *MRxSetFileInfoAtCleanup* 例程来请求网络小型重定向程序在清理时在文件系统对象上设置文件信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxSetFileInfoAtCleanup;

NTSTATUS MRxSetFileInfoAtCleanup(
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

*MRxSetFileInfoAtCleanup* 返回 \_ 成功或适当的 NTSTATUS 值的状态成功。

<a name="remarks"></a>备注
-------

当关闭文件对象的最后一个句柄时，RDBSS 会发出对 *MRxSetFileInfoAtCleanup* 的调用。 这与 close 操作不同，后者是在删除对文件对象的最后一个引用时调用的。

如果文件上的时间戳或文件大小已更改，则 RDBSS 调用 *MRxSetFileInfoAtCleanup* 。 对每个此类更改分别进行对 *MRxSetFileInfoAtCleanup* 的调用。 如果文件大小和时间戳都发生了更改，则 RDBSS 对 *MRxSetFileInfoAtCleanup* 进行两次调用。

在调用 *MRxSetFileInfoAtCleanup* 之前， \_ 如果文件上的时间戳已更改，RDBSS 将修改 *RXCONTEXT* 参数指向的 RX 上下文结构中的以下成员：

**FileInformationClass** 成员设置为 FILE \_ INFORMATION \_ CLASS 值 of FileBasicInformation。

**Info. Buffer** 成员设置为 \_ \_ 在堆栈上分配的文件基本信息结构。

**信息. Length** 成员设置为 SIZEOF a FILE \_ BASIC \_ 信息结构。

在调用 *MRxSetFileInfoAtCleanup* 之前， \_ 如果文件大小已更改，RDBSS 将修改 *RXCONTEXT* 参数指向的 RX 上下文结构中的以下成员：

**FileInformationClass** 成员设置为 FILE \_ INFORMATION \_ CLASS 值 of FileEndOfFileInformation。

**Info. Buffer** 成员设置为 \_ \_ \_ \_ 堆栈上分配的文件信息结构的文件结尾。

**信息. Length** 成员设置为 <strong>sizeof (</strong>文件 \_ \_ \_ \_ 信息 <strong>)</strong>的文件结尾。

RDBSS 忽略 *MRxSetFileInfoAtCleanup* 的返回值。

网络小型重定向程序可在此例程中选择不执行任何操作，并返回状态 " \_ 成功"。 文件大小或时间戳的任何更改将在清理操作期间进行处理。

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

[**MRxQueryFileInfo**](mrxqueryfileinfo.md)

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfo**](mrxsetfileinfo.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

