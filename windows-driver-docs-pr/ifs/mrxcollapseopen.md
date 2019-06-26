---
title: MRxCollapseOpen 例程
description: 由 RDBSS 请求网络微型重定向折叠到现有 SRV 上一个打开的文件系统请求调用 MRxCollapseOpen 例程\_打开结构。
ms.assetid: 1c06b2f4-b44a-4d8a-9205-987be1e497ad
keywords:
- MRxCollapseOpen 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxCollapseOpen
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 777053136ec76efa89fc059a7f322c8060b296ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383879"
---
# <a name="mrxcollapseopen-routine"></a>MRxCollapseOpen 例程


*MRxCollapseOpen*由调用例程[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)请求网络微型重定向折叠到现有 SRV 上一个打开的文件系统请求\_打开结构。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxCollapseOpen;

NTSTATUS MRxCollapseOpen(
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

*MRxCollapseOpen*将返回状态\_成功的成功或相应 NTSTATUS 值，如下所示：

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
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>没有足够的资源来完成该操作。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

*MRxCollapseOpen* RDBSS 折叠 SRV 调用\_本地打开结构。 查阅网络微型重定向以确定这样就无需两次调用网络微型重定向是否可以折叠。 如果网络微型重定向决定折叠 SRV\_打开结构，然后，它将执行此操作，并传递回可再用状态。 返回值的状态\_的成功就是终止的返回值。 不同的返回值，例如，状态\_更多\_处理\_必需，被视为非终止的返回值。

然后再调用*MRxCollapseOpen*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**pRelevantSrvOpen**设置为 SRV\_打开结构以折叠。

**Create.pSrvCall**设置为 SRV\_SRV 与关联的调用结构\_打开。

如果网络微型重定向决定折叠 SRV\_打开结构，则**SrvOpen** RX 成员\_上下文结构必须设置为折叠 SRV\_打开结构。

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


[**MRxAreFilesAliased**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_chkfcb_calldown)

[**MRxCleanupFobx**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))

[**MRxCloseSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fcb)

[**MRxDeallocateForFobx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_deallocate_for_fobx)

[**MRxExtendForCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_extendfile_calldown)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_forceclosed_calldown)

[**MRxIsLockRealizable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_is_lock_realizable)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






