---
title: DBG\_转储\_字段\_XXX
description: DBG\_转储\_字段\_XXX
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
ms.openlocfilehash: 8493e16e28a046291f78cac60a7671eaeb9017f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837800"
---
# <a name="dbg_dump_field_xxx"></a>DBG\_转储\_字段\_XXX


## <span id="ddk_dbg_dump_xxx_dbx"></span><span id="DDK_DBG_DUMP_XXX_DBX"></span>


[ **\_字段**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_field_info)的 "**用于**" 成员可以使用 "DBG\_转储\_" 字段\_*XXX*位标志，以控制[**IG\_转储\_符号\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_sym_dump_param)[**的行为Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作。

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
<td align="left"><p>DBG_DUMP_FIELD_CALL_BEFORE_PRINT</p></td>
<td align="left"><p>在打印成员之前调用回调函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_NO_CALLBACK_REQ</p></td>
<td align="left"><p>未调用回调函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_RECUR_ON_THIS</p></td>
<td align="left"><p>处理成员的 tablixmember。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_FULL_NAME</p></td>
<td align="left"><p><strong>fName</strong>必须完全匹配，而不是只需具有匹配的前缀即可处理要处理的成员。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_ARRAY</p></td>
<td align="left"><p>打印数组成员的数组元素。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_COPY_FIELD_DATA</p></td>
<td align="left"><p>成员的值将复制到<strong>pBuffer</strong>中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_RETURN_ADDRESS</p></td>
<td align="left"><p>在回调期间或<strong>Ioctl</strong>返回时，FIELD_INFO。<strong>address</strong>成员包含符号成员的地址。</p>
<p>如果没有为类型提供地址，则为 FIELD_INFO。<strong>address</strong>包含成员相对于类型开始的总偏移量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_SIZE_IN_BITS</p></td>
<td align="left"><p>对于位域，返回以位而不是字节表示的偏移和大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_NO_PRINT</p></td>
<td align="left"><p>不要打印此成员（仅调用回调函数并执行数据副本）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_DEFAULT_STRING DBG_DUMP_FIELD_WCHAR_STRING DBG_DUMP_FIELD_MULTI_STRING DBG_DUMP_FIELD_GUID_STRING</p></td>
<td align="left"><p>如果成员是一个指针，则将其打印为字符串、ANSI 字符串、WCHAR 字符串、多字符串或 GUID。</p></td>
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

[**字段\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_field_info)

 

 






