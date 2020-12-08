---
title: 调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI
description: 调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI
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
ms.openlocfilehash: 1f0be8d9843ceee6617d020b1c169769cf126b3f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787797"
---
# <a name="debug_request_ext_typed_data_ansi"></a>调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI


DEBUG \_ 请求 \_ EXT \_ 类型化的 \_ 数据 \_ ANSI [**请求**](request.md) 操作执行各种不同的子操作，有助于解释类型化数据。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
指定用于确定要执行的子操作的 [**EXT \_ 类型化的 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构。 此扩展 \_ 类型化 \_ 数据结构包含该子操作的输入参数以及任何 (可选) 其他数据。 其他数据将包含在 *InBuffer* 中的 EXT \_ 类型化 \_ 数据结构之后。 *InBuffer* 的大小是包含 EXT \_ 类型化 \_ 数据结构和其他数据的缓冲区的总大小。 有关此结构的详细信息以及如何包含其他数据，请参阅 **EXT \_ 类型化 \_ 数据** 。

支持以下子操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Sub-Operation</th>
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
接收包含输出参数和子操作的任何其他数据的 [**EXT \_ 类型化的 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构。 与 *InBuffer* 一样， *OutBuffer* 的大小是包含 EXT \_ 类型化 \_ 数据结构和任何其他数据的缓冲区的总大小。

"调试" \_ 请求 \_ EXT \_ 类型化 \_ \_ 的数据 ANSI 操作最初会将 *InBuffer* 复制到 *OutBuffer* ，然后就地修改 *OutBuffer* 的内容。 这意味着将 *OutBuffer* 用 EXT \_ 类型化数据的输入参数 \_ 以及在 *InBuffer* 中提供的任何附加数据填充 OutBuffer。 这也意味着 *OutBuffer* 的大小必须至少与 *InBuffer* 的大小相同。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

<span id="S_OK"></span><span id="s_ok"></span>S \_ 正常  
操作成功。

此方法还可以返回错误值。 有关更多详细信息，请参阅 [**返回值**](./hresult-values.md) 。

此操作返回的值还存储在 *OutBuffer* 的 **Status** 成员中。

<a name="remarks"></a>备注
-------

由调试 \_ 请求 \_ 扩展 \_ 类型化数据 ANSI 请求操作执行的子操作由 \_ \_ [**Ext \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)结构的 **操作** 成员确定，该结构在 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中采用值。 [**Request**](request.md)

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**Request**](request.md)

 

