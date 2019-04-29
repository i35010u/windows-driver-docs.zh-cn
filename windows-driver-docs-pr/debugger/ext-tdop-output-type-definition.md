---
title: EXT\_TDOP\_输出\_类型\_定义
description: EXT\_TDOP\_输出\_类型\_定义子操作的调试\_请求\_EXT\_类型化\_数据\_ANSI 请求操作将打印指定的类型化数据类型的定义。
ms.assetid: 88e97066-f471-4e6c-9b9b-369f31da5bde
keywords:
- EXT_TDOP_OUTPUT_TYPE_DEFINITION Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_TYPE_DEFINITION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b60acaae7a16995166aa64a58b6b57f28c22b852
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379889"
---
# <a name="exttdopoutputtypedefinition"></a>EXT\_TDOP\_输出\_类型\_定义


EXT\_TDOP\_输出\_类型\_定义的子操作[**调试\_请求\_EXT\_类型化\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作打印指定的类型化数据类型的定义。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**Operation**  
设置为 EXT\_TDOP\_输出\_类型\_此子操作定义。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定将打印其类型定义的类型化的数据。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
接收此子操作返回的状态代码。 这是与返回的值相同[**请求**](request.md)。

<a name="remarks"></a>备注
-------

格式化类型的定义并将其发送到调试器引擎[输出回调](https://msdn.microsoft.com/library/windows/hardware/ff560116#output-callbacks)。

EXT\_TDOP\_输出\_类型\_定义是中的值[ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)枚举。

此子操作的参数属于[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)结构。 EXT 隶属\_类型化\_前面的参数部分中未列出的数据不使用此子操作，应设置为零。 前面的 Parameters 节中的成员的说明指定使用的成员。 请参阅**EXT\_类型化\_数据**的更多详细信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DEBUG\_REQUEST\_EXT\_TYPED\_DATA\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**请求**](request.md)

 

 






