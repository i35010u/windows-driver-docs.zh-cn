---
title: DBG\_DUMP\_FIELD\_XXX
description: DBG\_DUMP\_FIELD\_XXX
ms.assetid: c168c1b7-c4ef-4a70-9060-611b86120635
ms.date: 12/07/2017
keywords:
- DBG_DUMP_FIELD_XXX Windows 调试
topic_type:
- apiref
api_name:
- DBG_DUMP_FIELD_XXX
api_location:
- wdbgexts.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 801f794c62a429485a550f72dd53ec9c9f86caa1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376117"
---
# <a name="dbgdumpfieldxxx"></a>DBG\_DUMP\_FIELD\_XXX


## <span id="ddk_dbg_dump_xxx_dbx"></span><span id="DDK_DBG_DUMP_XXX_DBX"></span>


DBG\_转储\_字段\_*XXX*位标志由**fOptions**隶属[**字段\_信息** ](https://msdn.microsoft.com/library/windows/hardware/ff545316)结构，以控制的行为[ **IG\_转储\_符号\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff550906) [ **Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084)操作。

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
<td align="left"><p>DBG_DUMP_FIELD_CALL_BEFORE_PRINT</p></td>
<td align="left"><p>打印该成员之前调用回调函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_NO_CALLBACK_REQ</p></td>
<td align="left"><p>不调用任何回调函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_RECUR_ON_THIS</p></td>
<td align="left"><p>子成员的成员进行处理。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_FULL_NAME</p></td>
<td align="left"><p><strong>fName</strong>而不只是要处理的成员匹配的前缀，必须完全匹配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_ARRAY</p></td>
<td align="left"><p>打印数组成员的数组元素。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_COPY_FIELD_DATA</p></td>
<td align="left"><p>成员的值复制到<strong>pBuffer</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_RETURN_ADDRESS</p></td>
<td align="left"><p>在回调过程时，或者当<strong>Ioctl</strong>返回 FIELD_INFO。<strong>地址</strong>成员包含符号的成员的地址。</p>
<p>如果为的类型，FIELD_INFO 提供任何地址。<strong>地址</strong>包含总偏移量从一开始类型的成员。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_SIZE_IN_BITS</p></td>
<td align="left"><p>对于位字段，以位而不是字节为单位返回的偏移量和大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_NO_PRINT</p></td>
<td align="left"><p>（仅调用回调函数和执行数据副本），则无法打印此成员。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_DEFAULT_STRING DBG_DUMP_FIELD_WCHAR_STRING DBG_DUMP_FIELD_MULTI_STRING DBG_DUMP_FIELD_GUID_STRING</p></td>
<td align="left"><p>如果该成员是一个指针，它将打印为字符串、 ANSI 字符串、 WCHAR 字符串、 多字符串或 GUID。</p></td>
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

[**FIELD\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff545316)

 

 






