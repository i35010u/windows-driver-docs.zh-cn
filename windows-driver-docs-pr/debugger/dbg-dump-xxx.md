---
title: DBG\_DUMP\_XXX
description: DBG\_DUMP\_XXX
ms.assetid: d34ecf95-3aea-4850-a2de-76f239e8b8a0
ms.date: 12/07/2017
keywords:
- DBG_DUMP_XXX Windows 调试
topic_type:
- apiref
api_name:
- DBG_DUMP_XXX
api_location:
- wdbgexts.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 0f4f0809aa12ca9bcca330b1d529f52a6c79300d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374933"
---
# <a name="dbgdumpxxx"></a>DBG\_DUMP\_XXX


## <span id="ddk_dbg_dump_xxx_dbx"></span><span id="DDK_DBG_DUMP_XXX_DBX"></span>


DBG\_转储\_*XXX*位标志由**选项**符号成员\_转储\_PARAM 结构，以控制行为[**IG\_转储\_符号\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff550906)[**Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084)操作。

以下标志可以出现。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DBG_DUMP_NO_INDENT</p></td>
<td align="left"><p>成员不缩进输出中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_NO_OFFSET</p></td>
<td align="left"><p>偏移量不打印。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_VERBOSE</p></td>
<td align="left"><p>详细输出。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_CALL_FOR_EACH</p></td>
<td align="left"><p>为每个成员调用回调函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_LIST</p></td>
<td align="left"><p>符号是将项记入链接的列表和 IG_DUMP_SYMBOL_INFO <strong>Ioctl</strong>操作将循环访问此列表。 通过指定指向列表中的下一项成员的说明<strong>linkList</strong> SYM_DUMP_PARAM 结构中的成员。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_NO_PRINT</p></td>
<td align="left"><p>（仅调用回调函数和执行数据副本），会输出任何内容。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_GET_SIZE_ONLY</p></td>
<td align="left"><p><strong>Ioctl</strong>操作将返回仅的符号的大小; 它将不打印成员信息或调用回调函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_COMPACT_OUT</p></td>
<td align="left"><p>换行符不打印后每个成员。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_ARRAY</p></td>
<td align="left"><p>符号是一个数组。 该成员指定数组中元素的数目<strong>listLink-&gt;大小</strong>SYM_DUMP_PARAM 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_ADDRESS_OF_FIELD</p></td>
<td align="left"><p>值<strong>addr</strong>是实际的成员的地址<strong>listLink-&gt;fName</strong> SYM_DUMP_PARAM 结构和不符号开头。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_ADDRESS_AT_END</p></td>
<td align="left"><p>值<strong>addr</strong>是实际在符号末尾的和不符号开头的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_COPY_TYPE_DATA</p></td>
<td align="left"><p>符号的值复制到该成员<strong>pBuffer</strong>。 这只能使用对于基元类型--例如，ULONG 或 PVOID-它无法使用的结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_READ_PHYSICAL</p></td>
<td align="left"><p>将从目标计算机的物理内存中直接读取符号的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FUNCTION_FORMAT</p></td>
<td align="left"><p>格式设置时有一种函数类型的符号，函数将使用格式，例如， <code>function(arg1, arg2, ...)</code></p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_BLOCK_RECURSE</p></td>
<td align="left"><p>通过嵌套结构; recurse但不是遵循指针。</p></td>
</tr>
</tbody>
</table>

 

此外，宏 DBG 的结果\_转储\_重复\_级别 (*级别*) 可以添加到要指定如何深入了解结构要进行递归的位集。 *级别*可以是介于 0 到 15 之间的数字。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Wdbgexts.h （包括 Wdbgexts.h、 Wdbgexts.h 或 Dbgeng.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**IG\_转储\_符号\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff550906)

[**Ioctl**](https://msdn.microsoft.com/library/windows/hardware/ff551084)

 

 






