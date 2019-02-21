---
title: EXT\_TDOP\_GET\_TYPE\_SIZE
description: EXT\_TDOP\_获取\_类型\_大小子操作的调试\_请求\_EXT\_类型化\_数据\_ANSI 请求操作返回指定的类型化数据的大小。
ms.assetid: 3e668522-60bb-4abc-87b8-6b1beea573a3
keywords:
- EXT_TDOP_GET_TYPE_SIZE Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_TYPE_SIZE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10e1481ff1b5e54ac5a2479ee7eda94978be54ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554886"
---
# <a name="exttdopgettypesize"></a>EXT\_TDOP\_GET\_TYPE\_SIZE


EXT\_TDOP\_获取\_类型\_大小的子操作[**调试\_请求\_EXT\_类型化\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作返回指定的类型化数据的大小。

**参数**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**Operation**  
设置为 EXT\_TDOP\_获取\_类型\_此子操作的大小。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定正在请求其大小的类型化的数据。

<span id="Out32"></span><span id="out32"></span><span id="OUT32"></span>**Out32**  
接收大小，以字节为单位的类型化数据。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
接收此子操作返回的状态代码。 这是与返回的值相同[**请求**](request.md)。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_获取\_类型\_大小是中的值[ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)枚举。

此子操作的参数属于[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)结构。 EXT 隶属\_类型化\_前面的参数部分中未列出的数据不使用此子操作，应设置为零。 前面的 Parameters 节中的成员的说明指定使用的成员。 请参阅**EXT\_类型化\_数据**的更多详细信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DEBUG\_REQUEST\_EXT\_TYPED\_DATA\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**请求**](request.md)

 

 






