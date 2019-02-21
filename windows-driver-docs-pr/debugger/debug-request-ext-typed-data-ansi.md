---
title: 调试\_请求\_EXT\_类型化\_数据\_ANSI
description: 调试\_请求\_EXT\_类型化\_数据\_ANSI
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
ms.openlocfilehash: c4efeb9c99f2b921b2213b714501068e8c0269d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524753"
---
# <a name="debugrequestexttypeddataansi"></a>调试\_请求\_EXT\_类型化\_数据\_ANSI


调试\_请求\_EXT\_类型化\_数据\_ANSI [**请求**](request.md)操作执行各种不同帮助解释的类型化数据的子操作。

**参数**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
指定[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)结构，它确定要执行的子操作。 此 EXT\_类型化\_数据结构中包含的输入的参数的子操作以及 （可选） 的任何其他数据。 其他数据包括在*InBuffer* EXT 后\_类型化\_数据结构。 大小*InBuffer*是包含 EXT 的缓冲区的总大小\_类型化\_数据结构和其他数据。 请参阅**EXT\_类型化\_数据**有关此结构以及如何包括附加的数据的详细信息。

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
<td align="left"><p>创建类型化的数据说明的副本。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-release.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_RELEASE&lt;/strong&gt;](ext-tdop-release.md)"><strong>EXT_TDOP_RELEASE</strong></a></p></td>
<td align="left"><p>释放类型化的数据说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-set-from-expr.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_FROM_EXPR&lt;/strong&gt;](ext-tdop-set-from-expr.md)"><strong>EXT_TDOP_SET_FROM_EXPR</strong></a></p></td>
<td align="left"><p>返回表达式的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-set-from-u64-expr.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_FROM_U64_EXPR&lt;/strong&gt;](ext-tdop-set-from-u64-expr.md)"><strong>EXT_TDOP_SET_FROM_U64_EXPR</strong></a></p></td>
<td align="left"><p>返回表达式的值。 可以作为表达式的参数提供一个可选的地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-field.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_FIELD&lt;/strong&gt;](ext-tdop-get-field.md)"><strong>EXT_TDOP_GET_FIELD</strong></a></p></td>
<td align="left"><p>返回结构的成员。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-evaluate.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_EVALUATE&lt;/strong&gt;](ext-tdop-evaluate.md)"><strong>EXT_TDOP_EVALUATE</strong></a></p></td>
<td align="left"><p>返回表达式的值。 可以作为表达式的参数提供一个可选值。</p></td>
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
<td align="left"><p>打印该值的类型化的数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-output-full-value.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_FULL_VALUE&lt;/strong&gt;](ext-tdop-output-full-value.md)"><strong>EXT_TDOP_OUTPUT_FULL_VALUE</strong></a></p></td>
<td align="left"><p>输出类型和类型化的数据值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-has-field.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_HAS_FIELD&lt;/strong&gt;](ext-tdop-has-field.md)"><strong>EXT_TDOP_HAS_FIELD</strong></a></p></td>
<td align="left"><p>确定一个结构是否包含指定的成员。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-get-field-offset.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_FIELD_OFFSET&lt;/strong&gt;](ext-tdop-get-field-offset.md)"><strong>EXT_TDOP_GET_FIELD_OFFSET</strong></a></p></td>
<td align="left"><p>返回在结构中成员的偏移量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-array-element.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_ARRAY_ELEMENT&lt;/strong&gt;](ext-tdop-get-array-element.md)"><strong>EXT_TDOP_GET_ARRAY_ELEMENT</strong></a></p></td>
<td align="left"><p>从数组中返回的元素。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-get-dereference.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_DEREFERENCE&lt;/strong&gt;](ext-tdop-get-dereference.md)"><strong>EXT_TDOP_GET_DEREFERENCE</strong></a></p></td>
<td align="left"><p>取消引用返回它所指向的值的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-type-size.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_TYPE_SIZE&lt;/strong&gt;](ext-tdop-get-type-size.md)"><strong>EXT_TDOP_GET_TYPE_SIZE</strong></a></p></td>
<td align="left"><p>返回指定的类型化数据的大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-output-type-definition.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_TYPE_DEFINITION&lt;/strong&gt;](ext-tdop-output-type-definition.md)"><strong>EXT_TDOP_OUTPUT_TYPE_DEFINITION</strong></a></p></td>
<td align="left"><p>打印指定的类型化数据类型的定义。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-pointer-to.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_POINTER_TO&lt;/strong&gt;](ext-tdop-get-pointer-to.md)"><strong>EXT_TDOP_GET_POINTER_TO</strong></a></p></td>
<td align="left"><p>返回表示指向指定的类型化数据的指针的新类型化的数据说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-set-from-type-id-and-u64.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_FROM_TYPE_ID_AND_U64&lt;/strong&gt;](ext-tdop-set-from-type-id-and-u64.md)"><strong>EXT_TDOP_SET_FROM_TYPE_ID_AND_U64</strong></a></p></td>
<td align="left"><p>从类型和内存位置中创建类型化的数据说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-set-ptr-from-type-id-and-u64.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64&lt;/strong&gt;](ext-tdop-set-ptr-from-type-id-and-u64.md)"><strong>EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64</strong></a></p></td>
<td align="left"><p>创建到指定的内存位置时提供指定的类型表示的指针的类型化的数据说明。</p></td>
</tr>
</tbody>
</table>

 

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
接收[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)结构，其中包含输出参数和子操作的任何其他数据。 如同*InBuffer*，则大小*OutBuffer*是包含 EXT 的缓冲区的总大小\_类型化\_数据结构和任何其他数据。

调试\_请求\_EXT\_类型化\_数据\_ANSI 操作最初会将复制*InBuffer*到*OutBuffer* ，然后修改的内容*OutBuffer*到位。 这意味着*OutBuffer*将使用 EXT 的输入参数填充\_类型化\_数据和在中提供的任何其他数据*InBuffer*。 这也意味着的大小*OutBuffer*必须至少与的大小一样大*InBuffer*。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

<span id="S_OK"></span><span id="s_ok"></span>S\_确定  
操作成功。

此方法还可以返回错误值。 请参阅[**返回值**](https://msdn.microsoft.com/library/windows/hardware/ff549771)的更多详细信息。

此操作返回的值也存储在**状态**的成员*OutBuffer*。

<a name="remarks"></a>备注
-------

子操作执行的调试\_请求\_EXT\_类型化\_数据\_ANSI [**请求**](request.md)确定操作通过**操作**的成员[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)结构，它采用一个值[**EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)枚举。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**请求**](request.md)

 

 






