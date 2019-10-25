---
title: DBG\_转储\_XXX
description: DBG\_转储\_XXX
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
ms.openlocfilehash: cec17542dc42a26d5514b54e6b08ff560f93d5a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837803"
---
# <a name="dbg_dump_xxx"></a>DBG\_转储\_XXX


## <span id="ddk_dbg_dump_xxx_dbx"></span><span id="DDK_DBG_DUMP_XXX_DBX"></span>


符号\_\_DUMP 的**Options**成员使用 DBG\_转储\_*XXX*位标志来控制[**IG\_转储\_符号\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_sym_dump_param)[**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)的行为运作.

可以存在以下标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">旗帜</th>
<th align="left">作用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DBG_DUMP_NO_INDENT</p></td>
<td align="left"><p>成员不会在输出中缩进。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_NO_OFFSET</p></td>
<td align="left"><p>不打印偏移量。</p></td>
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
<td align="left"><p>符号是链接列表中的条目，IG_DUMP_SYMBOL_INFO <strong>Ioctl</strong>操作将循环访问此列表。 指向列表中下一项的成员的说明由 SYM_DUMP_PARAM 结构的<strong>linkList</strong>成员指定。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_NO_PRINT</p></td>
<td align="left"><p>不打印任何内容（仅调用回调函数并执行数据副本）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_GET_SIZE_ONLY</p></td>
<td align="left"><p><strong>Ioctl</strong>操作仅返回符号的大小;它不会打印成员信息或调用回调函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_COMPACT_OUT</p></td>
<td align="left"><p>不会在每个成员后打印换行符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_ARRAY</p></td>
<td align="left"><p>符号为数组。 数组中元素的数目由 SYM_DUMP_PARAM 结构的成员<strong>listLink&gt;大小</strong>指定。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_ADDRESS_OF_FIELD</p></td>
<td align="left"><p><strong>Addr</strong>的值实际上是 SYM_DUMP_PARAM 结构的成员<strong>&gt;listLink fName</strong>的地址，而不是符号的开头。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_ADDRESS_AT_END</p></td>
<td align="left"><p><strong>Addr</strong>的值实际上是符号末尾的地址，而不是符号的开头。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_COPY_TYPE_DATA</p></td>
<td align="left"><p>符号的值将复制到成员<strong>pBuffer</strong>中。 它只能用于基元类型，例如 ULONG 或 PVOID--不能用于结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_READ_PHYSICAL</p></td>
<td align="left"><p>将直接从目标的物理内存中读取符号的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FUNCTION_FORMAT</p></td>
<td align="left"><p>在设置具有函数类型的符号的格式时，将使用函数格式，例如 <code>function(arg1, arg2, ...)</code></p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_BLOCK_RECURSE</p></td>
<td align="left"><p>通过嵌套结构递归;但不要关注指针。</p></td>
</tr>
</tbody>
</table>

 

此外，还可以向位集添加宏 DBG\_转储\_重复\_级别（*级别*）的结果，以指定要递归的结构的深度。 *级别*可以是0到15之间的数字。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Wdbgexts （包括 Wdbgexts、Wdbgexts 或 Dbgeng）。</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**IG\_转储\_符号\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_sym_dump_param)

[**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)

 

 






