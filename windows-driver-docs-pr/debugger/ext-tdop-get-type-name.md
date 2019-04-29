---
title: EXT\_TDOP\_GET\_TYPE\_NAME
description: EXT\_TDOP\_获取\_类型\_NAME 子操作的调试\_请求\_EXT\_类型化\_数据\_ANSI 请求操作返回指定的类型化数据的类型名称。
ms.assetid: ce896ded-a49e-4f89-969e-6d464e583ca8
keywords:
- EXT_TDOP_GET_TYPE_NAME Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_TYPE_NAME
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 132d5a92956d3fed4dd25e0b7a4c8e10688c3ab0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379892"
---
# <a name="exttdopgettypename"></a>EXT\_TDOP\_GET\_TYPE\_NAME


EXT\_TDOP\_获取\_类型\_名称的子操作[**调试\_请求\_EXT\_类型化\_数据\_ANSI**](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作将返回指定的类型化数据的类型名称。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**Operation**  
设置为 EXT\_TDOP\_获取\_类型\_此子操作的名称。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定正在请求其类型名称的类型化的数据。

<span id="StrBufferIndex"></span><span id="strbufferindex"></span><span id="STRBUFFERINDEX"></span>**StrBufferIndex**  
接收的类型名称。

<span id="StrBufferChars"></span><span id="strbufferchars"></span><span id="STRBUFFERCHARS"></span>**StrBufferChars**  
指定的大小，以字符为单位的 ANSI 字符串缓冲区**StrBufferIndex**。

<span id="StrCharsNeeded"></span><span id="strcharsneeded"></span><span id="STRCHARSNEEDED"></span>**StrCharsNeeded**  
接收大小，以字符为单位的类型名称。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
接收此子操作返回的状态代码。 这是与返回的值相同[**请求**](request.md)。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_获取\_类型\_名称是中的值[ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)枚举。

此子操作的参数属于[ **EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)结构。 EXT 隶属\_类型化\_前面的参数部分中未列出的数据不使用此子操作，应设置为零。 前面的 Parameters 节中的成员的说明指定使用的成员。 请参阅**EXT\_类型化\_数据**的更多详细信息。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DEBUG\_REQUEST\_EXT\_TYPED\_DATA\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_类型化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**请求**](request.md)

 

 






