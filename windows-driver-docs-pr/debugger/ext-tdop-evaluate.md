---
title: 扩展\_TDOP\_评估
description: EXT\_TDOP\_评估调试\_请求的子操作\_EXT\_类型\_数据\_ANSI 请求操作返回表示表达式值的类型化数据说明。
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
ms.openlocfilehash: a51949a330074584b59d5254e5d27b0a4f9187fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826529"
---
# <a name="ext_tdop_evaluate"></a>扩展\_TDOP\_评估


EXT\_TDOP\_评估调试\_请求的子操作[ **\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作返回表示的值的类型化数据说明表达式.

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT\_TDOP\_计算此子操作。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**随意**  
指定用于描述表达式的值所在的目标内存的位标志。 有关这些标志的详细信息，请参阅[**EXT\_类型化的\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定可在**InStrIndex**指定的表达式中使用其值的可选类型化数据。 表达式将此值用作伪寄存器 **$extin**。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收[ **\_数据结构的调试\_类型化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)，该结构表示表达式的值。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定要计算的表达式。 此表达式通过默认表达式计算器进行计算。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与[**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_计算是[**ext\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的一个值。

此子操作的参数是[**类型\_数据结构的 EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)的成员。 此子操作不使用 EXT\_类型化\_数据的成员，此子操作不使用该类型的数据，应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅**EXT\_类型化的\_数据**。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试\_请求\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**需要**](request.md)

 

 






