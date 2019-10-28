---
title: MRxTruncate 例程
description: MRxTruncate 例程由 RDBSS 调用，请求网络最小化重定向器截断文件系统对象的内容。
ms.assetid: d60ec8ef-2ccf-42ad-97d2-1aaf9d60acfb
keywords:
- MRxTruncate 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxTruncate
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8da02ba0d6fc92962ac9d6f2fbc0fc484c41fd20
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841064"
---
# <a name="mrxtruncate-routine"></a>MRxTruncate 例程


*MRxTruncate*例程由[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用，请求网络最小化重定向器截断文件系统对象的内容。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxTruncate;

NTSTATUS MRxTruncate(
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

*MRxTruncate*返回成功的状态\_成功或使用适当的 NTSTATUS 值，如以下之一：

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

如果以下两个条件均为 true，则将*MRxTruncate*作为清理操作的一部分进行调用：

-   文件对象对应于磁盘文件或目录

-   这是最后一个清理调用，文件对象标记为要截断。

如果 FCB 结构的**fcbstate**成员具有 FCB\_状态\_截断\_关闭位集上的\_，则将文件对象标记为截断。 RDBSS 会在以后的某个时间取消初始化缓存映射。

调用*MRxTruncate*后，将在清理操作过程中调用[**MRxCleanupFobx**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85)) 。

RDBSS 忽略*MRxTruncate*的返回值。

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

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






