---
title: 调试\_请求\_EXT\_类型\_数据\_ANSI
description: 调试\_请求\_EXT\_类型\_数据\_ANSI
ms.assetid: ac883bc8-3956-4bc3-a11e-b6e036305329
keywords:
- DEBUG_REQUEST_EXT_TYPED_DATA_ANSI Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_EXT_TYPED_DATA_ANSI
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 676cb449a0804ef2e4395750923e711cd7e7346c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837798"
---
# <a name="debug_request_ext_typed_data_ansi"></a>调试\_请求\_EXT\_类型\_数据\_ANSI


调试\_请求\_EXT\_类型\_数据\_ANSI[**请求**](request.md)操作执行各种不同的子操作，这些子操作有助于解释类型化数据。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
指定用于确定要执行的子操作的[ **\_数据结构的 EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 。 此扩展\_类型化\_数据结构包含该子操作的输入参数以及任何（可选）附加数据。 其他数据将包含在*InBuffer*中的 EXT\_类型\_数据结构之后。 *InBuffer*的大小是包含类型\_数据结构和其他数据的扩展\_的缓冲区的总大小。 有关此结构的详细信息，请参阅**EXT\_类型化的\_数据**，以及如何包含其他数据。

支持以下子操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">子操作</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-copy.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_COPY&lt;/strong&gt;](ext-tdop-copy.md)"><strong>EXT_TDOP_COPY</strong></a></p></td>
<td align="left"><p>创建类型化数据说明的副本。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-release.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_RELEASE&lt;/strong&gt;](ext-tdop-release.md)"><strong>EXT_TDOP_RELEASE</strong></a></p></td>
<td align="left"><p>释放类型化数据说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-set-from-expr.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_FROM_EXPR&lt;/strong&gt;](ext-tdop-set-from-expr.md)"><strong>EXT_TDOP_SET_FROM_EXPR</strong></a></p></td>
<td align="left"><p>返回表达式的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-set-from-u64-expr.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_FROM_U64_EXPR&lt;/strong&gt;](ext-tdop-set-from-u64-expr.md)"><strong>EXT_TDOP_SET_FROM_U64_EXPR</strong></a></p></td>
<td align="left"><p>返回表达式的值。 可选地址可作为参数提供给表达式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-field.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_FIELD&lt;/strong&gt;](ext-tdop-get-field.md)"><strong>EXT_TDOP_GET_FIELD</strong></a></p></td>
<td align="left"><p>返回结构的成员。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-evaluate.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_EVALUATE&lt;/strong&gt;](ext-tdop-evaluate.md)"><strong>EXT_TDOP_EVALUATE</strong></a></p></td>
<td align="left"><p>返回表达式的值。 可选值可以作为参数提供给表达式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-type-name.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_TYPE_NAME&lt;/strong&gt;](ext-tdop-get-type-name.md)"><strong>EXT_TDOP_GET_TYPE_NAME</strong></a></p></td>
<td align="left"><p>返回类型化数据的类型名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-output-type-name.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_TYPE_NAME&lt;/strong&gt;](ext-tdop-output-type-name.md)"><strong>EXT_TDOP_OUTPUT_TYPE_NAME</strong></a></p></td>
<td align="left"><p>打印类型化数据的类型名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-output-simple-value.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_SIMPLE_VALUE&lt;/strong&gt;](ext-tdop-output-simple-value.md)"><strong>EXT_TDOP_OUTPUT_SIMPLE_VALUE</strong></a></p></td>
<td align="left"><p>打印类型化数据的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-output-full-value.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_FULL_VALUE&lt;/strong&gt;](ext-tdop-output-full-value.md)"><strong>EXT_TDOP_OUTPUT_FULL_VALUE</strong></a></p></td>
<td align="left"><p>打印类型化数据的类型和值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-has-field.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_HAS_FIELD&lt;/strong&gt;](ext-tdop-has-field.md)"><strong>EXT_TDOP_HAS_FIELD</strong></a></p></td>
<td align="left"><p>确定结构是否包含指定的成员。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-get-field-offset.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_FIELD_OFFSET&lt;/strong&gt;](ext-tdop-get-field-offset.md)"><strong>EXT_TDOP_GET_FIELD_OFFSET</strong></a></p></td>
<td align="left"><p>返回结构内成员的偏移量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-array-element.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_ARRAY_ELEMENT&lt;/strong&gt;](ext-tdop-get-array-element.md)"><strong>EXT_TDOP_GET_ARRAY_ELEMENT</strong></a></p></td>
<td align="left"><p>返回数组中的一个元素。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-get-dereference.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_DEREFERENCE&lt;/strong&gt;](ext-tdop-get-dereference.md)"><strong>EXT_TDOP_GET_DEREFERENCE</strong></a></p></td>
<td align="left"><p>取消引用指针，返回它所指向的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-type-size.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_TYPE_SIZE&lt;/strong&gt;](ext-tdop-get-type-size.md)"><strong>EXT_TDOP_GET_TYPE_SIZE</strong></a></p></td>
<td align="left"><p>返回指定的类型化数据的大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-output-type-definition.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_TYPE_DEFINITION&lt;/strong&gt;](ext-tdop-output-type-definition.md)"><strong>EXT_TDOP_OUTPUT_TYPE_DEFINITION</strong></a></p></td>
<td align="left"><p>为指定的类型化数据打印类型的定义。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-pointer-to.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_POINTER_TO&lt;/strong&gt;](ext-tdop-get-pointer-to.md)"><strong>EXT_TDOP_GET_POINTER_TO</strong></a></p></td>
<td align="left"><p>返回表示指向指定类型化数据的指针的新类型化数据说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-set-from-type-id-and-u64.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_FROM_TYPE_ID_AND_U64&lt;/strong&gt;](ext-tdop-set-from-type-id-and-u64.md)"><strong>EXT_TDOP_SET_FROM_TYPE_ID_AND_U64</strong></a></p></td>
<td align="left"><p>从类型和内存位置创建类型化的数据说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-set-ptr-from-type-id-and-u64.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64&lt;/strong&gt;](ext-tdop-set-ptr-from-type-id-and-u64.md)"><strong>EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64</strong></a></p></td>
<td align="left"><p>创建一个类型化的数据说明，该说明表示指向具有指定类型的指定内存位置的指针。</p></td>
</tr>
</tbody>
</table>

 

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
接收包含输出参数和子操作的任何其他数据的[**类型\_数据结构的 EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 。 与*InBuffer*一样， *OutBuffer*的大小是包含\_数据结构和任何其他数据的扩展\_类型的总大小。

调试\_请求\_EXT\_类型\_数据\_ANSI 操作最初将*InBuffer*复制到*OutBuffer* ，然后修改就地*OutBuffer*的内容。 这意味着*OutBuffer*将用\_数据的 EXT\_的输入参数以及在*InBuffer*中提供的任何附加数据填充。 这也意味着*OutBuffer*的大小必须至少与*InBuffer*的大小相同。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

<span id="S_OK"></span><span id="s_ok"></span>S\_确定  
操作成功。

此方法还可以返回错误值。 有关更多详细信息，请参阅[**返回值**](https://docs.microsoft.com/windows-hardware/drivers/debugger/hresult-values)。

此操作返回的值还存储在*OutBuffer*的**Status**成员中。

<a name="remarks"></a>备注
-------

调试\_请求所执行的子操作\_EXT\_类型\_数据\_ANSI[**请求**](request.md)操作由[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)结构的**操作**成员确定，它采用[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的值。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**需要**](request.md)

 

 






