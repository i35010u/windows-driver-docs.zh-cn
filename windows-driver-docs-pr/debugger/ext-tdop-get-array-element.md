---
title: EXT\_TDOP\_获取\_数组\_元素
description: EXT\_TDOP\_获取调试\_请求\_数组\_元素子操作\_EXT\_类型\_数据\_ANSI 请求操作返回数组中的元素。
ms.assetid: 67c87b14-3580-4507-884e-b02576ce7be2
keywords:
- EXT_TDOP_GET_ARRAY_ELEMENT Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_ARRAY_ELEMENT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc33b51ff92029743dfe6086bed78ac87278c031
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826509"
---
# <a name="ext_tdop_get_array_element"></a>EXT\_TDOP\_获取\_数组\_元素


EXT\_TDOP\_获取调试\_请求\_数组\_元素子操作[ **\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作返回数组中的元素。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
设置为 EXT\_TDOP\_获取此子操作\_数组\_元素。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定正在请求其元素的数组。 **InData**还可以指定指针，在这种情况下，它将被视为一个数组。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收数组中请求的元素。

<span id="In64"></span><span id="in64"></span><span id="IN64"></span>**In64**  
指定数组中元素的索引。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与[**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_GET\_ARRAY\_元素是[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)枚举中的一个值。

此子操作的参数是[**类型\_数据结构的 EXT\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)的成员。 此子操作不使用 EXT\_类型化\_数据的成员，此子操作不使用该类型的数据，应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅**EXT\_类型化的\_数据**。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试\_请求\_EXT\_类型\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**需要**](request.md)

 

 






