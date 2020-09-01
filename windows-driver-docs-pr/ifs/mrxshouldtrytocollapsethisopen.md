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
ms.openlocfilehash: 6626548191ee7ef4b17445d2967a0d3028557034
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067380"
---
# <a name="mrxshouldtrytocollapsethisopen-routine"></a>MRxShouldTryToCollapseThisOpen 例程


*MRxShouldTryToCollapseThisOpen*例程由[RDBSS](./the-rdbss-driver-and-library.md)调用，请求网络小型重定向程序指示 RDBSS 应尝试并将打开的请求折叠到现有的文件系统对象。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxShouldTryToCollapseThisOpen;

NTSTATUS MRxShouldTryToCollapseThisOpen(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>parameters
----------

*RxContext* \[in、out\]  
指向 RX \_ 上下文结构的指针。 此参数包含请求操作的 IRP。

<a name="return-value"></a>返回值
------------

*MRxShouldTryToCollapseThisOpen* 返回 \_ 成功或适当的 NTSTATUS 值（如下所示）的状态成功：

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

在调用 *MRxShouldTryToCollapseThisOpen*之前，RDBSS 会修改 \_ *RXCONTEXT* 参数指向的 RX 上下文结构中的以下成员：

**PRelevantSrvOpen**成员设置为 SRV \_ OPEN。

对 *MRxShouldTryToCollapseThisOpen* 的调用可能是对目录的更改通知请求。 因此，网络小型重定向程序可能不允许折叠打开的请求，使更改通知正常工作。

如果 RX 上下文结构的 **NtCreateParameters. CreateOptions** 成员 \_ 具有 " \_ 打开备份方法的文件" \_ \_ \_ 选项或设置了 " \_ 关闭时删除文件" \_ \_ 选项，则 RDBSS 不允许折叠打开。

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
<td align="left">桌面型</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Mrx (包含 Mrx) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MRxAreFilesAliased**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown)

[**MRxCleanupFobx**](/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))

[**MRxCloseSrvOpen**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown)

[**MRxCollapseOpen**](mrxcollapseopen.md)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)

[**MRxDeallocateForFobx**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)

[**MRxExtendForCache**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)

[**MRxIsLockRealizable**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

