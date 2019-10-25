---
title: EXT\_TDOP\_设置\_\_U64\_EXPR
description: EXT\_TDOP\_从调试\_请求的\_U64\_EXPR sub 操作设置\_\_EXT\_类型\_DATA\_ANSIRequest 操作返回一个表示表达式的值。
ms.assetid: 3d0007f8-09c7-4333-a1f0-090918c9f8fa
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
ms.openlocfilehash: 981bee5b9f5ee0aa834072a3722076d7180a93a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838761"
---
# <a name="ext_tdop_set_from_u64_expr"></a>EXT\_TDOP\_设置\_\_U64\_EXPR


EXT\_TDOP\_设置\_\_从调试\_请求的 U64\_EXPR sub 操作\_[**EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作返回类型化数据表示表达式的值的说明。

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT\_TDOP\_将\_从\_U64\_EXPR 设置为此子操作。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**随意**  
指定用于描述表达式的值所在的目标内存的位标志。 有关这些标志的详细信息，请参阅[**EXT\_类型化的\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定可在**InStrIndex**指定的表达式中使用目标内存中的地址的可选类型化数据。 表达式使用此地址作为伪寄存器 **$extin**。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收[ **\_数据结构的调试\_类型化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)，该结构表示表达式的值。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定要计算的表达式。 此表达式通过默认表达式计算器进行计算。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与[**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_从\_U64 设置\_\_EXPR 是[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的一个值。

此子操作的参数是[**类型\_数据结构的 EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)的成员。 此子操作不使用 EXT\_类型化\_数据的成员，此子操作不使用该类型的数据，应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅**EXT\_类型化的\_数据**。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试\_请求\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**需要**](request.md)

 

 






