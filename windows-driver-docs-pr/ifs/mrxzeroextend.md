---
title: MRxZeroExtend 例程
description: MRxZeroExtend 例程由 RDBSS 调用，请求网络最小化重定向器截断文件系统对象的内容。
ms.assetid: d4a7c201-3c7d-40e9-a7da-17f40862c258
keywords:
- MRxZeroExtend 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxZeroExtend
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c700125a6b6318942346339d7b9930f221051878
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841062"
---
# <a name="mrxzeroextend-routine"></a>MRxZeroExtend 例程


*MRxZeroExtend*例程由[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用，请求网络最小化重定向器截断文件系统对象的内容。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxZeroExtend;

NTSTATUS MRxZeroExtend(
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

*MRxZeroExtend*返回成功的状态\_成功或相应的 NTSTATUS 值，如下所示：

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
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现此例程。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果文件对象未标记为要删除并且文件对象不是分页文件，则将*MRxZeroExtend*作为清理操作的一部分进行调用。 调用*MRxZeroExtend*以确保有效数据长度和文件大小之间的部分为零扩展。 在调用*MRxZeroExtend*之后，RDBSS 将 FCB 结构的结构的**ValidDataLength QuadPart**成员设置为等于 FileSize**结构的 QuadPart 成员。**

调用*MRxZeroExtend*后，将在清理操作过程中调用[**MRxCleanupFobx**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85)) 。

RDBSS 忽略*MRxZeroExtend*的返回值。

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


[**MRxAreFilesAliased**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown)

[**MRxCleanupFobx**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))

[**MRxCloseSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown)

[**MRxCollapseOpen**](mrxcollapseopen.md)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)

[**MRxDeallocateForFobx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)

[**MRxExtendForCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)

[**MRxIsLockRealizable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

 

 






