---
title: EXT \_ TDOP \_ OUTPUT \_ 简单 \_ 值
description: "\"调试\" 请求的 \"EXT \\_ TDOP \\_ OUTPUT \\_ 简单 \\_ 值\" 子操作将 \\_ \\_ \\_ \\_ \\_ 打印指定的类型化数据的值。"
keywords:
- EXT_TDOP_OUTPUT_SIMPLE_VALUE Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_SIMPLE_VALUE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8af20de3b8c42493bb391b41ad333d62bd1f02a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837823"
---
# <a name="ext_tdop_output_simple_value"></a>EXT \_ TDOP \_ OUTPUT \_ 简单 \_ 值


"调试" 请求的 "EXT \_ TDOP \_ OUTPUT \_ 简单 \_ 值" 子操作将打印指定的类型化数据的值。 [**\_ \_ \_ \_ \_**](debug-request-ext-typed-data-ansi.md)[**Request**](request.md)

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT \_ TDOP \_ OUTPUT \_ \_ 此子操作的简单值。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定将打印其值的类型化数据。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

值已设置格式，并发送到调试器引擎的 [输出回调](./using-input-and-output.md#output-callbacks)。

EXT \_ TDOP \_ OUTPUT \_ 简单 \_ 值是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

