---
title: EXT \_ TDOP \_ 输出的 \_ 完整 \_ 值
description: "\"调试\" 请求的 \"EXT TDOP OUTPUT\" 的 \" \\_ \\_ \\_ 完全值\" \\_ 子操作 \" \\_ \\_ ext \\_ 类型化 \\_ 数据 \\_ ANSI 请求\" 操作会打印指定类型化数据的类型和值。"
ms.assetid: d64f7a38-c9ae-412f-985b-22115d772116
keywords:
- EXT_TDOP_OUTPUT_FULL_VALUE Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_FULL_VALUE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 751adb40a937710270833827bd9ab85eca48847d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211169"
---
# <a name="ext_tdop_output_full_value"></a>EXT \_ TDOP \_ 输出的 \_ 完整 \_ 值


"调试" 请求的 "EXT TDOP OUTPUT" 的 " \_ \_ \_ 完全值" \_ 子操作 " [** \_ \_ ext \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md) " 操作会打印指定类型化数据的类型和值。

**参数**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
\_对于此子操作，设置为 EXT TDOP \_ 输出 \_ \_ 的完整值。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定将打印其类型名称和值的类型化数据。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

类型名称和格式化值将发送到调试器引擎的 [输出回调](./using-input-and-output.md#output-callbacks)。 EXT \_ TDOP \_ output \_ FULL \_ 值打印有关值的更多详细信息，而不是 [**EXT \_ TDOP \_ OUTPUT \_ 简单 \_ 值**](ext-tdop-output-simple-value.md)。 例如，引用指针并同时打印它们指向的值。

EXT \_ TDOP \_ OUTPUT \_ FULL \_ 值是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

