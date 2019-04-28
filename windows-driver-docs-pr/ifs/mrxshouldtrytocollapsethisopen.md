---
title: MRxShouldTryToCollapseThisOpen 例程
description: 由 RDBSS 请求网络微型重定向指示是否 RDBSS 应尝试并折叠了打开请求到现有的文件系统对象上调用 MRxShouldTryToCollapseThisOpen 例程。
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
ms.openlocfilehash: b61fe389d1a54bbcbea8161ed2afb50af27d1647
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352893"
---
# <a name="mrxshouldtrytocollapsethisopen-routine"></a>MRxShouldTryToCollapseThisOpen 例程


*MRxShouldTryToCollapseThisOpen*由调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)请求网络微型重定向指示是否 RDBSS 应尝试并折叠了打开请求到现有的文件系统对象.

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxShouldTryToCollapseThisOpen;

NTSTATUS MRxShouldTryToCollapseThisOpen(
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

*MRxShouldTryToCollapseThisOpen*将返回状态\_成功的成功或相应 NTSTATUS 值，如下所示：

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
<td align="left"><p>网络微型重定向返回此值以禁用此打开请求的折叠。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

*MRxShouldTryToCollapseThisOpen*调用以确定是否打开请求应不会自动折叠。

然后再调用*MRxShouldTryToCollapseThisOpen*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**PRelevantSrvOpen**成员设置为 SRV\_打开。

在调用*MRxShouldTryToCollapseThisOpen*可能会更改通知目录的请求。 因此，网络微型重定向可能不允许折叠开放请求，因此，正确变更通知的工作原理。

RDBSS 不允许折叠随即打开，如果**Create.NtCreateParameters.CreateOptions** RX 成员\_上下文结构的文件\_打开\_为\_备份\_意向选项或文件\_删除\_ON\_关闭选项集。

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


[**MRxAreFilesAliased**](https://msdn.microsoft.com/library/windows/hardware/ff549838)

[**MRxCleanupFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549841)

[**MRxCloseSrvOpen**](https://msdn.microsoft.com/library/windows/hardware/ff549845)

[**MRxCollapseOpen**](mrxcollapseopen.md)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://msdn.microsoft.com/library/windows/hardware/ff549871)

[**MRxDeallocateForFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549872)

[**MRxExtendForCache**](https://msdn.microsoft.com/library/windows/hardware/ff549878)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://msdn.microsoft.com/library/windows/hardware/ff550677)

[**MRxIsLockRealizable**](https://msdn.microsoft.com/library/windows/hardware/ff550691)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






