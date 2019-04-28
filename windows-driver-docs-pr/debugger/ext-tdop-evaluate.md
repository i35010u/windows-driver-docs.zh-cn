---
title: EXT\_TDOP\_EVALUATE
description: EXT\_TDOP\_评估子操作的调试\_请求\_EXT\_类型化\_数据\_ANSI 请求的操作返回的类型化的数据说明表示表达式的值。
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
ms.openlocfilehash: 0c80df88845aeddae6418f471d1adf1a90ab7e4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329626"
---
# <a name="exttdopevaluate"></a>EXT\_TDOP\_EVALUATE


EXT\_TDOP\_评估的子操作[**调试\_请求\_EXT\_类型化\_数据\_ANSI** ](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作将返回表示表达式的值的类型化的数据说明。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**Operation**  
设置为 EXT\_TDOP\_评估此子操作。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**标志**  
指定描述表达式的值所在的目标的内存的位标志。 请参阅[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)的这些标志的详细信息。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定可以使用其值的可选类型化的数据中指定的表达式**InStrIndex**。 此值由表达式作为伪寄存器 **$extin**。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收[**调试\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff541706)结构，它表示的表达式的值。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定要计算的表达式。 默认表达式计算器计算此表达式。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
接收此子操作返回的状态代码。 这是与返回的值相同[**请求**](request.md)。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_评估是中的值[ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)枚举。

此子操作的参数属于[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)结构。 EXT 隶属\_类型化\_前面的参数部分中未列出的数据不使用此子操作，应设置为零。 前面的 Parameters 节中的成员的说明指定使用的成员。 请参阅**EXT\_类型化\_数据**的更多详细信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DEBUG\_REQUEST\_EXT\_TYPED\_DATA\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**请求**](request.md)

 

 






