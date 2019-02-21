---
title: EXT\_TDOP\_SET\_PTR\_FROM\_TYPE\_ID\_AND\_U64
description: EXT\_TDOP\_设置\_PTR\_FROM\_类型\_ID\_AND\_U64 子操作的调试\_请求\_EXT\_类型化\_数据\_ANSI 请求的操作将创建表示到具有指定类型的指定的内存位置的指针的类型化的数据说明。
ms.assetid: 1ca61962-718e-4cbd-8e16-f87e0c9ec9af
keywords:
- EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64 Windows Debugging
topic_type:
- apiref
api_name:
- EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 416ffe6f75517082538a03605fe9f5ce4b1620f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534558"
---
# <a name="exttdopsetptrfromtypeidandu64"></a>EXT\_TDOP\_SET\_PTR\_FROM\_TYPE\_ID\_AND\_U64


EXT\_TDOP\_设置\_PTR\_FROM\_类型\_ID\_AND\_U64 子操作[**调试\_请求\_EXT\_类型化\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作创建类型化数据说明表示到具有指定类型的指定的内存位置的指针。

**参数**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**Operation**  
设置为 EXT\_TDOP\_设置\_PTR\_FROM\_类型\_ID\_AND\_U64 此子操作。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**标志**  
指定位标志，用于描述类型化数据的值所在的目标的内存。 请参阅[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)的这些标志的详细信息。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定的类型和内存位置。 此实例的[**调试\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff541706)结构可以手动创建并填充其所需的成员。 使用以下成员：

<span id="ModBase"></span><span id="modbase"></span><span id="MODBASE"></span>**ModBase**  
指定包含类型的模块的基址的目标的虚拟内存中的位置。

<span id="Offset"></span><span id="offset"></span><span id="OFFSET"></span>**Offset**  
在数据的目标的内存中指定的位置。 **偏移量**是虚拟内存地址，除非有标志中存在**标志**，用于指定的**偏移量**是物理内存地址。

<span id="TypeId"></span><span id="typeid"></span><span id="TYPEID"></span>**TypeId**  
指定类型的类型 ID。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收到的内存位置和类型表示的指针的类型化的数据说明。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
接收此子操作返回的状态代码。 这是与返回的值相同[**请求**](request.md)。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_设置\_PTR\_FROM\_类型\_ID\_AND\_U64 是中的值[ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)枚举。

此子操作的参数属于[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)结构。 EXT 隶属\_类型化\_前面的参数部分中未列出的数据不使用此子操作，应设置为零。 前面的 Parameters 节中的成员的说明指定使用的成员。 请参阅**EXT\_类型化\_数据**的更多详细信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DEBUG\_REQUEST\_EXT\_TYPED\_DATA\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**请求**](request.md)

 

 






