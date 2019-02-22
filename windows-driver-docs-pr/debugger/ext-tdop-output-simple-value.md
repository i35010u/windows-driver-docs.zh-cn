---
title: EXT\_TDOP\_输出\_简单\_值
description: EXT\_TDOP\_输出\_简单\_值子操作的调试\_请求\_EXT\_类型化\_数据\_ANSI 请求操作将打印指定的类型化数据的值。
ms.assetid: dce51823-34e9-43b9-9cbd-41b436b43ccb
keywords:
- EXT_TDOP_OUTPUT_SIMPLE_VALUE Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_SIMPLE_VALUE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: acaf37b2c3c1c157a112b23a0cf0da3b7607eed2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525301"
---
# <a name="exttdopoutputsimplevalue"></a>EXT\_TDOP\_输出\_简单\_值


EXT\_TDOP\_输出\_简单\_值的子操作[**调试\_请求\_EXT\_类型化\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作将打印指定的类型化数据的值。

**参数**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**Operation**  
设置为 EXT\_TDOP\_输出\_简单\_此子操作的值。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定将打印其值的类型化的数据。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
接收此子操作返回的状态代码。 这是与返回的值相同[**请求**](request.md)。

<a name="remarks"></a>备注
-------

值的格式，并且发送到调试器引擎[输出回调](https://msdn.microsoft.com/library/windows/hardware/ff560116#output-callbacks)。

EXT\_TDOP\_输出\_简单\_值是中的值[ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)枚举。

此子操作的参数属于[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)结构。 EXT 隶属\_类型化\_前面的参数部分中未列出的数据不使用此子操作，应设置为零。 前面的 Parameters 节中的成员的说明指定使用的成员。 请参阅**EXT\_类型化\_数据**的更多详细信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DEBUG\_REQUEST\_EXT\_TYPED\_DATA\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**请求**](request.md)

 

 






