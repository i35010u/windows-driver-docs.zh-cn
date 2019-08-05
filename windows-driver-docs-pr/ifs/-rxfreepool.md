---
title: '\_RxFreePool 函数'
description: '\_RxFreePool 释放以前分配使用的内存\_RxAllocatePoolWithTag。'
ms.assetid: 383deda9-6151-420b-afa9-445cd05e998b
keywords:
- _RxFreePool 函数可安装文件系统驱动程序
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
ms.openlocfilehash: 4b424acace9d2e59e0c910301e762aace1ed73a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323307"
---
# <a name="_rxfreepool-function"></a>\_RxFreePool 函数


**\_RxFreePool**释放以前分配使用的内存 **\_RxAllocatePoolWithTag**。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID _RxFreePool(
   PVOID Buffer,
   PSZ   FileName,
   ULONG LineNumber
);
```

<a name="parameters"></a>Parameters
----------

*缓冲区*   
指向要释放的池内存缓冲区的指针。

*FileName*   
指向源文件名发生内存分配的指针。 当前未使用此参数。

*LineNumber*   
发生内存分配的源文件中的行号。 当前未使用此参数。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

建议**RxFreePool**宏调用而不是直接使用此例程。 在零售版本中，定义此宏调用**ExFreePool**。

使用分配的内存[  **\_RxAllocatePoolWithTag** ](-rxallocatepoolwithtag.md)应释放通过调用 **\_RxFreePool**。

**\_RxFreePool**例程调用**ExFreePool**。

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
<td align="left">Ntrxdef.h （包括 Ntrxdef.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[ **\_RxAllocatePoolWithTag**](-rxallocatepoolwithtag.md)

[ **\_RxCheckMemoryBlock**](-rxcheckmemoryblock.md)

 

 






