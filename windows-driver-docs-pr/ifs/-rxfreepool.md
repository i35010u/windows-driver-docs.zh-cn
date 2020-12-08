---
title: '\_RxFreePool 函数'
description: '\_RxFreePool 释放以前使用 RxAllocatePoolWithTag 分配的内存 \_ 。'
keywords:
- _RxFreePool 功能可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- _RxFreePool
api_location:
- ntrxdef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ebcebc62861c94bf69ab3e652496c430d7c337d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840991"
---
# <a name="_rxfreepool-function"></a>\_RxFreePool 函数


**\_ RxFreePool** 释放以前使用 **\_ RxAllocatePoolWithTag** 分配的内存。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID _RxFreePool(
   PVOID Buffer,
   PSZ   FileName,
   ULONG LineNumber
);
```

<a name="parameters"></a>参数
----------

*宽限*   
指向要释放的池内存缓冲区的指针。

*名字*   
指向发生内存分配的源文件名的指针。 当前未使用此参数。

*LineNumber*   
源文件中发生内存分配的行号。 当前未使用此参数。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

建议调用 **RxFreePool** 宏，而不是直接使用此例程。 在零售版上，此宏定义为调用 **ExFreePool**。

使用 [**\_ RxAllocatePoolWithTag**](-rxallocatepoolwithtag.md)分配的内存应通过调用 **\_ RxFreePool** 来释放。

**\_ RxFreePool** 例程调用 **ExFreePool**。

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
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntrxdef (包含 Ntrxdef) </td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**\_RxAllocatePoolWithTag**](-rxallocatepoolwithtag.md)

[**\_RxCheckMemoryBlock**](-rxcheckmemoryblock.md)

 

 






