---
title: MRxExtendForNonCache 例程
description: MRxExtendForNonCache 例程由 RDBSS 请求网络微型重定向扩展一个文件，当缓存管理器不缓存该文件时调用。
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
ms.openlocfilehash: 883b4a9f2844232a854175c31c3b4cc3b5fa1d6c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379691"
---
# <a name="mrxextendfornoncache-routine"></a>MRxExtendForNonCache 例程


*MRxExtendForNonCache*由调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)请求网络微型重定向扩展一个文件，当缓存管理器不缓存该文件。

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

<a name="parameters"></a>Parameters
----------

*RxContext* \[in、 out\]  
指向 RX\_上下文结构。 此参数包含 IRP 请求该操作。

*pNewFileSize* \[in, out\]  
指向大\_整数值，该值指示新的文件大小的字节数。

*pNewAllocationSize* \[out\]  
指向大型\_用于存储新分配的整数大小[ **MRxExtendForCache** ](https://msdn.microsoft.com/library/windows/hardware/ff549878)返回。

<a name="return-value"></a>返回值
------------

*MRxExtendForNonCache*将返回状态\_成功或失败的错误代码成功。

<a name="remarks"></a>备注
-------

*MRxExtendForNonCache*句柄网络请求，若要为非缓存 I/O 扩展文件。

然后再调用*MRxExtendForNonCache*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**LowIoContext.Operation**设置为 LOWIO\_OP\_编写

**LowIoContext.ParamsFor.ReadWrite.Flags**具有 LOWIO\_READWRITEFLAG\_扩展\_设置位文件大小

网络微型重定向的缓存文件或目录的信息可能需要时扩展该文件使其缓存信息无效。

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

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://msdn.microsoft.com/library/windows/hardware/ff550677)

[**MRxIsLockRealizable**](https://msdn.microsoft.com/library/windows/hardware/ff550691)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






