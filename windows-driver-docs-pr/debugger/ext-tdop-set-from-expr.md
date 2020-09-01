---
title: '\_ \_ \_ 来自 EXPR 的 EXT TDOP 集 \_'
description: '\_ \_ \_ \_ 用于调试请求的 EXPR 子操作的 ext TDOP 集 \_ \_ Ext \_ 类型化的 \_ 数据 \_ ANSI 请求操作返回一个表示表达式的值的类型化数据说明。'
ms.assetid: 51d5884e-da7f-4bce-ba49-12500208d117
keywords:
- EXT_TDOP_SET_FROM_EXPR Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_SET_FROM_EXPR
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78581755eced11de552f701221ecb763d2157cfc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206813"
---
# <a name="ext_tdop_set_from_expr"></a>\_ \_ \_ 来自 EXPR 的 EXT TDOP 集 \_


\_ \_ \_ \_ 用于调试请求的 EXPR 子操作的 ext TDOP 集[** \_ \_ ext \_ 类型化的 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作返回一个表示表达式的值的类型化数据说明。

**参数**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
\_ \_ \_ \_ 对于此子操作，请将设置为 "EXT TDOP set FROM EXPR"。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**随意**  
指定用于描述表达式的值所在的目标内存的位标志。 有关这些标志的详细信息，请参阅 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收表示表达式的值的 [**调试 \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data) 结构。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定要计算的表达式。 此表达式通过默认表达式计算器进行计算。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

\_来自 EXPR 的 ext TDOP \_ SET \_ \_ 是[**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

