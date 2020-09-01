---
title: DBG \_ 转储 \_ 字段 \_ XXX
description: DBG \_ 转储 \_ 字段 \_ XXX
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
ms.openlocfilehash: 8e5f4cfc7451f64752878d417ee7de1546108789
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210867"
---
# <a name="dbg_dump_field_xxx"></a>DBG \_ 转储 \_ 字段 \_ XXX


## <span id="ddk_dbg_dump_xxx_dbx"></span><span id="DDK_DBG_DUMP_XXX_DBX"></span>


\_ \_ \_ [**字段 \_ 信息**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_field_info)结构的**用于**成员使用 DBG 转储字段*XXX*位标志来控制[**IG \_ 转储 \_ 符号 \_ 信息**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_sym_dump_param)[**Ioctl**](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作的行为。

可以存在以下标志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志</th>
<th align="left">效果</th>
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
<td align="left"><p><strong>fName</strong> 必须完全匹配，而不是只需具有匹配的前缀即可处理要处理的成员。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_ARRAY</p></td>
<td align="left"><p>打印数组成员的数组元素。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_COPY_FIELD_DATA</p></td>
<td align="left"><p>成员的值将复制到 <strong>pBuffer</strong>中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_RETURN_ADDRESS</p></td>
<td align="left"><p>在回调期间或 <strong>Ioctl</strong> 返回时，FIELD_INFO。<strong>address</strong> 成员包含符号成员的地址。</p>
<p>如果没有为类型提供地址，则 FIELD_INFO。<strong>address</strong> 包含成员相对于类型开始的总偏移量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_SIZE_IN_BITS</p></td>
<td align="left"><p>对于位域，返回以位而不是字节表示的偏移和大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_NO_PRINT</p></td>
<td align="left"><p>请勿打印此成员 (仅调用回调函数并) 执行数据复制。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_DEFAULT_STRING DBG_DUMP_FIELD_WCHAR_STRING DBG_DUMP_FIELD_MULTI_STRING DBG_DUMP_FIELD_GUID_STRING</p></td>
<td align="left"><p>如果成员是一个指针，则将其打印为字符串、ANSI 字符串、WCHAR 字符串、多字符串或 GUID。</p></td>
</tr>
</tbody>
</table>

 

此外，宏 DBG 转储的结果 \_ \_ \_ (*级别*) 可添加到位集，以指定要递归的结构的深度。 *级别* 可以是0到15之间的数字。

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
<td align="left"> (包含 Wdbgexts、Wdbgexts 或 Dbgeng 的 Wdbgexts) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**IG \_ 转储 \_ 符号 \_ 信息**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_sym_dump_param)

[**Ioctl**](/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)

[**字段 \_ 信息**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_field_info)

 

