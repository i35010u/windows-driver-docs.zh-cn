---
title: MRxCollapseOpen 例程
description: MRxCollapseOpen 例程由 RDBSS 调用，请求网络微重定向程序将打开的文件系统请求折叠到现有的 SRV \_ 开放式结构。
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
ms.openlocfilehash: 97ea2314366be8e1732d933ab518374c5659ca8b
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063046"
---
# <a name="mrxcollapseopen-routine"></a>MRxCollapseOpen 例程


*MRxCollapseOpen*例程由[RDBSS](./the-rdbss-driver-and-library.md)调用，请求网络微重定向程序将打开的文件系统请求折叠到现有的 SRV \_ 开放式结构。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxCollapseOpen;

NTSTATUS MRxCollapseOpen(
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

*MRxCollapseOpen* 返回 \_ 成功或适当的 NTSTATUS 值（如下所示）的状态成功：

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
<td align="left"><p>资源不足，无法完成此操作。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

*MRxCollapseOpen* 由 RDBSS 调用，以在本地折叠 SRV \_ 开放式结构。 建议使用网络小型重定向程序来确定是否可以进行折叠，因此没有理由调用网络微重定向程序两次。 如果网络小型重定向器决定要折叠 SRV \_ 开放式结构，则它将执行此操作并返回可再用状态。 状态成功的返回值 \_ 是终止返回值。 例如，如果需要更多的状态处理，则会将其他返回值 \_ \_ \_ 视为非终止返回值。

在调用 *MRxCollapseOpen*之前，RDBSS 会修改 \_ *RXCONTEXT* 参数指向的 RX 上下文结构中的以下成员：

**pRelevantSrvOpen** 设置为 \_ 要折叠的 SRV 开放式结构。

**PSrvCall** 设置为 \_ 与 srv OPEN 关联的 srv 调用结构 \_ 。

如果网络小型重定向器决定要折叠 SRV \_ 开放式结构，则 RX 上下文结构的 **SrvOpen** 成员 \_ 必须设置为折叠的 srv \_ 开放结构。

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

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)

[**MRxDeallocateForFobx**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)

[**MRxExtendForCache**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)

[**MRxIsLockRealizable**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

