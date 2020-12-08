---
title: '\_ \_ \_ \_ U64 EXPR 中的 EXT TDOP 集 \_'
description: '\_ \_ \_ \_ \_ DEBUG 请求的 U64 EXPR sub 操作的 ext TDOP 集 \_ \_ ext \_ 类型化 \_ 数据 \_ ANSIRequest 操作返回一个表示表达式的值的类型化数据说明。'
keywords:
- EXT_TDOP_SET_FROM_U64_EXPR Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_SET_FROM_U64_EXPR
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 181fcd3f9179fab99a7e59b566b2fe5f77b67c74
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840209"
---
# <a name="ext_tdop_set_from_u64_expr"></a>\_ \_ \_ \_ U64 EXPR 中的 EXT TDOP 集 \_


\_ \_ \_ \_ \_ DEBUG 请求的 U64 EXPR sub 操作的 ext TDOP 集 [**\_ \_ ext \_ 类型化的 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作返回一个表示表达式的值的类型化数据说明。

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
\_ \_ \_ \_ 对于此子操作，设置为从 U64 EXPR 的 EXT TDOP 集 \_ 。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**随意**  
指定用于描述表达式的值所在的目标内存的位标志。 有关这些标志的详细信息，请参阅 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定可在 **InStrIndex** 指定的表达式中使用目标内存中的地址的可选类型化数据。 表达式使用此地址作为伪寄存器 **$extin**。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收表示表达式的值的 [**调试 \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data) 结构。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定要计算的表达式。 此表达式通过默认表达式计算器进行计算。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

U64 EXPR 中的 EXT \_ TDOP \_ 集 \_ \_ \_ 是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

