---
title: MRxExtendForNonCache 例程
description: MRxExtendForNonCache 例程由 RDBSS 调用，以请求当缓存管理器未缓存文件时，网络小型重定向程序会扩展文件。
ms.assetid: 80ec5142-7188-45ba-a1cb-73be99ce1ac4
keywords:
- MRxExtendForNonCache 例程可安装文件系统驱动程序
- PMRX_EXTENDFILE_CALLDOWN
topic_type:
- apiref
api_name:
- MRxExtendForNonCache
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7d441b7a68e156c07e54a4320a946d21b52fcef
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066144"
---
# <a name="mrxextendfornoncache-routine"></a>MRxExtendForNonCache 例程


*MRxExtendForNonCache*例程由[RDBSS](./the-rdbss-driver-and-library.md)调用，以请求当缓存管理器未缓存文件时，网络小型重定向程序会扩展文件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_EXTENDFILE_CALLDOWN MRxExtendForNonCache;

ULONG MRxExtendForNonCache(
  _Inout_ PRX_CONTEXT    RxContext,
  _Inout_ PLARGE_INTEGER pNewFileSize,
  _Out_   PLARGE_INTEGER pNewAllocationSize
)
{ ... }
```

<a name="parameters"></a>parameters
----------

*RxContext* \[in、out\]  
指向 RX \_ 上下文结构的指针。 此参数包含请求操作的 IRP。

*pNewFileSize* \[in、out\]  
指向大 \_ 整数值的指针，指示新文件大小的字节计数。

*pNewAllocationSize* \[弄\]  
一个指针，指向 \_ 用于在 [**MRxExtendForCache**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown) 返回时存储新分配大小的大整数。

<a name="return-value"></a>返回值
------------

*MRxExtendForNonCache* 返回成功状态 \_ 或失败时返回错误代码。

<a name="remarks"></a>备注
-------

*MRxExtendForNonCache* 处理网络请求，以扩展非缓存 i/o 的文件。

在调用 *MRxExtendForNonCache*之前，RDBSS 会修改 \_ *RXCONTEXT* 参数指向的 RX 上下文结构中的以下成员：

**LowIoContext** 设置为 LOWIO \_ OP \_ WRITE

**LowIoContext PARAMSFOR** LOWIO \_ READWRITEFLAG \_ 扩展 \_ FILESIZE 位集

缓存文件或目录信息的网络微型重定向程序可能需要在扩展文件时使其缓存信息无效。

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

## <a name="see-also"></a>请参阅


[**MRxAreFilesAliased**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown)

[**MRxCleanupFobx**](/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))

[**MRxCloseSrvOpen**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown)

[**MRxCollapseOpen**](mrxcollapseopen.md)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)

[**MRxDeallocateForFobx**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)

[**MRxExtendForCache**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)

[**MRxIsLockRealizable**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

