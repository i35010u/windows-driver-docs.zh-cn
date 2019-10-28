---
title: MRxShouldTryToCollapseThisOpen 例程
description: MRxShouldTryToCollapseThisOpen 例程由 RDBSS 调用，请求网络小型重定向程序指示 RDBSS 应尝试并将打开的请求折叠到现有的文件系统对象。
ms.assetid: a68755c1-73f5-4134-b506-2a0163637a13
keywords:
- MRxShouldTryToCollapseThisOpen 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxShouldTryToCollapseThisOpen
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeed09a83fa2ef39ad224f661c7b7093e492defb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841068"
---
# <a name="mrxshouldtrytocollapsethisopen-routine"></a>MRxShouldTryToCollapseThisOpen 例程


*MRxShouldTryToCollapseThisOpen*例程由[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用，请求网络小型重定向程序指示 RDBSS 应尝试并将打开的请求折叠到现有的文件系统对象。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxShouldTryToCollapseThisOpen;

NTSTATUS MRxShouldTryToCollapseThisOpen(
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

*MRxShouldTryToCollapseThisOpen*返回成功的状态\_成功或相应的 NTSTATUS 值，如下所示：

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
<td align="left"><strong>STATUS_MORE_PROCESSING_REQUIRED</strong></td>
<td align="left"><p>网络小型重定向程序返回此值以禁用此打开请求的折叠。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

调用*MRxShouldTryToCollapseThisOpen*来确定是否应折叠打开的请求。

在调用*MRxShouldTryToCollapseThisOpen*之前，RDBSS 会修改 RX\_由*RxContext*参数指向的上下文结构中的以下成员：

**PRelevantSrvOpen**成员设置为打开的 SRV\_。

对*MRxShouldTryToCollapseThisOpen*的调用可能是对目录的更改通知请求。 因此，网络小型重定向程序可能不允许折叠打开的请求，使更改通知正常工作。

如果 RX\_上下文结构的**NtCreateParameters. CreateOptions**成员具有\_为\_备份\_意向选项或文件\_删除\_打开文件，则不允许折叠打开\_在\_关闭 "选项集。

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

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






