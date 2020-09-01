---
title: EXT \_ TDOP \_ GET \_ ARRAY \_ 元素
description: "\"扩展 \\_ TDOP \\_ 获取 \\_ \\_ \" 调试请求的数组元素子操作 \\_ \\_ Ext \\_ 类型化 \\_ 的数据 \\_ ANSI 请求操作返回数组中的一个元素。"
ms.assetid: 67c87b14-3580-4507-884e-b02576ce7be2
keywords:
- EXT_TDOP_GET_ARRAY_ELEMENT Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_ARRAY_ELEMENT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d366642800eae904e2774957aa65dcca7003c69
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213017"
---
# <a name="ext_tdop_get_array_element"></a>EXT \_ TDOP \_ GET \_ ARRAY \_ 元素


"扩展 \_ TDOP \_ 获取 \_ \_ " 调试请求的数组元素子 [**操作 \_ \_ ext \_ 类型化的 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md) 操作返回数组中的一个元素。

**参数**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT \_ TDOP \_ 获取 \_ \_ 此子操作的数组元素。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定正在请求其元素的数组。 **InData** 还可以指定指针，在这种情况下，它将被视为一个数组。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收数组中请求的元素。

<span id="In64"></span><span id="in64"></span><span id="IN64"></span>**In64**  
指定数组中元素的索引。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT \_ TDOP \_ GET \_ ARRAY \_ 元素是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

