---
title: EXT \_ TDOP \_ 输出 \_ 类型 \_ 名称
description: "\"调试请求\" 的 \"EXT \\_ TDOP \\_ OUTPUT \\_ 类型 \\_ 名称\" 子操作 \" \\_ Ext 类型 \\_ \\_ 化 \\_ 数据 \\_ ANSI 请求\" 操作会打印指定类型化数据的类型名称。"
keywords:
- EXT_TDOP_OUTPUT_TYPE_NAME Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_TYPE_NAME
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dff05a69eb552d7d1c577a9028b719ca9f3caa3d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829973"
---
# <a name="ext_tdop_output_type_name"></a>EXT \_ TDOP \_ 输出 \_ 类型 \_ 名称


"调试请求" 的 "EXT \_ TDOP \_ OUTPUT \_ 类型 \_ 名称" 子操作 " [**ext 类型 \_ \_ \_ 化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md) " 操作会打印指定类型化数据的类型名称。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT \_ TDOP \_ \_ \_ 此子操作的输出类型名称。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定将打印其类型名称的类型化数据。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

类型名称将发送到调试器引擎的 [输出回调](./using-input-and-output.md#output-callbacks)。

EXT \_ TDOP \_ OUTPUT \_ TYPE \_ NAME 是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

