---
title: EXT\_TDOP\_获取\_数组\_元素
description: EXT\_TDOP\_获取\_数组\_元素的子操作的调试\_请求\_EXT\_类型化\_数据\_ANSI 请求操作从数组中返回的元素。
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
ms.openlocfilehash: b7d15155b4130a5df52b953998858d0146c17881
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332090"
---
# <a name="exttdopgetarrayelement"></a>EXT\_TDOP\_获取\_数组\_元素


EXT\_TDOP\_获取\_数组\_元素的子操作[**调试\_请求\_EXT\_类型化\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作从数组中返回的元素。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**Operation**  
设置为 EXT\_TDOP\_获取\_数组\_此子操作的元素。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定正在请求其元素的数组。 **InData**还可以指定一个指针，在这种情况下它将被视为一个数组。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
从数组中接收请求的元素。

<span id="In64"></span><span id="in64"></span><span id="IN64"></span>**In64**  
指定数组中元素的索引。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
接收此子操作返回的状态代码。 这是与返回的值相同[**请求**](request.md)。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_获取\_数组\_元素是中的值[ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)枚举。

此子操作的参数属于[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)结构。 EXT 隶属\_类型化\_前面的参数部分中未列出的数据不使用此子操作，应设置为零。 前面的 Parameters 节中的成员的说明指定使用的成员。 请参阅**EXT\_类型化\_数据**的更多详细信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DEBUG\_REQUEST\_EXT\_TYPED\_DATA\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**请求**](request.md)

 

 






