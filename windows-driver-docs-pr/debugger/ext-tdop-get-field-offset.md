---
title: EXT \_ TDOP \_ GET \_ FIELD \_ OFFSET
description: '\_调试请求的 ext TDOP \_ GET \_ FIELD \_ OFFSET 子操作 \_ \_ ext \_ 类型化 \_ 数据 \_ ANSI 请求操作返回结构内成员的偏移量。'
keywords:
- EXT_TDOP_GET_FIELD_OFFSET Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_FIELD_OFFSET
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd70725c6785fd5886e18abfe092f4f7ab1da611
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839953"
---
# <a name="ext_tdop_get_field_offset"></a>EXT \_ TDOP \_ GET \_ FIELD \_ OFFSET


\_调试请求的 ext TDOP \_ GET \_ FIELD \_ OFFSET 子操作 [**\_ \_ ext \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作返回结构内成员的偏移量。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT \_ TDOP \_ 获取 \_ \_ 此子操作的字段偏移量。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定表示结构实例的类型化数据，该结构包含要请求其偏移量的成员。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定要请求其偏移量的成员的名称。 该名称是一个点分隔的路径，可以包含子成员。 例如， **mymember. mysubmember**。 此点分隔路径上的指针将自动取消引用。 但是，点 **运算符 (，** 此处仍应使用) ，而不是常规的 C 指针取消引用运算符 (**-&gt;**) 。

<span id="Out32"></span><span id="out32"></span><span id="OUT32"></span>**Out32**  
接收结构的实例内的成员的偏移量。 这是结构实例和成员之间的字节数。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT \_ TDOP \_ GET \_ FIELD \_ OFFSET 是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

