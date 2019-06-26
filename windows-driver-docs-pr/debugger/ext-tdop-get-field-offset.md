---
title: EXT\_TDOP\_GET\_FIELD\_OFFSET
description: EXT\_TDOP\_获取\_字段\_偏移量子操作的调试\_请求\_EXT\_类型化\_数据\_ANSI 请求操作返回在结构中成员的偏移量。
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
ms.openlocfilehash: 1d12cd2a78a51fb2c4ffbd6ae37b4dd47fd01d6f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361359"
---
# <a name="exttdopgetfieldoffset"></a>EXT\_TDOP\_GET\_FIELD\_OFFSET


EXT\_TDOP\_获取\_字段\_偏移量的子操作[**调试\_请求\_EXT\_类型化\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作将返回在结构中成员的偏移量。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**Operation**  
设置为 EXT\_TDOP\_获取\_字段\_此子操作的偏移量。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定表示包含正在请求其偏移量的成员的结构的实例的类型化的数据。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定正在请求其偏移量的成员的名称。 名称是以点号分隔的路径，并且可以包含子成员。 例如， **mymember.mysubmember**。 将自动取消引用此以点号分隔的路径上的指针。 但是，点运算符 ( **。** ) 仍可使用此处而不是常用的 C 指针取消引用运算符 ( **-&gt;** )。

<span id="Out32"></span><span id="out32"></span><span id="OUT32"></span>**Out32**  
接收的结构的实例中的成员的偏移量。 这是实例的结构的开头和成员之间的字节数。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
接收此子操作返回的状态代码。 这是与返回的值相同[**请求**](request.md)。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_获取\_字段\_偏移量是中的值[ **EXT\_TDOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)枚举。

此子操作的参数属于[ **EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)结构。 EXT 隶属\_类型化\_前面的参数部分中未列出的数据不使用此子操作，应设置为零。 前面的 Parameters 节中的成员的说明指定使用的成员。 请参阅**EXT\_类型化\_数据**的更多详细信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DEBUG\_REQUEST\_EXT\_TYPED\_DATA\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**请求**](request.md)

 

 






