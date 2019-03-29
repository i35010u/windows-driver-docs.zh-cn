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
ms.openlocfilehash: b430112cd814ab7801a285a0c2195dd7e9c8bc85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566620"
---
# <a name="mrxcollapseopen-routine"></a>MRxCollapseOpen 例程


*MRxCollapseOpen*由调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)请求网络微型重定向折叠到现有 SRV 上一个打开的文件系统请求\_打开结构。

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


[**MRxAreFilesAliased**](https://msdn.microsoft.com/library/windows/hardware/ff549838)

[**MRxCleanupFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549841)

[**MRxCloseSrvOpen**](https://msdn.microsoft.com/library/windows/hardware/ff549845)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://msdn.microsoft.com/library/windows/hardware/ff549871)

[**MRxDeallocateForFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549872)

[**MRxExtendForCache**](https://msdn.microsoft.com/library/windows/hardware/ff549878)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://msdn.microsoft.com/library/windows/hardware/ff550677)

[**MRxIsLockRealizable**](https://msdn.microsoft.com/library/windows/hardware/ff550691)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






