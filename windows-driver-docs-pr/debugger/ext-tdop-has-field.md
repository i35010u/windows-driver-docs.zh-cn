---
title: EXT\_TDOP\_有\_字段
description: EXT\_TDOP\_具有调试\_请求的\_"字段子操作"\_类型\_数据\_ANSI 请求操作确定结构是否包含指定的成员。
ms.assetid: c1486aff-63d3-4ceb-8dce-45a9c5835c99
keywords:
- EXT_TDOP_HAS_FIELD Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_HAS_FIELD
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 823a524bfb7f71986caec66646f6a97e13c56066
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838770"
---
# <a name="ext_tdop_has_field"></a>EXT\_TDOP\_有\_字段


EXT\_TDOP\_具有调试\_请求的\_"字段子操作"\_[**类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作确定结构是否包含指定的成员。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT\_TDOP\_具有此子操作\_字段。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定检查是否存在该成员的类型化数据。 首先检查类型化数据是否表示结构的实例，然后检查结构以查看它是否包含指定的成员。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定成员的名称。 该名称是一个点分隔的路径，可以包含子成员-例如， **mymember. mysubmember**。 此点分隔路径上的指针将自动取消引用。 但是，仍应在此处使用点运算符（ **.** ），而不是常规的 C 指针取消引用运算符（ **-&gt;** ）。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与[**请求**](request.md)返回的值相同。

如果类型化数据包含成员，则 "**状态**"\_"确定"。 如果类型化数据不包含成员，则**状态**将接收 E\_NOINTERFACE。 还可能返回其他错误值。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_具有\_字段是[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的值。

此子操作的参数是[**类型\_数据结构的 EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)的成员。 此子操作不使用 EXT\_类型化\_数据的成员，此子操作不使用该类型的数据，应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅**EXT\_类型化的\_数据**。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试\_请求\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**需要**](request.md)

 

 






