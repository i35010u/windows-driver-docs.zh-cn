---
title: '\_RxCheckMemoryBlock 例程'
description: '\_RxCheckMemoryBlock 检查内存块中是否有特殊的 RX \_ 池 \_ 标头签名。'
keywords:
- _RxCheckMemoryBlock 日常可安装文件系统驱动程序
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
ms.openlocfilehash: f45de74131f2bae0c4f913d77b14e635f1a011c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789941"
---
# <a name="_rxcheckmemoryblock-routine"></a>\_RxCheckMemoryBlock 例程


**\_ RxCheckMemoryBlock** 检查特定 RX \_ 的内存块池 \_ 标头签名。 请注意，网络小型重定向器驱动程序需要将此特殊的签名块添加到分配的内存，以便使用该例程。 不应使用此例程，因为尚未实现此特殊标头块。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
BOOLEAN _RxCheckMemoryBlock(
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
指向发生内存分配的源文件名的指针。

*LineNumber*   
源文件中发生内存分配的行号。

<a name="return-value"></a>返回值
------------

如果内存块通过检查，则 **RxCheckMemoryBlock** 返回 **TRUE** ; 否则返回 **FALSE** 。

<a name="remarks"></a>备注
-------

建议调用 **RxCheckMemoryBlock** 宏，而不是直接使用此例程。 在零售版上，此宏定义为 nothing。 在选中的生成上，此宏定义为调用 **\_ RxCheckMemoryBlock**。

不应使用此例程，因为特殊内存标头块 (RX \_ 池 \_ 标头) 此例程检查在调用 **\_ RxAllocatePoolWithTag** 例程时未添加。 网络小型重定向程序驱动程序需要将此特殊的签名块添加到分配的内存，以便使用此例程。

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

[**\_RxFreePool**](-rxfreepool.md)

 

 






