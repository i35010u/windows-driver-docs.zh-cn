---
title: '\_RxCheckMemoryBlock 例程'
description: '\_RxCheckMemoryBlock 检查的内存块的特殊 RX\_池\_标头标头签名。'
ms.assetid: 972cef55-e541-450c-8128-1d026042c4ca
keywords:
- _RxCheckMemoryBlock 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- _RxCheckMemoryBlock
api_location:
- ntrxdef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03bbc59aa34dfce4503f4b7fe17e04a2ac0c29bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542713"
---
# <a name="rxcheckmemoryblock-routine"></a>\_RxCheckMemoryBlock 例程


**\_RxCheckMemoryBlock**检查的内存块的特殊 RX\_池\_标头标头签名。 请注意，网络微型重定向程序驱动程序将需要此特殊的签名块添加到内存分配才能使用该例程。 由于尚未实现此特殊的标头块，则不应使用此例程。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
BOOLEAN _RxCheckMemoryBlock(
   PVOID Buffer,
   PSZ   FileName,
   ULONG LineNumber
);
```

<a name="parameters"></a>参数
----------

*缓冲区*   
指向要释放的池内存缓冲区的指针。

*FileName*   
指向源文件名发生内存分配的指针。

*LineNumber*   
发生内存分配的源文件中的行号。

<a name="return-value"></a>返回值
------------

**RxCheckMemoryBlock**返回**TRUE**是否内存块已通过检查，或者**FALSE**失败。

<a name="remarks"></a>备注
-------

建议**RxCheckMemoryBlock**宏调用而不是直接使用此例程。 在零售版本中，为 nothing 定义此宏。 在 checked 版本中，定义此宏调用 **\_RxCheckMemoryBlock**。

此例程不应使用特殊的内存标头块自 (RX\_池\_标头) 调用时不添加此例程会检查 **\_RxAllocatePoolWithTag**例程。 网络微型重定向程序驱动程序将需要此特殊的签名块添加到要使用此例程分配的内存。

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
<td align="left"><p>标头</p></td>
<td align="left">Ntrxdef.h （包括 Ntrxdef.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**\_RxAllocatePoolWithTag**](-rxallocatepoolwithtag.md)

[**\_RxFreePool**](-rxfreepool.md)

 

 






