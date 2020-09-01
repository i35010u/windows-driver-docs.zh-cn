---
title: EXT \_ TDOP \_ 评估
description: EXT \_ TDOP \_ 评估调试请求的子操作 " \_ \_ ext \_ 类型化 \_ 数据 \_ ANSI 请求" 操作返回表示表达式的值的类型化数据说明。
ms.assetid: 2df6cf92-6889-4407-93c0-4c777a68cbc8
keywords:
- EXT_TDOP_EVALUATE Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_EVALUATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80527c29d629df478992e553413484d2f3725f2a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213019"
---
# <a name="ext_tdop_evaluate"></a>EXT \_ TDOP \_ 评估


EXT \_ TDOP \_ 评估调试请求的子操作 " [** \_ \_ ext \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md) " 操作返回表示表达式的值的类型化数据说明。

**参数**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
\_对于此子操作，设置为 EXT TDOP \_ 评估。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**随意**  
指定用于描述表达式的值所在的目标内存的位标志。 有关这些标志的详细信息，请参阅 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定可在 **InStrIndex**指定的表达式中使用其值的可选类型化数据。 表达式将此值用作伪寄存器 **$extin**。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收表示表达式的值的 [**调试 \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data) 结构。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定要计算的表达式。 此表达式通过默认表达式计算器进行计算。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT \_ TDOP \_ 评估是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

