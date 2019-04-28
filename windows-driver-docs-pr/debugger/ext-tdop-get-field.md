---
title: EXT\_TDOP\_GET\_FIELD
description: EXT\_TDOP\_获取\_字段的调试子操作\_请求\_EXT\_类型化\_数据\_ANSI 请求的操作返回类型化的数据表示给定结构的成员的说明。
ms.assetid: c91c0ecf-c093-4585-a6b5-6bda91899ec3
keywords:
- EXT_TDOP_GET_FIELD Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_FIELD
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d15a0fd165d1756353143385f5922148a7664b75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346283"
---
# <a name="exttdopgetfield"></a>EXT\_TDOP\_GET\_FIELD


EXT\_TDOP\_获取\_字段的子操作[**调试\_请求\_EXT\_类型化\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md) [**请求**](request.md)操作将返回表示给定结构的成员的类型化的数据说明。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**Operation**  
设置为 EXT\_TDOP\_获取\_此子操作的字段。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定的实例[**调试\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff541706)描述所需其成员的结构。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收的实例[**调试\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff541706)为请求的成员。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
指定请求的成员的名称。 成员的名称是以点号分隔的路径和包含子成员-例如， **mymember.mysubmember**。 将自动取消引用此以点号分隔的路径上的指针。 但是，点运算符 (**。**) 仍可使用此处而不是常用的 C 指针取消引用运算符 (**-&gt;**)。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
接收此子操作返回的状态代码。 这是与返回的值相同[**请求**](request.md)。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_获取\_字段是中的值[ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)枚举。

此子操作的参数属于[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)结构。 EXT 隶属\_类型化\_前面的参数部分中未列出的数据不使用此子操作，应设置为零。 前面的 Parameters 节中的成员的说明指定使用的成员。 请参阅**EXT\_类型化\_数据**的更多详细信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DEBUG\_REQUEST\_EXT\_TYPED\_DATA\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**请求**](request.md)

 

 






