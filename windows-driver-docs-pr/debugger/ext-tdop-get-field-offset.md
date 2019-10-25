---
title: EXT\_TDOP\_获取\_字段\_偏移量
description: EXT\_TDOP\_获取\_字段\_调试\_请求的偏移子操作\_EXT\_类型\_数据\_ANSI 请求操作返回结构内成员的偏移量。
ms.assetid: 2703d518-1bc3-42a2-9a22-f9ea88a12c05
keywords:
- EXT_TDOP_GET_FIELD_OFFSET Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_FIELD_OFFSET
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2b1b59ef256d9f1739f797efd2f33c772a563ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826467"
---
# <a name="ext_tdop_get_field_offset"></a>EXT\_TDOP\_获取\_字段\_偏移量


EXT\_TDOP\_获取\_字段\_调试\_请求的偏移子操作[ **\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作返回成员在构造.

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT\_TDOP\_获取此子操作\_偏移\_字段。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定表示结构实例的类型化数据，该结构包含要请求其偏移量的成员。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定要请求其偏移量的成员的名称。 该名称是一个点分隔的路径，可以包含子成员。 例如， **mymember. mysubmember**。 此点分隔路径上的指针将自动取消引用。 但是，仍应在此处使用点运算符（ **.** ），而不是常规的 C 指针取消引用运算符（ **-&gt;** ）。

<span id="Out32"></span><span id="out32"></span><span id="OUT32"></span>**Out32**  
接收结构的实例内的成员的偏移量。 这是结构实例和成员之间的字节数。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与[**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_GET\_字段\_OFFSET 是[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的一个值。

此子操作的参数是[**类型\_数据结构的 EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)的成员。 此子操作不使用 EXT\_类型化\_数据的成员，此子操作不使用该类型的数据，应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅**EXT\_类型化的\_数据**。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试\_请求\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**需要**](request.md)

 

 






