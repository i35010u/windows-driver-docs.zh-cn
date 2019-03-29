---
title: EXT\_TDOP\_HAS\_FIELD
description: EXT\_TDOP\_HAS\_字段的调试子操作\_请求\_EXT\_类型化\_数据\_ANSI 请求的操作将确定如果结构包含指定的成员。
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
ms.openlocfilehash: 0f81f57aa3beebbc3813c2cc8ba392031d6e8f60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576587"
---
# <a name="exttdophasfield"></a>EXT\_TDOP\_HAS\_FIELD


EXT\_TDOP\_HAS\_字段的子操作[**调试\_请求\_EXT\_类型化\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md) [**请求**](request.md)操作确定一个结构是否包含指定的成员。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**Operation**  
设置为 EXT\_TDOP\_HAS\_此子操作的字段。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定检查存在该成员的类型化的数据。 类型化的数据首先检查是否表示结构的实例，然后检查结构，以确定它是否包含指定的成员。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定的成员的名称。 名称是以点号分隔的路径和包含子成员-例如， **mymember.mysubmember**。 将自动取消引用此以点号分隔的路径上的指针。 但是，点运算符 (**。**) 仍可使用此处而不是常用的 C 指针取消引用运算符 (**-&gt;**)。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
接收此子操作返回的状态代码。 这是与返回的值相同[**请求**](request.md)。

如果类型化的数据中的成员，**状态**接收 S\_确定。 如果类型化的数据不包含该成员**状态**接收电子\_NOINTERFACE。 可能还会返回其他错误值。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_HAS\_字段是中的值[ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)枚举。

此子操作的参数属于[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)结构。 EXT 隶属\_类型化\_前面的参数部分中未列出的数据不使用此子操作，应设置为零。 前面的 Parameters 节中的成员的说明指定使用的成员。 请参阅**EXT\_类型化\_数据**的更多详细信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DEBUG\_REQUEST\_EXT\_TYPED\_DATA\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**请求**](request.md)

 

 






